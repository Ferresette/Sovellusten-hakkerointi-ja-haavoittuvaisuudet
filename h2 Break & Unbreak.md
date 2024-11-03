### x) Lue/katso/kuuntele ja tiivistä.

**- OWASP: OWASP Top 10: A01 Broken Access Control** 

  Mahdollisuus päästä käsiksi tietoihin tai toimintoihin mihin ei kuuluisi päästä. Syynä useasti heikot pääsynvalvonta toteutukset. Mahdollisuus tietovuotoihin, tietojen muuttamiseen tai järjestelmän kaatumiseen.

**- Karvinen 2023: Find Hidden Web Directories - Fuzz URLs with ffuf**

  Avoimen lähdekoodin netti fuzzeri, millä koitetaan löytää haavoittuvaisuuksia yleensä hakemisto/tiedostopoluista web palvelimelta. Äärimmäisen nopea ja tehokas työkalu.

**- PortSwigger: Access control vulnerabilities and privilege escalation**

  Liittyy edellä mainittuun Broken Access Controliin, privilege escalation tarkoittaa, että hyökkääjä saa korotettua käyttäjäoikeuksiaan. Esimerkiksi norimikäyttäjästä järjestelmänvalvojaksi.

**- Karvinen 2006: Raportin kirjoittaminen**

  Teron vinkit raportin kirjoittamiseen. Hyviä ohjeita, mitä olen monia itsekin pyrkinyt hyödyntämään parhaani mukaan.

**- Vapaaehtoinen: PortSwigger 2020: What is SQL injection? - Web Security Academy (noin 10 min video)**

  SQL injektio on hyökkäysmetodi, missä yritetään syöttää haitallista SQL koodia syötekenttään tai url osoitteeseen. Tällä tavalla voidaan saada manipuloitua tietokantaa. Johtuu yleensä heikosta validoinnista ennen SQL kyselyn suorittamista.


### a) Murtaudu 010-staff-only. Ks. Karvinen 2024: Hack'n Fix

  Minulta löytyi aikaisemmin ohjeistettu ladattava Debian 12 Bookworm, millä lähdin ratkaisemaan tehtäviä. Aloitin lataamalla micro tekstieditorin ensimmäiseksi.
  
      sudo apt update
      sudo apt install micro

  Tämän jälkeen teron sivuilla oli zippi paketti tehtävää varten, joten aloitettiin lataamalla se. Tämän jälkeen unzipattiin paketti. Aluksi minulla ei toiminut wget komento, mutta selvisi ettei sitä ollut valmiiksi asennettuna joten täytyi ladata se myös.

      $ wget https://terokarvinen.com/hack-n-fix/teros-challenges.zip
      $ unzip teros-challenges.zip

