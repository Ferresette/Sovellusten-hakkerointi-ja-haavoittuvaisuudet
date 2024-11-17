### x) Lue/katso/kuuntele ja tiivistä. (Tässä x-alakohdassa ei tarvitse tehdä testejä tietokoneella, vain lukeminen tai kuunteleminen ja tiivistelmä riittää. Tiivistämiseen riittää muutama ranskalainen viiva.)
Hammond 2022: Ghidra for Reverse Engineering (PicoCTF 2022 #42 'bbbloat') (Video, noin 20 min)

-Videolla käytiin läpi Ghidran toimintaa ja miten se käyttäytyy.
-Avoimen lähdekoodin reverse engineering työkalu

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

Ghidra analysoi kyseisen tiedoston, Symbol treessä siirryin tutkimaan funktioita ja sieltä valitstin "main" funktion, missä nähdään ohjelman toiminta. Tämän jälkeen päästiin käsiksi Decompile ruutuun. Tunnilla käytiin kyseistä tehtävää läpi ja minulla oli jonkinverran muistikuvia, miten tämä suoritettaisiin. Lähdin muuttamaan muuttujien nimiä, että ne olisi selkokielisiä.





### c) Jos väärinpäin. Muokkaa passtr-ohjelman binääriä (ilman alkuperäistä lähdekoodia) niin, että se hyväksyy kaikki salasanat paitsi oikean. Osoita testein, että ohjelma toimii. ezbin-challenges.zip
### d) Nora CrackMe: Käännä binääreiksi Tindall 2023: NoraCodes / crackmes. Lue README.md: älä katso lähdekoodeja, ellet tarvitse niitä apupyöriksi. Näissä tehtävissä binäärejä käänteismallinnetaan. Binäärejä ei muokata, koska muutenhan jokaisen tehtävän ratkaisu olisi vaihtaa palautusarvoksi "return 0".
### e) Nora crackme01. Ratkaise binääri.
### e) Nora crackme01e. Ratkaise binääri.
### f) Nora crackme02. Nimeä pääohjelman muuttujat käänteismallinnetusta binääristä ja selitä ohjelman toiminta. Ratkaise binääri.
