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

![image](https://github.com/user-attachments/assets/e8b5a51d-adc7-494f-bf0a-4bca5da7264e)




  Löydettiin ip-osoite, missä sovellus on käynnissä ja lähdettiin sitä kohti seuraavaksi.

  Tarkoitus oli selvittää SUPERADMININ salasana, kokeilin eri variaatioita esimerkiksi 123 mitä ohjeistettiin. Tämä paljasti salasanan. Huomasin, että kenttään ei voinut kirjoittaa tekstiä vaan pelkkiä numeroita, joten lähdin tutkimaan tiedostoja lisää. Siirryin templateseihin ja sieltä löytyi index.html tiedosto, jota lähdin tutkailemaan micro tekstieditorilla.

  ![image](https://github.com/user-attachments/assets/6c1ba84d-00f6-48d5-9946-231f20b28b8a)

  Tutkailtuani koodia, selvisi että vain numeroita pystyi kirjoittamaan, joten pyyhin sen pois koodista. Käynnistin uudelleen staff-only.py tiedoston ja siirryin selaimeen kokeilemaan toimiko muutokset. Nyt pystyin kirjoittamaan tekstiä salasanakenttään ja lähdin kokeilemaan saisinko salasanan selvitettyä. Hyödynsin tunnilla opittuja SQL-injektiossa käytettäviä komentoja ja sain SUPERADMININ salasanan selville.

  ![image](https://github.com/user-attachments/assets/929adfa5-9b98-4e1a-b177-91da6fd4af69)


  ![image](https://github.com/user-attachments/assets/5990f2c7-ba70-439b-9fff-91c6cd9d9352)




### b) Korjaa 010-staff-only haavoittuvuus lähdekoodista. Osoita testillä, että ratkaisusi toimii.
### c) Ratkaise dirfuzt-1 artikkelista Karvinen 2023: Find Hidden Web Directories - Fuzz URLs with ffuf. Tämä auttaa 020-your-eyes-only ratkaisemisessa.
### d) Murtaudu 020-your-eyes-only. Ks. Karvinen 2024: Hack'n Fix
### e) Korjaa 020-your-eyes-only haavoittuvuus. Osoita testillä, että ratkaisusi toimii.
