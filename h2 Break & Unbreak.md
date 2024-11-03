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

    sql = "SELECT password FROM pins WHERE pin = :pin" # Käyttää :pin paikkamerkkiä SQL kyselyssä, eikä se toimi varsinaisena arvona.
    db.session.execute(text(sql), {"pin": pin}) # Käyttää kyseistä sanakirjaa, mikä sisältää avaimen pin ja se vastaa paikkamerkkiä :pin. Sekä käyttäjän syötteen eli pin. SQLalchemy korvaa datan paikkamerkillä niin ettei SQL rakennetta voi muuttaa.




### c) Ratkaise dirfuzt-1 artikkelista Karvinen 2023: Find Hidden Web Directories - Fuzz URLs with ffuf. Tämä auttaa 020-your-eyes-only ratkaisemisessa.
### d) Murtaudu 020-your-eyes-only. Ks. Karvinen 2024: Hack'n Fix
### e) Korjaa 020-your-eyes-only haavoittuvuus. Osoita testillä, että ratkaisusi toimii.
