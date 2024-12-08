### x) Lue/katso/kuuntele ja tiivistä. (Tässä x-alakohdassa ei tarvitse tehdä testejä tietokoneella, vain lukeminen tai kuunteleminen ja tiivistelmä riittää. Tiivistämiseen riittää muutama ranskalainen viiva.)

**€ Schneier 2015: Applied Cryptography, 20ed: Chapter 1: Foundations:**

- 1.1 Terminology ("Historical Terms" loppuun)
  
  - Käsitellään salakirjoituksen erilaisia termejä ja yleiskäsitteitä. Esimerkkinä *plaintext*, mikä kertoo viestin alkuperäisessä muodossaan, *ciphertext*, mikä kertoo salauksen tuloksen.

  - Kryptografiassa nojaudutaan myös kolmeen eri kohtaan luotettavuuden takaamiseksi, Authentication, Integrity ja Nonrepudiation.
 
  - Kryptografiassa käytetään algotrimia, mitä kutsutaan *cipher*. Matemaattinen funktio, mikä auttaa encryptaamaan ja decryptaamaan. Modernissa kryptografiassa käytetään erilaisia avaimia suojaamaan algoritmeja.
  
- 1.4 Simple XOR

   - Ekskluusvinen or operaatio.
 
   - Looginen operaatio, joka palauttaa "true" vain jos molemmat syötteet eroavat toisistaan.
 
   - Helppo ja tehokas tapa krypata dataa. Selvä kieli yhdistetään salausavaimeen kanssa bittitasolla.
     
- 1.7 Large Numbers

   - Lukujen merkitystä kryptografiassa
 
   - Luotu taulukko, mikä auttaa hahmottamaan suuria lukuja paremmin.
     

**Karvinen 2024: Python Basics for Hackers**

 - Teron luomia ohjeita pythonin käyttöön tukemaan hakkerointia

 - REPL, iPython, F5 compile

 - Pythonin käyttö esimerkiksi laskimena



### Ratkaise CryptoPals Set 1 -haasteet. Tehtävät saa ratkaista millä vain ohjelmointikielellä ja käyttää mitä tahansa tekstieditoria tai IDE:ä. Tehtäviä ei kannata ratkaista tekoälyllä, koska se vain kopioi malliratkaisun suoraan koulutusmateriaalistaan.

Ei ollut hirveästi hajua näistä tehtävistä, ja en muutenkaan ole hirveä fani koodaamisen kanssa. Mutta päätin lähteä siitä huolimatta tutkimaan, miten näitä tehtäviä voisi ratkaista ja saada parempaa ymmärrystä kyseisistä asioista.

#### a) 1. Convert hex to base64.

Teron ohjeissa sanottiin, että mikä tahansa tekstieditori ja koodikieli olisi käyttökelpoinen. Päädyin microon ja pythoniin. Aloitin lataamalla microeditorin virtuaalikoneelleni.

    sudo apt install micro

Tarkoituksena muuntaa cryptopalsin sivustolla oleva hexadesimaali pätkä base64 muotoon. Aloitin luomaan python koodia microeditorilla, jotta saisin muunnettua sen oikeaan muotoon.

![image](https://github.com/user-attachments/assets/722f6fb5-2f01-4ba7-acaa-7c573e98bc32)

``import base64`` - importaan base64, mikä auttaa base64 koodausta ja purkua

``HEX_STRING =`` - Tähän tulee hexadesimaalinen string

``BYTE_ARRAY = bytearray.fromhex(HEX_STRING)`` - muuntaa hexadesimaalisen stringin binääridataa vastaavaksi tavutaulukoksi

``print(BYTE_ARRAY)`` - tulostetaan tavutaulukko (BYTE_ARRAY), binääridata näkyy ihmisen luettavana

``BASE64_VAL = base64.b64encode(BYTE_ARRAY)`` - binäärimuotoinen taulukko koodataan base64 muotoon

``print(BASE64_VAL)`` - tulostaa koodatun base64 merkkijonon



![image](https://github.com/user-attachments/assets/7f263ff1-8116-4d75-be45-7b955bfd5d38)

Valmis lopputulos, mikä näkyy kun ajetaan kyseinen python tiedosto. Ollaan onnistuttu kääntämään hexadesimaaleista base64 muotoon, sekä nähdään sen lisäksi vielä byte_arrayn kautta teksti. En tiedä olisko pelkkä base64 muotoinen stringi ollut riittävä tähän tehtävään pelkästään.


#### b) 2. Fixed XOR.

Aika ja osaaminen ei riittänyt ratkaisemaan tätä tehtävää, tutkiskelin erilaisia foorumeita ja sivustoja, mistä sain jonkin näköisen kuvan mitä tässä haluttaisiin tehdä, mutta omalla osaamistasollani ei riittänyt. Koodaaminen on muutenkin asia, mistä en hirveästi nauti ja se ei tunnu omalta jutulta.

#### c) 3. Single-byte XOR cipher.

#### d) 4. Detect single-character XOR.


### Lähteet

https://terokarvinen.com/application-hacking/#laksyt

https://terokarvinen.com/getting-started-python-cryptopals/

https://terokarvinen.com/python-for-hackers/

https://cryptopals.com/sets/1

https://www.oreilly.com/library/view/applied-cryptography-protocols/9781119096726/08_chap01.html#chap01-sec001
