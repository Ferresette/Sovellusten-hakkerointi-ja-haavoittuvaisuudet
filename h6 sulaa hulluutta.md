## h6 Sulaa hulluutta

### a) Tutki tiedostoa h1.jpg jo opituilla työkaluilla. Mitä saat selville?

Tarkoituksena tehtävässä oli tutkia h1.jpg tunnilla opituilla työkaluilla. En ole ihan varma käytiinkö viimeisemmällä tunnilla jotain uusia työkaluja läpi, koska en päässyt osallistumaan sairastumisen vuoksi. Aloitin tekemään tehtävää lataamalla kuvan virtuaalikoneelleni.
Ensimmäisenä kokeilin komentoa *cat h1.jpg*, tämä lähinnä antoi vain binääridataa ulos, mistä ei oikein ottanut mitään selkoa.

Seuraavaksi lähdin käyttämään *file h1.jpg* komentoa saadakseni tietoa kyseisestä tiedostosta. Saatiin ainakin selville, että kuva nyt on ainakin JPEG-tiedosto.

![image](https://github.com/user-attachments/assets/d2266b67-924d-41a4-9f5b-f3de0c8431d8)

Tämän jälkeen lähdin kokeilemaan jo tunnilla tutuksi tullutta *strings h1.jpg* ja tämä tulosti tajuttoman määrän luettavaa tekstiä. Selasin koko tekstin läpi ja se oli pääosin aika samankaltaista.

![image](https://github.com/user-attachments/assets/445601ac-15fd-405a-a21e-a73ed7490b46)

Löysin tietoa netistä (https://infosecwriteups.com/beginners-ctf-guide-finding-hidden-data-in-images-e3be9e34ae0d), että binwalk tai exitfool työkaluista voisi olla apua tiedoston tutkimisessa, joten päätin asentaa ne virtuaalikoneelleni. Kummastakaan minulla ei ollut aikaisempaa kokemusta.

    sudo apt install libimage-exiftool-perl

    sudo apt install binwalk



### b) Tutki tiedostoa h1.jpg binwalk:lla. Mitä tietoja löydät nyt tiedostosta? Mitä työkalua käyttäisit tiedostojen erottamiseen? (Huomaa, että binwalk versio 2.x ja 3.x toimivat eri tavalla.)

### c) FOSS (Free Android OpenSource). Tutustu Android-sovelluksiin Offan (2024) listalta: Android FOSS. Valitse listalla itsellesi mielenkiintoisin applikaatio ja mene sen GitHubiin. Lataa ohjelman APK itsellesi ja käytä seuraavia työkaluja tutustuaksesi, miten APK:n voi avata.
  - ZIP
  - JADX
  - Bytecode-viewer
