### a) Lab1. Tutkiminen mikä on ohjelmassa vialla ja miten se korjataan. lab1.zip

Aloitin tehtävän lataamalla lab01.zip tiedoston sivustolta https://terokarvinen.com/application-hacking/#laksyt. Siirryin downloads hakemistoon ja purin kyseisen zip tiedoston "unzip lab01.zip".

Ajoin kyseisen gdb_example1 ohjelman, jotta näkisin mitä se antaa tulokseksi. 

![image](https://github.com/user-attachments/assets/c9f5f87d-9394-4088-95b6-7153038d29b8)

Sain käsityksen, että Segementation fault ei ollut toivottu lopputulos kyseisessä tulosteessa. Googlettelin ja kyselin ChatGPT:ltä apuja kyseisen ongelman kanssa. Äkkiä ilmeni, että yllätys yllätys se tarkoittaa virhettä koodissa. Ja tämä pitäisi nyt ratkaista.

Avasin ensi töikseni ohjelman GNU Debuggerilla komennolla *gdb ./gdb_example1* ja tämän jälkeen hyödynsin tunnilla opetettua *layout split* komentoa nähdäkseni enemmän tietoa tiedostosta.

Ensiksi lähdin liikkeelle *run* komennolla, mikä ajaa tiedoston gdbllä. Alla olevassa kuvassa näkyy sama Segmentation fault ja missä kohti koodia se sijaitsee.

![image](https://github.com/user-attachments/assets/ff3c6286-d092-4274-81fe-02d3b492f816)

Onglema tuntuu olevan muuttuja **message** pointerissa. Mutta se ei osoita mihinkään kelvolliseen muistiosoitteeseen, siksi koska se on NULL (0x0) jokainen yritys johtaa segmentation faultiin. 
Asetin breakpointin *break print_scrambled*, jotta näen tarkemmin tietoa siitä. Siirryin *next* komennolla eteenpäin mihin kyseinen message osoittaa.  

Lähdin muokkaamaan koodia nanolla. Alkuperäinen koodi:

![image](https://github.com/user-attachments/assets/a39d0282-329b-4e84-8165-a1412ed471b8)

Muokattu koodi:

![image](https://github.com/user-attachments/assets/232fdc29-e555-4976-b083-4da93a7c4608)

Koodin muokkaamisen jälkeen käytin komentoa *gcc -o gdb_example1 gdb_example1.c*, mikä kääntää ohjelman uudestaan. Ja suoritin vielä ajon muokatulla ohjelmalla.

![image](https://github.com/user-attachments/assets/6955e717-4a99-47ce-956d-84641f8dc887)

Muokkaamisen jälkeen Segementation fault on saatu poistettua lisäämällä koodiin kohta, missä se tarkastaa onko message NULL. 


### b) Lab2. Selvitä salasana ja lippu + kirjoita raportti siitä miten aukesi. lab2.zip

Lab2 alkoi samanlailla kun Lab1 eli purettiin paketit ensimmäiseksi. Tutkailtiin lab2 sisältöä ja sieltä löytyi passtr hakemisto. Luin seuraavaksi README.md kansion, jotta sain vähän lisätietoja tehtävää varten. Tarkoituksena siis löytää flagi passtr2o tiedostosta debuggeria käyttämällä. Kyseisessä tiedostossa ei ollut lähdekoodia, joten lähdin tutkailemaan assemblerilla ja kokeilemaan eri komentoja. Käytin *break main* ja *run* komentoa nähdäkseni mitä assemblerissa tapahtuu. Löysin ihan mielenkiintoisen kohdan, mistä ajattelisin olevan hyötyä tehtävän ratkaisussa.

![image](https://github.com/user-attachments/assets/d3c42ff0-03e5-457c-b4f5-fec3e29eff43)

Kokeilin paljon erilaisia komentoja ja koitin ymmärtää debuggerin toimintatapoja useamman tunnin, mutta tuntui etten oikein edennyt mihinkään suuntaan tehtävän kanssa. Tämän viikon tehtävät osottautui itselleni ainakin liian haastaviksi suorittaa. Lähdekoodista kykenin vielä suoriutumaan ihan hyvin, mutta ilman lähdekoodia olin aivan mankelissa.

Koen vielä, että oikeasti yritin suorittaa tehtävät kunnialla loppuun hakemalla tietoja eri lähteistä ja yrittämällä perehtyä asiaan, enkä heittää hanskoja samantien tiskiin.


### c) Lab3. Kokeile Nora Crackmes harjoituksia tehtävä 3 ja 4 ja loput vapaaehtoisia. Tindall 2023: NoraCodes / crackmes.


### Lähteet

https://terokarvinen.com/application-hacking/#laksyt

https://www-users.cse.umn.edu/~kauffman/tutorials/gdb

https://www.geeksforgeeks.org/gdb-step-by-step-introduction/

https://stackoverflow.com/questions/26462227/debugging-with-gdb-without-sources

https://chatgpt.com/






