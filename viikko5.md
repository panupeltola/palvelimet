# x)

T. Karvinen, 2018 Apache User Homepages Automatically – Salt Package-File-Service Example

* Ohjeessa näytettiin miten Saltilla voidaan keskitetysti hallita orjakoneiden apache palvelimia käyttäen komentoja idempotetnttitiloja pakettien, palvelujen ja tiedostojen ostalta.
*  Hyväksi tavaksi 'cmd.run' komennon välttäminen ja saman asian tekeminen idempotetnttitiloilla
*  Ohjeen alussa käytiin myös find komennon hyödyntämistä muuttuneiden tiedostojen löytämisen kannalta.


Host ympäristö:

    Windows 10
    Intel Core i7-10770K
    Nvidia GeForce 3080
    32 GB RAM
    Virtualbox 7.0.12
    Debian 11 virtuaalikone


# a) CSI Kerava

Käytän ohjeessa Karvisen viime tunnilla näyttämää komentoa 'find /etc/ -printf '%T+ %p\n' | sort'

Tässä komennossa on seruaavat osat:
* find = kutsuu komennon find
* /etc/ kertoo komennolle tiedoksi hakea kansion /etc/
* printf= print format, formatoi tulosteen 
* %T+ = palauttaa ajan, jolloin tiedostoa on viimeksi muokattu, tässä tapauksessa ajan formatoinnille '+' joka palauttaa ajan muodossa vvvv-kk-pp+tt-mm-ss, eli esimerkiksi tämän hetken aika palautuisi muodossa 2023-11-26+09-24-56. Lisäksi perään tulee vielä millisekunnit
* %p palauttaa tiedoston nimen
* \n luo tulosteeseen uuden rivin
* '|' lähettää edellisen ohjelman tulosteen yms ulostuotetun datan seuraavalle komennolle syötteeksi
* sort järjestää rivit parhaan ymmärrykseni mukaan ensimmäisen riveillä tulevan yhtenevän muutoksen avulla (tässä tapauksessa päivämäärä) sillä mitään parametrejä järjestämiselle ei ole annettu.


Ajoin komennon 'find /etc/ -printf '%T+ %p\n' | sort'

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/e1ab449c-050c-4a0b-a2d0-4765544ade29)

ensimmäiset rivit

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/28b6e380-af07-4b45-bf3b-a54bda46b51b)

viimeiset rivit

Näin sain ajettua /etc/ kansion sisällön järjestettynä muokkaamispäivän mukaan.

# b) Gui2fs

Päätin muuttaa teemaani Firefox selaimessa.
![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/43b70bbd-49a4-4c2f-b908-1261855cae46)

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/e5b8fc84-93ce-4ef2-9140-07012e16fd1c)

Teema vaihdettu tummaksi polusta "asetukset > yleiset > Kieli ja ulkoasu

Nyt etsin muutosta äsken käytetyllä komennolla.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/887f7058-72f8-476a-b264-58b0e1b0737c)

Ei muuttuneita tiedostoja oikeassa aikaikkunassa (Kello todellisuudessa 9:43)
Yritän muuttaa jotain toisen ohjelman asetusta ja katsoa vaikuttaako se tiedostoihin.
Muutin Libre Writerin tietoja

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/ac2c20dd-8079-45eb-9cf4-cf5aec3d5eb7)

Ajan komennon uudelleen.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/7186352a-760f-4e6b-bf9f-5e572ee87fc2)


Mikään ei ole muuttunut oikeassa aikaikkunassa.


Yritän vielä muuttaa suoraan Debianin asetuksia muokkaamalla asetusta "Tyhjän näytön viive" 5 minuutista 15 minuuttiin

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/af54c99d-7dbd-4514-b540-cf66b049c09b)

Mikään ei muuttunut vaikka säädin useita asetuksia ja käynnistin koneen uudelleen.
Lopulta yritin muuttaa komentoriviltä apache2 asetusta kotikansion asentamisesta ja sen muutokset tulivat näkyviin.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/bbd3757e-17eb-4435-b840-dc034ccb9c45)

Lopputulemana on, etten tiedä mihin graaffisessa käyttöliittymässä tehdyt muutokset menevät.


# c) Komennus

Vaihdan  loppuja tehtäviä varten Karvisen ohjeella tehtyihin Vagrant koneisiin.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/e7344662-2f8b-4bff-b195-6669a5fe97e1)

Koneet luotu ja yhteystoimii, joten aloitan tekemällä yksinkertaisen ohjelman:

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/77a60116-d0e8-48c5-a036-32ece8c287fb)

Unohdin ottaa seuraavista välivaiheista erillisiä kuvia, mutta selostuksena ajatuksen juoksuni:

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/63ced43f-c84d-42be-a231-4f1d0bc31670)

* Komento ei toiminut, epäilin tehneeni jotain väärin ja vaihdoin varalta bash komentoihin.
* Lisäsin tiedostoon '.sh' päätteen komennolla 'mv heimaailma heimaailma.sh'
* Ei toiminut
* Muistin, etten ole käyttänyt 'chmod' komentoa vielä tiedostoon
* Yritin lisätä käyttöoikeudet komennolla 'chmod -755 heimaailma.sh'
* Tämä ei toiminut, muttei myöskään antanut virheilmoitusta, eli jotain se teki. Katson myöhemmin mitä -755 todellisuudessa teki vai tekikö mitään.
* Lisäsin oikeudet lukemiseen ja ajamiseen komennolla 'chmod +rx heimaailma.sh'
* Varmistin oikeat oikeudet komennolla 'ls -l'
* ajoin komennon ja sain haluamani vastauksen.
* Nähdäkseni ohjelma siis toimii.

