### x) Lue/katso/kuuntele ja tiivistä. (Tässä x-alakohdassa ei tarvitse tehdä testejä tietokoneella, vain lukeminen tai kuunteleminen ja tiivistelmä riittää. Tiivistämiseen riittää muutama ranskalainen viiva.)
Hammond 2022: Ghidra for Reverse Engineering (PicoCTF 2022 #42 'bbbloat') (Video, noin 20 min)

-Videolla käytiin läpi Ghidran toimintaa ja miten se käyttäytyy.
-Avoimen lähdekoodin reverse engineering työkalu
-ltrace ja strace

### a) Asenna Ghidra.

Ensimmäisessä tehtävässä oli tarkoituksena asentaa Ghidra. Tein kyseisiä tehtäviä KaliLinuxilla, joten käytin komentoa:

    sudo apt-get install ghidra

![image](https://github.com/user-attachments/assets/d5abd629-396f-4ba5-871d-f73e6dbfe85e)

Ghidra ladattuna ja aloitus screeni, mistä pääsee luomaan uuden projektin.

    
### b) rever-C. Käänteismallinna packd-binääri C-kielelle Ghidralla. Etsi pääohjelma. Anna muuttujielle kuvaavat nimet. Selitä ohjelman toiminta. Ratkaise tehtävä binääristä, ilman alkuperäistä lähdekoodia. ezbin-challenges.zip

Aloitin lataamalla teron sivustola ezbin-challenges.zipin. Purin kyseisen tiedoston ja siirryin sen sisällä myös purkamaan packd tiedoston komennolla "upx -d packd". Tämä komento poistaa UPX pakkauksen ja palauttaa sen alkuperäiseen muotoonsa.

![image](https://github.com/user-attachments/assets/dff37943-99ac-4bd5-83d2-3f147f610f6c)

Loin uuden projektin Ghidraan ja siirsin packd tiedoston sen sisälle.

![image](https://github.com/user-attachments/assets/008d0c38-4e99-47c3-a9ef-c85463b766a7)

Ghidra analysoi kyseisen tiedoston, Symbol treessä siirryin tutkimaan funktioita ja sieltä valitsin "main" funktion, missä nähdään ohjelman toiminta. Tämän jälkeen päästiin käsiksi Decompile ruutuun, sieltä löytyi kyseisen ohjelman koodi C-kielellä. Tunnilla käytiin kyseistä tehtävää läpi ja minulla oli jonkinverran muistikuvia, miten tämä suoritettaisiin. Seuraavaksi lähdin muuttamaan muuttujien nimiä, että ne olisi selkokielisiä koodissa. Vaihdoin undefined8 <-> int main pääfunktion. Seuraavaksi muutettiin käyttäjänsyöte local_28 <-> input, mikä kuulostaa paljon loogisemmalta koska siihen syötetään tieto. Viimeinen muuttuja minkä vaihdoin oli Var1 <-> difference, muuttuja vertailee kahta eri merkkijonoa keskenään ja palauttaa kokonaislukuna eroavaisuudet.

![image](https://github.com/user-attachments/assets/14300d5e-08c5-4477-96c6-15e503112cd9)

![image](https://github.com/user-attachments/assets/14761850-2deb-4375-82e0-bf0f985f2715)

Tallensin kyseiset muutokset nimellä packd_testi ja muutin formaatin Orginal fileksi. Avasin terminaalin ja annoin execute oikeudet kyseisellä tiedostolle "chmod +x packd_testi". Suoritin ajon "./packd_testi".

![image](https://github.com/user-attachments/assets/c6d512f1-8b77-451f-b06f-124041ee0332)


### c) Jos väärinpäin. Muokkaa passtr-ohjelman binääriä (ilman alkuperäistä lähdekoodia) niin, että se hyväksyy kaikki salasanat paitsi oikean. Osoita testein, että ohjelma toimii. ezbin-challenges.zip

Aloitin suorittamaan tehtävää luomalla uuden projektin ja lisäämällä sinne passtr tiedoston. Samalla tyylillä kuin edellisessä tehtävässä lähdin navigoimaan Symbol treetä ja siirryin Functions ja main sivulle nähdäkseni ohjelman koodin. Tarkoituksena tässä tehtävässä olisi muokata ohjelman binääriä niin, että ohjelma muuttaisi if lauseen väärinpäin. Tunnilla tätä käytiinkin läpi, joten se oli aika hyvin muistissa. Klikkasin if lausetta ja listings kohtaan tuli highlighti, mitä halusin alkaa muuttamaan, jotta saadaan kaikki muut salasanat paitsi oikea hyväksytyksi. Kohdassa oli JNZ komento, mikä tarkoittaa jump not zero. Tehtävän ratkaisemiseksi halutaan muuttaa kyseinen komento JZ eli jump zero. Tämä toimenpide onnistuu kun siirtyy kyseisen komennon kohdalla Path instructions osioon. Muutosten jälkeen lähdin exporttaamaan ja testaamaan toimiiko tämä muutos. Annettiin taas execute oikeudet exportatulle tiedostolle ja tämän jälkeen ajettiin kyseisen tiedosto. Kokeiltiin vääriä salasanoja, milloin saatiin flagi esiin ja oikealla salasanalla ei saatu salasanaa.

![image](https://github.com/user-attachments/assets/342dbcc0-b424-4914-821d-851316ec2093)

### d) Nora CrackMe: Käännä binääreiksi Tindall 2023: NoraCodes / crackmes. Lue README.md: älä katso lähdekoodeja, ellet tarvitse niitä apupyöriksi. Näissä tehtävissä binäärejä käänteismallinnetaan. Binäärejä ei muokata, koska muutenhan jokaisen tehtävän ratkaisu olisi vaihtaa palautusarvoksi "return 0".

Siirryin https://github.com/NoraCodes/crackmes mikä oli tarkoitus kloonata omalle virtuaalikoneelleni. Aluksi ei onnistunut, mutta tajusin, että minun tarvitsee ladata git ensin. Tämän jälkeen kloonaus onnistui.

        sudo apt install git
        git clone https://github.com/NoraCodes/crackmes

![image](https://github.com/user-attachments/assets/b55465cc-2235-48e3-a325-db0801912df6)

Luin README.md tiedoston ja sieltä löytyi ohjeita seuraavia tehtäviä varten. 

![image](https://github.com/user-attachments/assets/98d997d1-10fb-4451-b8ea-8584470dc335)

### e) Nora crackme01. Ratkaise binääri.

Ensi töiksi suoritin komennon make crackme01. Seuraavaksi lähdin kokeilemaan eri komentoja, jotta saisin vähän tietoa kyseisestä tiedostosta. 

        file crackme01.64
        strings crackme01.64

![image](https://github.com/user-attachments/assets/7854d5e1-6c4b-452e-94d9-e6ea3e6c9152)

file komennolla saatiin tietoa kyseisestä tiedostosta, se on 64 bittinen linux ohjelma ja dynaamisesti linkitetty.

![image](https://github.com/user-attachments/assets/81868dd1-a53c-4554-b7c4-5aa5ee1214b1)

strings komento etsii ja  tulostaa merkkijonoja tiedostosta, ja näistä pystyi jo aika pitkälle päättelemään asioita. Silmääni osui "password1", mikä vaikutti aika potentiaaliselta salasanavaihtoehdolta.

![image](https://github.com/user-attachments/assets/edcd20b6-0a24-4773-b982-130a9a767f0e)

Kokeilin kyseistä "password1" vaihtoehtoa ja saatiin onnistuneesti oikea vastaus.


### e) Nora crackme01e. Ratkaise binääri.

Tehtävä vaikutti saman tyyliseltä kuin aiempi joten lähdin suorittamaan tätä tehtävää samalla tyylillä kun edellistä, eli make crackme01e. Sen jälkeen taas strings komentoa sisään ja tutkailemaan tekstiä. 

![image](https://github.com/user-attachments/assets/8338a12a-1bcb-4693-9506-d50582346dfd)

Tekstin seasta erottui kohta "slm!paas.k", mikä erosi muista ja vaikutti siltä että se voisi olla mahdollinen salasana. Lähdin testaamaan menisikö tällä tehtävä läpi. 

![image](https://github.com/user-attachments/assets/fce7ed62-165f-423f-a15c-15c4d810649f)

En saanut oikeaa vastausta kyseisellä salasanalla, halusin tietää mitä komento antaisi eri tekstillä, joten testailin vähän eri vaihtoehtoja.

![image](https://github.com/user-attachments/assets/3d543c9d-bdac-4083-9817-b5f91ad05e73)

Tässä tulokseksi saatiin suoraan väärä vastaus, joten ensimmäisen salasanan tuloste jäi mietityttämään. Kysyin apua tekoälyltä, ja siitä sain selville, että huutomerkkiä ei pystytty lukemaan ja sain vinkiksi kokeilla käyttää hipsukoita apuna.

![image](https://github.com/user-attachments/assets/2a8b47d8-7890-4d08-84f7-6877341717d4)

Hipsukat toimi ja saatiin oikea tuloste.


### f) Nora crackme02. Nimeä pääohjelman muuttujat käänteismallinnetusta binääristä ja selitä ohjelman toiminta. Ratkaise binääri.

En kerennyt enään suorittamaan tätä tehtävää, joten palaan tähän myöhemmin.

Minulla oli aika paljon ongelmia virtuaalikoneiden kanssa, Kalilla tehdessäni interfacet alkoi reistailemaan ja kokeilin aika paljon erilaisia ratkaisuvaihtoehtoja, mutta en löytänyt tyydyttävää ratkaisua ongelmaan. Siirryin seuraavaksi käyttämään Debian 12:sta, että pääsisin etenemään tehtävissä, mutta kyseinen virtuaalikone laittoi myös aika paljon vastaan. Debian 12 oli muistiongelmia, käytännössä muisti täynnä vaikka ihan tuoreena ladattu ja asetukset olivat kunnossa. Aika hyvän tovin latailin sekä asentelin uudelleen virtuaalikoneita, että saisin ne toimimaan normaalisti. Aikaisemmilla kursseilla ei ole ollut näiden kanssa hirveästi mitään ongelmia, niin en oikein tiedä mitä nyt on mennyt pieleen tai muuttunut. Sain virtuaalikoneeni lopulta toimimaan taas normaalisti, jotta sain tehtävät suoritettua. Aikaa kokonaisuudessaan meni 21.00-3.00, mistä varmaan 4 tuntia virtuaalikoneiden kanssa taisteluun.


### Lähteet

https://terokarvinen.com/application-hacking/#laksyt

Hammond 2022: Ghidra for Reverse Engineering (PicoCTF 2022 #42 'bbbloat')

https://github.com/NoraCodes/crackmes

https://chatgpt.com


