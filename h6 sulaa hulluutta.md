## h6 Sulaa hulluutta

### a) Tutki tiedostoa h1.jpg jo opituilla työkaluilla. Mitä saat selville?

Tarkoituksena tehtävässä oli tutkia h1.jpg tunnilla opituilla työkaluilla. En ole ihan varma käytiinkö viimeisemmällä tunnilla jotain uusia työkaluja läpi, koska en päässyt osallistumaan sairastumisen vuoksi. Aloitin tekemään tehtävää lataamalla kuvan virtuaalikoneelleni.
Ensimmäisenä kokeilin komentoa ``cat h1.jpg``, tämä lähinnä antoi vain binääridataa ulos, mistä ei oikein ottanut mitään selkoa.

Seuraavaksi lähdin käyttämään ``file h1.jpg`` komentoa saadakseni tietoa kyseisestä tiedostosta. Saatiin ainakin selville, että kuva nyt on ainakin JPEG-tiedosto.

![image](https://github.com/user-attachments/assets/d2266b67-924d-41a4-9f5b-f3de0c8431d8)

Tämän jälkeen lähdin kokeilemaan jo tunnilla tutuksi tullutta ``strings h1.jpg`` ja tämä tulosti tajuttoman määrän luettavaa tekstiä. Selasin koko tekstin läpi ja se oli pääosin aika samankaltaista.

![image](https://github.com/user-attachments/assets/445601ac-15fd-405a-a21e-a73ed7490b46)

Löysin tietoa netistä (https://infosecwriteups.com/beginners-ctf-guide-finding-hidden-data-in-images-e3be9e34ae0d), että binwalk tai exitfool työkaluista voisi olla apua tiedoston tutkimisessa, joten päätin asentaa ne virtuaalikoneelleni. Kummastakaan minulla ei ollut aikaisempaa kokemusta.

    $ sudo apt install libimage-exiftool-perl -y

    $ sudo apt install binwalk

Exiftoolin antamaa näkymää. Nämä tiedot eivät ainakaan minun mielestäni herättänyt mitään poikkeuksellisen erinevää tietoa mihin tarttuisin tarkemmin.

![image](https://github.com/user-attachments/assets/4b1c6d53-0e72-43d8-a627-d06f0a38b921)

![image](https://github.com/user-attachments/assets/105e8501-d005-4fa1-81ea-f1aed5c0072a)

En tiedä olisiko vielä ollut tarkoitus saada enemmän tietoa esille, tai käytiinkö tunnilla vielä lisää läpi jotain eri metodeja tutkimista varten. Suoritin komennon ``binwalk h1.jpg`` tämän pitäisi analysoida tiedosto ja näyttää kaikki sisäiset tiedostot, kuten pakatut tiedostot, piilotetut tiedostot ja metatietoja. 


### b) Tutki tiedostoa h1.jpg binwalk:lla. Mitä tietoja löydät nyt tiedostosta? Mitä työkalua käyttäisit tiedostojen erottamiseen? (Huomaa, että binwalk versio 2.x ja 3.x toimivat eri tavalla.)

Binwalk tulikin jo ladattua A tehtävässä, joten jatkan binwalkilla h1.jpg tiedoston tutkimista. Suoritin komennon ``binwalk h1.jpg`` tämän pitäisi analysoida tiedosto ja näyttää kaikki sisäiset tiedostot, kuten pakatut tiedostot, piilotetut tiedostot ja metatietoja.

![image](https://github.com/user-attachments/assets/c627b7f6-6af8-40e7-ba42-b79a775ea28e)

Binwalkilla selvisi, että tiedoston sisällä on paljon zip arkiston osia. Sieltä löytyy myös paljon xml tiedostoja, erityisesti kiinnostukseni herätti word/document.xml. En oikein tiennyt, mitä tässä kohti tekisin, joten kysyin tekoälyltä apua. Tekoäly ehdotti kokeilemaan komentoa ``binwalk -e h1.jpg``. Tämän tarkoituksena on purkaa zip rakenteet ja laittaa ne erillisiin hakemistoihin.

![image](https://github.com/user-attachments/assets/77e9767c-ed5e-4d6c-b9ca-a53dc04d6034)

Niinkun näkyy, luotu uusi hakemisto, mistä löytyy eriteltyjä osia tiedostosta. 

Lähdin tutkimaan hieman eriosia tiedostosta. ``docProps`` löytyi ``core.xml`` tiedosto. Tämä näyttää esimerkiksi perusmetatiedot, mistä näkyy tekijä ja ajankohta. 

![image](https://github.com/user-attachments/assets/4ade906b-1406-4699-ac89-3af79d480050)

``docProps`` löytyi myös ``app.xml`` mikä näyttää sovelluskohtaiset metatiedot.

![image](https://github.com/user-attachments/assets/48a5d1f8-fec4-48ec-b52b-9a91636884b5)

Puretuissa hakemistoissa oli yksi "purkamaton" zip tiedosto. Yritin purkaa kyseistä tiedostoa, mutta se ei onnistunut. Tarkastelin kyseistä tiedostoa file komennolla ja selvisi, että se on word tiedosto, minkä takia purkaminen ei onnistunut.

![image](https://github.com/user-attachments/assets/d16928d5-9be5-44c8-b646-4f5407443208)

Puretuissa hakemistoissa oli myös ``word``, minkä sisältä löytyi ``document.xml`` tutkailin myös tämän sisältöä ja sieltä löytyi linkkejä ja vähän erikoista tekstiä.

![image](https://github.com/user-attachments/assets/9210c737-159f-4646-9737-9dbc80fbf8fc)

Jäi häiritsemään tekstin sisältö, joten päädyin tutkailemaan sitä viel XML viewerillä. Käytännössä tiedostossa oli Ennustukset 50v päähän.

![image](https://github.com/user-attachments/assets/229518bf-1dee-43ec-847a-d7f03162c53e)



### c) FOSS (Free Android OpenSource). Tutustu Android-sovelluksiin Offan (2024) listalta: Android FOSS. Valitse listalla itsellesi mielenkiintoisin applikaatio ja mene sen GitHubiin. Lataa ohjelman APK itsellesi ja käytä seuraavia työkaluja tutustuaksesi, miten APK:n voi avata.
  - ZIP
  - JADX
  - Bytecode-viewer


Aloin tutustumaan listaan sivustolla https://github.com/offa/android-foss. Sovelluksia oli ihan tajuton määrä, joten hetki meni miettiessä minkä niistä valitsisi. Arpanumero osui kyseiseen sovellukseen: https://github.com/m-i-n-a-r/birday. Eli käytännössä sovellus mikä muistaa syntymäpäivät ja tapahtumat. Siirryin seuraavaksi lataamaan ohjelman APKta itselleni. (Android Package Kit) tiedostomuoto, mitä käytetään androidille ladatessa. 

Aloitin tutustumalla miten se avataan **ZIP**:illä. Ensiksi uudelleen nimeämällä sen ja purkamalla:

        $ mv Birday-451.apk Birday-451.zip
        $ unzip Birday-451.zip

![image](https://github.com/user-attachments/assets/30fd43d2-b8df-4e5b-a793-eccdd9297aee)

Tiedoston purku onnistui, se tuli vähän vammaisesti hajautettuna Downloads kansioon sen jälkeen.

![image](https://github.com/user-attachments/assets/7f7a1fd2-d1e9-4f24-8ea5-3d836ae77dc0)

Alla olevat tiedot ovat kyseisen tiedoston sisältämiä.

 - META-INF/: Contains metadata.
 - res/: Resources like images, layout XML files, etc.
 - AndroidManifest.xml: The app’s manifest file that contains important information like permissions.
 - classes.dex: The compiled Java code (which you’ll need other tools to view in readable format).


Tässä vaiheessa voin käsittääkseni vain tutkia ja analysoida resursseja ja luettelotiedostoa, mutta Java-koodin analysointiin tarvitsen muita työkaluja. Ne ovat ymmärtääkseni juuri nämä kyseiset JADX tai Bytecode Viewer.

Aloin tutustumaan **JADX**:in käyttöön kyseisellä sivustolla: https://github.com/skylot/jadx/releases/tag/v1.5.1. Latasin JADX:in

        $ git clone https://github.com/skylot/jadx.git

        ~jadx$ ./gradlew dist

Luulen, että lataaminen releaseista olisi ollut huomattavasti nopeampaa, mutta mentiin nyt tällä. Kestää kestää, käyn pakkaamassa kertauskamat tässä välissä. Meni liian sekavaksi, enkä oikein saanut toimimaan tätä kautta, joten poistin JADXin ja lähdin lataamaan sieltä releaseista. 

Latasin paketin virtuaalikoneelleni. ``jadx-1.5.1.zip``. Purin paketit tämän jälkeen. Ladattuani paketit lähdin käynnistämään JADX:ia

        $ ./jadx-gui

Kun JADX avautui, siirsin kyseisen Birdayn apk tiedoston ohjelmaan.

![image](https://github.com/user-attachments/assets/57e959c7-5256-482d-b146-63dec9cc11ce)

Ohjelma avasi kyseisen sovelluksen tiedot, mitä pystyi kätevästi tutkailemaan sen kautta. Tämän kautta, näki esimerkiksi lähdekoodia.

![image](https://github.com/user-attachments/assets/3e490f98-845f-492f-9c57-74418f196821)

![image](https://github.com/user-attachments/assets/dd92460e-fcb9-4c9b-89ef-20dd719552d8)

Viimeisenä oli vielä tarkoitus tarkastella **Bytecode Vieweriä**. Latasin kyseisen ohjelman https://github.com/Konloch/bytecode-viewer. Tuttuun tyyliin purettiin taas paketit.

Käynnistin sovelluksen komennolla:

        $ java -jar Bytecode-Viewer-2.12.jar

Sovellusnäkymä avautuneena:

![image](https://github.com/user-attachments/assets/dc359307-e682-4565-9b83-90b59d583879)

Tuntuu toimivan aika samantyylisesti kun JADX, eli mahdollistavat esimerkiksi APK pakettien tutkimisen ja purkamisen.

![image](https://github.com/user-attachments/assets/215840cf-7c18-431b-90a6-1228e688ccce)


### Lähteet

https://terokarvinen.com/application-hacking/#laksyt

https://github.com/skylot/jadx/releases/tag/v1.5.1

https://github.com/Konloch/bytecode-viewer

https://github.com/offa/android-foss?tab=readme-ov-file#-calculator

https://chatgpt.com 

https://github.com/m-i-n-a-r/birday

https://infosecwriteups.com/beginners-ctf-guide-finding-hidden-data-in-images-e3be9e34ae0d









