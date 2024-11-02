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

  Unzippaamisen jälkeen seikkailin itseni kyseiseen kansioon ja sieltä löytyi tehtävät.

### b) Korjaa 010-staff-only haavoittuvuus lähdekoodista. Osoita testillä, että ratkaisusi toimii.
### c) Ratkaise dirfuzt-1 artikkelista Karvinen 2023: Find Hidden Web Directories - Fuzz URLs with ffuf. Tämä auttaa 020-your-eyes-only ratkaisemisessa.
### d) Murtaudu 020-your-eyes-only. Ks. Karvinen 2024: Hack'n Fix
### e) Korjaa 020-your-eyes-only haavoittuvuus. Osoita testillä, että ratkaisusi toimii.
