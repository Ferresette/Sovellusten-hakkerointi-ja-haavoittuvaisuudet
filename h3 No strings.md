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

Tarkoitus tässä oli peittää salasana, jotta se ei näkyisi suoraan binäärissä. Käytettiin XOR-koodausta sen peittämiseen 



### c) Packd. Aja 'packd' paketista ezbin-challenges.zip. Mikä on salasana? Mikä on lippu? (Tämä tehtävä on hieman haastavampi. Kirjaa ylös kokeilemasi lähestymistavat ja keksimäsi hypoteesit. Toivottavasti pääset itse maaliin, mutta jos et, läpikävely paljastuu tunnilla...)
