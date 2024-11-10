### a) Strings. Lataa ezbin-challenges.zip Aja 'passtr'. Selvitä oikea salasana 'strings' avulla. Selvitä myös lippu. (Ensisijaisesti katsomatta sorsia, jos osaat.)

Aloitin tehtävän siirtymällä Teron sivuille, ja lataamalla zip paketin. Paketista löytyi aika nopeasti "passtr" tiedosto, joten siirryin cmd:hen seuraavaksi.

![image](https://github.com/user-attachments/assets/77dc73d8-23d7-4a66-80ca-0677d0cdcb45)

Purin kyseisen tiedoston ja tutkailin vähän sisältöä sen jälkeen, miltä se näyttää.

![image](https://github.com/user-attachments/assets/7f6c4dd3-5a9c-4e50-adf0-d0f185c66f09)

Siirryin ajamaan kyseistä "passtr" tiedostoa strings ohjelmalla, ja ohjelma tulosti paljon tekstiä, minkä mukana löytyi myös flagi.

![image](https://github.com/user-attachments/assets/35176284-09b1-4b11-abd8-482030e1535d)


### b) Tee passtr.c -ohjelmasta uusi versio, jossa salasana ei näy suoraan sellaisenaan binääristä. Osoita testillä, että salasana ei näy. (Obfuskointi riittää.)

Tämä tehtävä tuotti aika paljon hankaluuksia, koska C kieli ei ollut yhtään tuttu. Avasin tiedoston kyllä micro tekstieditorilla ja tutkiskelin koodia parhaani mukaan. 

![image](https://github.com/user-attachments/assets/2e2d8de1-8868-4be4-ab6d-1efd233db484)

Oli pakko ottaa tekoäly käyttöön, että saisin jotain selkoa asiasta. Sitä tutkiskeltuani, sain vähän käsitystä miten koodia muutettaisiin ja mikä sen virka siinä olisi. Muutettu koodi alapuolella:

![image](https://github.com/user-attachments/assets/e9c0a04d-8b81-4b1c-950b-d0d6df444590)

Tarkoitus tässä oli peittää salasana, jotta se ei näkyisi suoraan binäärissä. Käytettiin XOR-koodausta sen peittämiseen. Alkuperäinen salasana on koodattu avaimella 0x5A, ja tallennettuna obsfuktoituna merkkijonona muuttujaan obfuscted_password. XOR-koodaus tekee salasanasta lukukelvottoman. xor_decrypt funktio vastaanottaa salatun merkkijonon ja purkaa sen suorittamalla saman operaation samalla avaimella. Mahdollistaa alkuperäisen salasanan palauttamisen vertailua varten. main funktiossa ohjelma kysyy käyttäjältä salasanaa ja vertaa sitä alkuperäiseen salasanaan, jos se täsmää tulee onnistumisviesti, muutoin ilmoitus väärästä salasanasta. Vertailun jälkeen ohjelma XORaa sen obsfuskoituun muotoon, jolloin se ei jää ohjelman muistiin. 

![image](https://github.com/user-attachments/assets/7926b00f-a8f2-4aca-9e8f-df3697ac3354)

Kokeilin vielä oikealla salasanalla, palauttaisiko se minulle Flagin, mutta en saanut sitä onnistumaan. Tutkin koodia ja koitin selvittää mikä siinä oli vikana, mutta en saanut sitä selvitettyä. Eli sain sen piilotettua binääristä, mutta oikealla salasanalla en saanut sitä palautettua jostain syystä.

![image](https://github.com/user-attachments/assets/682fc706-9bbf-49f3-8b8f-c2e6ae6091b4)



### c) Packd. Aja 'packd' paketista ezbin-challenges.zip. Mikä on salasana? Mikä on lippu? (Tämä tehtävä on hieman haastavampi. Kirjaa ylös kokeilemasi lähestymistavat ja keksimäsi hypoteesit. Toivottavasti pääset itse maaliin, mutta jos et, läpikävely paljastuu tunnilla...)

Lähdin tutkimaan kyseistä tiedostoa strings komennolla ja sieltä löytyi osia halutusta salasanasta ja lipusta, mutta ne olivat pilkottu eri osiin. En saanut ratkaistua kyseistä tehtävää, mutta uskoisin, että ideana olisi tarkoitus luoda erillinen koodi, millä pystyisi lukemaan kyseisen tiedoston sisällön.


![image](https://github.com/user-attachments/assets/db03ea37-247d-4913-9418-35636f565c5e)


### Lähteet

https://terokarvinen.com/application-hacking/#laksyt

https://chatgpt.com



