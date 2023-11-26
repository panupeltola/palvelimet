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
















Lähteet:

'man find', Free Software Foundation Inc, 2021
'man sort', M. Haertel & P. Eggert, 2020