![image](https://github.com/user-attachments/assets/dd98d5d7-a4ae-4087-a75b-bce80d19923d)

  Unzippaamisen jälkeen seikkailin itseni kyseiseen kansioon ja sieltä löytyi tehtävät. Jatkoin lataamalla python 3 flaskin ja flaskin laajennuksen sqlachemyn, jotta tietokantakirjaston käyttö olisi helpompaa. Tämän jälkeen runnasin tiedostosta löytyvän python tiedoston python3:sella.

    $ sudo apt-get -y install python3-flask python3-flask-sqlalchemy
    $ python3 staff-only.py

  Löydettiin ip-osoite, missä sovellus on käynnissä ja lähdettiin sitä kohti seuraavaksi.

  Tarkoitus oli selvittää SUPERADMININ salasana, kokeilin eri variaatioita esimerkiksi 123 mitä ohjeistettiin. Tämä paljasti salasanan. Huomasin, että kenttään ei voinut kirjoittaa tekstiä vaan pelkkiä numeroita, joten lähdin tutkimaan tiedostoja lisää. Siirryin templateseihin ja sieltä löytyi index.html tiedosto, jota lähdin tutkailemaan micro tekstieditorilla.

  ![image](https://github.com/user-attachments/assets/6c1ba84d-00f6-48d5-9946-231f20b28b8a)

  Tutkailtuani koodia, selvisi että vain numeroita pystyi kirjoittamaan, joten pyyhin sen pois koodista. Käynnistin uudelleen staff-only.py tiedoston ja siirryin selaimeen kokeilemaan toimiko muutokset. Nyt pystyin kirjoittamaan tekstiä salasanakenttään ja lähdin kokeilemaan saisinko salasanan selvitettyä. Hyödynsin tunnilla opittuja SQL-injektiossa käytettäviä komentoja ja sain SUPERADMININ salasanan selville.

  ![image](https://github.com/user-attachments/assets/929adfa5-9b98-4e1a-b177-91da6fd4af69)


  ![image](https://github.com/user-attachments/assets/e8b5a51d-adc7-494f-bf0a-4bca5da7264e)

  OR 1=1 tarkoittaa ehto palauttaa aina true, koska 1=1 on aina totta. Limit sen sijaan rajaa tulosta. Tässä tapauksessa ohitettiin 2 riviä ja palautettiin yksi rivi. Vähän jäi mietityttämään, miksi juuri tuo 2,1 paljasti SUPERADMININ, koska 1,1 tai 3,1 näytti taas eri tuloksia.


### b) Korjaa 010-staff-only haavoittuvuus lähdekoodista. Osoita testillä, että ratkaisusi toimii.

Tutkiskeltuani python koodia yksi rivi pisti silmään, mistä ongelmat voisi johtua.

![image](https://github.com/user-attachments/assets/5f9f331a-d279-4d1b-993e-78076ba89aeb)

Aika paljon pyörittelin päässäni kaikenlaisia ajatuksia, mikä siinä olisi vialla tai miten sitä olisi järkevä modata toimivampaan kuntoon. Netistä selatessani sain käsityksen, että tällä hetkellä käyttäjänsyöte liitetään suoraan SQL kyselyyn ilman parametrisoitua kyselyä, mikä altistaa SQL injektiolle. 

![image](https://github.com/user-attachments/assets/95d5d970-558c-4962-a2b5-a890342d3936)

Yläpuolella näkyy muutettu python koodi, millä sain sen toimimaan. Eli luotiin parametrisoitu kysely. 

  **sql = "SELECT password FROM pins WHERE pin = :pin"** # Käyttää :pin paikkamerkkiä SQL kyselyssä, eikä se toimi varsinaisena arvona.
    
  **db.session.execute(text(sql), {"pin": pin})** # Käyttää kyseistä sanakirjaa, mikä sisältää avaimen pin ja se vastaa paikkamerkkiä :pin. Sekä käyttäjän syötteen eli pin. SQLalchemy korvaa datan paikkamerkillä niin ettei SQL rakennetta voi muuttaa.

  Muutosten jälkeen lähdin yrittämään sivustolle, toimisiko aikaisemmin käytettävä haavoittuvuus. Kuten kuvasta näkyy, komento ei enään paljastanut SUPERADMININ salasanaa.

  ![image](https://github.com/user-attachments/assets/d2ee690a-d250-49de-9201-c07d9cb3c5ac)

  Tässä tehtävässä kului aika kauan aikaa useampi tunti, ja hyödynsin kyllä chatgpt:tä tehtävän ratkaisussa lopussa. Yllättävän pienillä muutoksila sai ehkäistyä kyseisen haavoittuvuuden. Vaikka aluksi oli pieni käry, missä se sijaitsisi niin pitäisi olla hieman parempi käsitys pythonin ja sql:n toiminnasta kokonaisuudessaan sen selvittämiseksi.


### c) Ratkaise dirfuzt-1 artikkelista Karvinen 2023: Find Hidden Web Directories - Fuzz URLs with ffuf. Tämä auttaa 020-your-eyes-only ratkaisemisessa.

Tämä tehtävä olikin aikaisemmin tuttu Tunkeutumistestaus kurssilta. En lähtenyt tekemään kyseistä tehtävää uudelleen vaan kertasin tehtävän omasta GitHubistani, tässä vielä linkki siihen: https://github.com/Ferresette/tunku/blob/main/h3FuffFaster.md

### d) Murtaudu 020-your-eyes-only. Ks. Karvinen 2024: Hack'n Fix

Tehtävä alkoi siirtymällä 020-your-eyes-only tiedostoon. Tämän jälkeen teron ohjeissa ohjeistettiin luomaan virtuaalinen ympäristö.

    $ sudo apt-get -y install virtualenv # lataa virtualenvin

    $ virtualenv virtualenv/ -p python3 --system-site-packages # luo virtualenv ympäristön käyttäen python3:sta ja sallii pakettejen käytön ympäristössä

![image](https://github.com/user-attachments/assets/76a8b9ac-5aef-4290-a8b0-4b3dd00eaade)

Seuraavaksi aktivoidaan virtualenv ja django toimii vain jos se on aktivoituna.

![image](https://github.com/user-attachments/assets/db8c9112-ba3a-4290-82bf-e5786bb0b5b2)

Seuraavaksi tutkittiin mitä requirements.txt pitää sisällään ja sieltä löytyi django. Siirryttiin lataamaan kyseinen tiedosto ja django pitäisi olla asennettuna. Tarkastettiin, että versio oli vielä oikein eli *4.2.16*.

![image](https://github.com/user-attachments/assets/e5db44b9-4e5e-45bd-b0bd-dfb39fa054ec)

Seuraavaksi päivitin databasen ja käynnistin testiserverin.

    $ ./manage.py makemigrations; ./manage.py migrate
    $ ./manage.py runserver

Hommat oli raiteillaan ja päästin tutkimaan sivustoa. 

![image](https://github.com/user-attachments/assets/3ef8d430-e247-40f4-ab23-89a61ce18ec1)


Sivustolta löytyi eri kohtia mitä pääsi klikkailemaan, login, register, show my personal data ja admin dashboard. Syötin vähän erilaisia tietoja, jotta näkisin millaista tulosta se antaa. 
Aloitin fuzzaamaan kyseistä sivustoa, koska sitä ehdotettiin vinkeissä. Latasin ffufin ja tekstilistat samaan tyyliin kun aikaisemmalla kurssilla. Fuzzaamisen ansiosta löysin admin-console tuloksen.

![image](https://github.com/user-attachments/assets/cc6787dc-f39d-4275-8907-62f75f86b489)

Muistelin edellisen kurssin tehtävistä, että urliin syöttämällä löydettyjä tietoja hommat pelitti usein aika hyvin. Pitkään koitin syötellä kyseistä admin-consolea urliin eri vaiheissa, mutta tuloksetta. Epätoivo meinasi jos iskeä, mutta vinkeistä huomasin että kirjautuminen saattaisi auttaa, joten rekistöröidyin sivulle. Kirjauduin sisään tunnuksella ja koitin nyt syöttää admin-consolea urliin ja kappas vaan sehän toimi.

![image](https://github.com/user-attachments/assets/1c496121-9038-4ffa-872e-620e71785db2)

Välillä turhauttaa aika paljon, kuinka pienestä kiinni ratkaisu voi olla. Käyttämällä monta tuntia asiaan, minkä periaatteessa voisi ratkaista minuutissa. Toisaalta onnistumisen tuoma hyvä fiilis ja itsensä pari kertaa idiootiksi haukkumisen jälkeen pääsee aika nopeasti takaisin jaloilleen.


### e) Korjaa 020-your-eyes-only haavoittuvuus. Osoita testillä, että ratkaisusi toimii.

Seuraavana tarkoitus oli korjata haavoittuvuus. Samaan tyyliin kun edellisessä tehtävässä lähdin tutkimaan python tiedostoja ja mitä ne pitivät sisällään. Hyvän tovin heiluin ja tutkin erilaisisa python tiedostoja. Aluksi olin vähän hakoteillä kun olin logtin/accounts/views.py/ polussa, en sieltä löytänyt ratkaisua. Tutkin lisää filejä ja huomasin että logtin/hats/ polusta löytyi myös views.py, missä oli eri koodi.

logtin/accounts/views.py näkymä microlla.

![image](https://github.com/user-attachments/assets/229c1627-2886-4ece-8227-93bab6d240f3)

logtin/hats/views.py näkymä microlla.

![image](https://github.com/user-attachments/assets/25e79190-1ed6-4b8f-9b32-fc933a0966d9)

Tämä jälkimmäinen näyttikin jo paljon lupaavammalta ratkaisun suhteen. Hetken silmäilyn jälkeen alkoi hahmottumaan. Kolme erilaista classia "MyDataView" eli oma profiili mihin päästiin sivustolla eteenpäin. Ja tämä vaatii kirjautumisen. Seuraava kohta "AdminDashbboardView" sinne kun koitti mennä tulee 403 forbidden vastaan. Eli kielletty, mutta koodissa on kohta, missä se vaatii käyttäjän olevan Staffia. Ja viimeisenä kohta oli "AdminShowAllView", millä oli samat vaatimukset kuin ensimmäisellä kohdalla. Päätin lisätä self.requestin staffiksi myös viimeiseen kohtaan, mikä todennäköisesti blockkaisi pääsyni nyt myös sinne. 

![image](https://github.com/user-attachments/assets/1818b61d-f9d7-4453-8453-890659b0a857)

![image](https://github.com/user-attachments/assets/bbd084aa-0ed5-4492-bc3d-edfb8ff0b659)

Tämän jälkeen pääsy oli myös evätty sinne. Koodia tutkimalla voi löytää virheitä näköjään aika helposti, tietty se vähän helpottaa kun tietää juuri mitä etsii. Harjoitukset oli hyviä, vaikka muutaman kerran epätoivo meinasi iskeä. Aikaa tehtävien suorittamiseen meni n. 7 tuntia.

### g) Vapaaehtoinen. Johdantotehtävä, joka auttaa 010-staff-only ratkaisemisessa. Ratkaise Portswigger Academyn "Lab: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data".

![image](https://github.com/user-attachments/assets/61ef4547-5098-4838-8efb-812cd6a35ab9)


### h) Vapaaehtoinen. Johdantotehtävä, joka auttaa 010-staff-only ratkaisemisessa. Ratkaise Portswigger Academyn "Lab: SQL injection vulnerability allowing login bypass"

![image](https://github.com/user-attachments/assets/44369dcb-22d7-4fb2-bfb7-abca75ab57bd)



### References

https://terokarvinen.com/application-hacking/#laksyt

https://terokarvinen.com/hack-n-fix/

https://terokarvinen.com/2023/fuzz-urls-find-hidden-directories/

https://portswigger.net/web-security/sql-injection/lab-retrieve-hidden-data

https://chatgpt.com

https://owasp.org/Top10/A01_2021-Broken_Access_Control/

https://portswigger.net/web-security/access-control