Seuraavaksi luon salt kansion ja vien sinne 'heimaailma.sh' tiedoston komennolla 'sudo cp heimaailma.sh /srv/salt/heippa'

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/e9437888-d085-436a-9097-2f317bb055a3)

Luon moduliin init.sls kansion testatakseni saltin toiminnan. 

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/ff2d1ba6-4f7e-4fce-b9fb-0c4a2b355942)

Luotu tiedosto

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/20d98053-043f-4008-a001-4f9e91b2947b)

Orjakoneiden vastaukset.

Tarkastan vielä tiedostojen olemassa olon saltin kautta ls komennolla.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/d8944da4-24ca-4316-a8ca-aa2f4110e6c3)


Vielä ennen kuin ajan komentoa Salt moduliin haluan varmistaa sen toiminnan herra koneessa siirtäämällä se /usr/bin/ kansioon

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/902e9883-da44-4043-b179-5d26c77431bf)

Ohjelma toimii.

Seuraavaksi vien scriptin osaksi modulia.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/9cb97527-6104-437a-b2ed-fdd02caa4ed4)

Mode: "0755" tulisi antaa tiedostolle oikeudet -rwxr-xr-x 


Yritän ajaa komennon 'sudo salt '*' state.apply heippa'

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/2c41ad42-e6b3-4740-8f59-11a99825bafc)

Näyttää oikealta.
Yritän vielä ajaa komennot orjalla.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/6da7f332-a67c-4ba3-b2c4-24a9b1367829)

Komento toimii.

Haluan vielä varmistaa että käyttöoikeudet ovat oikein.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/299e9f1f-b20d-4897-a378-3ff6876fa3ef)

Käyttöoikeudet ovat oikein, eli mode 755 teki tässä tapauksessa tehtävänsä.


# d) Ämpärillinen

Aloitan luomalla kolme yksinkertaista komentoa vastaavalla tavalla kuin aiemmin.


![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/8b51ac26-ed54-4412-99f5-c9a5b16482c6)

yksi (shebang muokattu oikeaksi myöhemmin)

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/6af6c96a-887b-4b30-88dd-37c0fd75414b)

kaksi

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/9c872a9b-0e52-4127-b4e8-8e1d1b7d7018)

kolme

Lisätään käyttäjäoikeudet:

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/6ea0fa91-af9c-4956-9135-51758706e5e3)


Yritän ajaa ohjelmat:

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/b6e4a0e1-69e5-4966-b2d0-42a5013d8a05)

Bash on määritetty väärin, tutkin mistä tämä johtuu

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/227396ff-27f1-43ad-a945-940e2135918a)

Esimerkki ohjelmasta kolme, vinoviiva puuttui

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/65f9af39-8429-466c-b869-4bc7adee9461)


Ohjelmat toimivat.

Selvitän seuraavaksi miten kokonaisen kansion sisällön saa siirrettyä saltin kautta.
Luin Statedocista sekä verkosta komennosta  'file.recurse' jonka pitäisi siirtää kansio sisältöineen uuteen kohteeseen. Haluan katsoa miten tämä toimii.

Tiedostot viety salt kansioon "Bucket"

Luon init.sls tiedoston.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/0282af94-7968-4736-8f16-b9c3b70273bb)

Sain ajaessa seuraavan virheen:

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/7e24bf27-15f5-47e2-955f-0b44d2489695)


![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/39017e14-2990-422d-b722-fd1a2184448b)

Ajoin tiedoston ja sain kopioitua tiedostot. Huomasin tässä pari asiaa. Ensimmäinen oli, että uutta kansiota ei luotu enää asetetun polun perään, kuten hiukan pelkäsin. Tämä tarkoittaa, että komento file.recurse toimii tässä tapauksessa.
Toisena ongelmana tajusin, että myös init.sls kopioituu mukana mikä ei ole tässä tapauksessa haluttavaa, tästä syystä lisään siirrettävät tiedostot uuteen kansioon ja muokkaan init.sls sen mukaisesti.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/237a3ae9-1d69-4f4f-b9ca-7e878012c5d7)


Korjattu init.sls

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/86732a16-adf2-4744-a8f5-299681ee9325)


Yritän nyt ajaa tilan komennolla 'sudo salt '*' state.apply bucket:

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/b1028fff-5fd0-4119-864e-c64b79033b7e)

1/2


![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/3b4c74c6-229c-4966-99bd-fc756c446341)

2/2

Käyttöoikeudet ja tiedostot vaikuttavat oikeilta, yritän vielä ajaa komennot komennolla sudo salt '*' cmd.run 'yksi && kaksi && kolme'.


![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/4805d99c-7a16-48a7-93a6-c2de157bf74a)

Ja niin on lisätty kansiollinen komentoja.


Lähteet:
* T. Karvinen, 2023, Salt Vagrant - automatically provision one master and two slaves, https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file, luettu 26.11.2023
* T. Karvinen, 2023, Infra as Code 2023, https://terokarvinen.com/2023/configuration-management-2023-autumn/, Luettu 26.11.2023
* T. Karvinen, 2018, Apache User Homepages Automatically – Salt Package-File-Service Example, https://terokarvinen.com/2018/04/03/apache-user-homepages-automatically-salt-package-file-service-example/, luettu 26.11.2023
* Salt Project, file.recurse, https://docs.saltproject.io/en/latest/ref/states/all/salt.states.file.html#salt.states.file.recurse, luettu 26.11.2023
* 'man find', Free Software Foundation Inc, 2021
* 'man sort', M. Haertel & P. Eggert, 2020
