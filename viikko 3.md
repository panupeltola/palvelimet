# Host ympäristö:
* Windows 10
* Intel Core i7-10770K
* Nvidia GeForce 3080
* 32 GB RAM
* Virtualbox 7.0.12
* Debian 11 virtuaalikone

# a) Online

Aloitan tehtävän luomalla uuden GitHub repositorion tilini "Your repositories" ikkkunasta

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/ae9a69da-c6c7-4059-ac39-eff5ef2b62d0)

Varmistan, että nimi kelpaa ja luon lyhyen kuvauksen repositorion luonteesta.
Lisäksi varmistan, että hakemistoon luodaan readme tiedosto ja lisenssityyppi on oikea.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/9b244bef-80fa-4877-bd8a-3d17e5e080f2)


Repositorio luotu.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/37ee84d8-3eb7-4f46-8d38-760df129cab0)


# b) Dolly

Varmistan ensin, että virtuaalikoneelleni on asennettu git. Kuvaa ennen on ajettu komento 'sudo apt-get update' 

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/6fca1b14-7935-42f9-a5af-26fc0fe50080)


Ei päivitettävää eikä asennettavaa, joten uusin Git on asennettuna.

Aloitan yrittämällä luoda yhteyttä ssh linkillä GitHubin sivuilta.
GitHub kuitenkin ilmoittaa jo tässä vaiheessa, että SSH-salausavainta ei ole, joten nähdäkseni on turha mennä pidemmälle ennen kuin tämä ongelma on ratkaistu.

Luon SSH-avainparin komennolla 'ssh-keygen'

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/3462d4e5-3c75-4a61-84cd-8a183dfd5ae0)


Avaimet luotu.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/54f85f46-6449-4c7d-b4ef-295eefb8ba80)


Lisään avaimen GitHubin käyttäjän asetuksista kohdasta "SSH and GPG keys"
Lisään julkisen avaimeni tähän kohtaan.
Avain näkyy listassa.
![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/a011d211-8729-46ef-b9c0-11d4894ae012)

Yritän kopioida SSH-linkkiä uudelleen ja varoitus on poistunut.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/2f13b22d-29f9-42d8-9286-d97e453e777e)

Kopioin SSH-linkin ja kloonaan repositorion komennolla 'git clone git@github.com:panupeltola/gitgudwinter.git'.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/e69926e1-b7fa-41b9-9d29-5cb488e22f1d)

Pienen tuskailun jälkeen ymmärsin, että minun pitää olla luodussa hakemistossa, jotta voin käyttää gitin komentoja.
Siirryin oikeaan hakemistoon ja ajoin komennon 'git pull'.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/5e2f58fe-96e6-4bc2-a263-e7e9b2a6ba75)

Kansion sisältö komennolla 'ls' vastasi verkkoselaimen sisältöä.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/98fbd8da-e626-42b4-a919-b3fb600eac8d)

Luon testitiedoston test.py ja lisään sen sisään tekstin "jouluun on käytännössä kuukausi".


![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/02e48c28-9068-4ba6-b104-29c04b7b4b3b)

Tiedoston luonti

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/6b41c4f9-bcd1-4a3b-af1f-ce7b386e14f3)

Muokkaaminen microlla.

Nyt komennolla 'git status' näen tekemieni muutosten tilan. Näen, ettei test.py tiedostoa ole vielä tallennettu muutokseksi.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/a8344289-5af5-4590-a8da-c5cb1d44ca55)

Teen sen seuraavaksi komennoilla 'git add .' ja 'git commit'
![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/64f4aeca-3cd3-4133-9cd4-8201e702b31d)

Ajettuani komennon, tuli virhe, ettei käyttäjälleni ole vielä määritetty sähköpostia tai nimeä. Näille annettiin komennot virheviestissä. Lisään nämä ja yritän ajaa komentoa uudestaan.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/eca000c7-b9db-47bf-8c8c-4687206416d4)
Ajettuani komennot terminaalini meni tilaan, mistä en päässyt takaisin ajamaan komentoja.
Asiaa tutkittuani totesin, että olin unohtanut lainausmerkit komennon 'git config --global user.email "bha531@myy.haaga-helia.fi' lopusta. Lisättyäni ne sain muutettua sähköpostin ja tein saman nimelle seuraavaksi

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/474f1147-5b5e-4a7d-870e-a8e85f352b5e)



Yritin seuraavaksi komentoa 'git commit' uudelleen.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/bfd3236c-6f94-4230-b0e7-0144b6dd2ceb)

Sain komennon toimimaan ja pääsin nano ikkunaan, mihin listaan seuraavaksi käskynä, preesenssissä ja englanniksi Teron viime luennon ohjeen mukaisesti.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/9633ff31-2e36-4624-9cda-75f1680c5268)

Lisätty teksi.


Terminaali antoi seuraavan vastauksen tallennettuani ja poistuttuani ikkunasta.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/302bb0d9-1f27-4b74-a831-753253513775)


Tarkastan seuraavaksi näkyykö tiedosto verkkoselaimessa.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/ad722df0-9035-47a5-ab72-0b6c13ec1847)

Tiedostoa ei näy, mutta tajusin etten ole vielä käyttänyt 'git push' komentoa ajaakseni niitä verkkoon.
Ajan kuitenkin 'git pull' komennon ennen hyvän työmallin vuoksi.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/0250504b-6010-47a8-af83-00ad1983ed67)

Uusi tiedosto näkyy nyt myös repositoriossa. Huomiona tähän, kuva on otettu välittömästi 'git push' komennon jälkeen, mutta commit ajoituksessa näkyy 8 minuuttia sitten. Tästä päättelin, että commit aika määräytyy 'git commit' komennon ajasta eikä 'git push' ajasta

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/d9dd2486-f64f-4a64-b40a-5029371a68fe)

Tarkastan vielä, että myös sisältö on tullut mukana.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/974919ea-d201-4cb2-8434-eca810b21fe7)

Oikealta näyttää.

# c) Doh!
Jatkan siitä mihin jäin. Haluan seuraavassa harjoituksessa koettaa miten komento 'git reset --hard' toimii.
Luon kaksi tiedostoa ja ajan komennon 'git reset --hard'

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/26bd9513-42ec-4435-a766-2e3b2376c9ba)

Komentoa 'git add .' ei ole ajettu, eikä 'git reset --hard' vaikuta tekevän tässä vaiheessa mitään. Tiedostot näkyvät yhä 'git status' komennolla.
Ajan komennon 'git add .'
Katson tiedostojen tilan 'git status komennolla' Tämän jälkeen koitan ajaa komennon 'git reset --hard'

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/26b10bd9-2748-4a65-b8e9-8cbe55398e71)

'git reset --hard' poisti työn aikaiset tiedostot ja palautti tilanteeksi edellisen 'git commit' komennon jälkeisen tilanteen.
Ennen lopullista päätelmääni haluan vielä koettaa miten käy jos vain osa tiedostoista on ollut muutettuna ennen 'git add .' komentoa

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/67afe71f-d736-402e-9e7b-49aaa3fd2d99)

Ajan vielä komennot git reset --hard ja git status

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/ea998520-c8ec-4cb9-a219-e47d1edf7ea9)

Vain tiedosto test.txt on poistunut ja "eitallenna" pysyi osiossa "Untracked files". Tästä voi päätellä komennon käyttäytymisestä, että 'git reset --hard' poistaa edellisen 'git commit' jälkeen tehdyt muutokset, joiden jälkeen on ajettu komento 'git add .'


# d) Tukki
Ajoin komennon git log --patch

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/70139ec5-cc0e-42a8-b147-e9f258a9d525)

Tästä logista ei sinänsä voi vielä päätellä kauheasti, mutta oletettavasti "+" tarkoittaa lisättyä.
Kokeilen luoda kolme tiedostoa, lisätä yhteen, poistaa yhdestä ja pitää yhden sellaisenaan nähdäkseni miten ne kirjautuvat lokiin.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/dbbd6eb2-23d8-4e69-9de4-3d0f9722149c)

Tiedostojen luonti (myös aiemmin roikkumaan jäänyt "eitallenna" päätyi nyt joukkoon)

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/02dd1c47-fdb9-4de2-98c2-76823868cf4d)

Ajetaan muutokset.

Tiedostoon Grute lisään tekstiä:

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/003ec975-7491-4e60-9dae-3cec16cb1660)

alkuperäinen

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/565aa545-b81f-43f0-ada7-c096ad086003)

Lisätty

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/1e9ca0d1-b7d8-4b7b-bf21-f354ebf92153)

Alkuperäinen (Poistin vahingossa tekstiä ennen kuvan ottamista ja palautin ennalleen, siksi näkyy muokattuna.)

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/72303929-c834-47f0-b12e-5fc7cd9a7dc5)

Poistettu

Poistin myös tiedoston "eitallenna"

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/c844fcf4-afa9-47ab-9118-283a78fbab40)

Seuraavaksi ajan komennon 'git add .' ja 'git commit' nähdäkseni miten tämä näkyy lokeissa.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/ba9bcb83-953a-4924-9a61-460720d0c26e)

Viedään muutokset läpi.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/9b0fca84-2dc1-44a4-bcc6-56139533ab2d)

Lokista katsottuna tiedosto "Grute" on päivittänyt lisätyn rivin tiedot. Tiedosto "Poro" käsittelee muuttunutta riviä näyttämällä edellisen rivin punaisella ja miinusetumerkillä poistuneena ja sen korvanneen tekstin vihreänä plus etumerkillä 
Tästä päättelen, että gitin loki merkkaa muutokset aina täysin poistuneina ja uudelleen tehtyinä, eikä yritä näyttää muutosta muulla tavalla.


# e) Yhteistyötä

Yritän lisätä käyttäjää käyttäen deploy keys menetelmää. (GitHub Docs)

Alustan toisen virtuaalikoneen ja luon sille uuden ssh avaimen.

Latasin toiselle virtuaalikoneelle gitin ja loin ssh avaimen komennolla 'ssh-keygen' ja kopioin julkisen avaimen projektin deploy keys osioon. Yritän seuraavaksi kloonata repositorion.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/742abb3d-c15f-4dd8-949e-1cb5303480af)

Repositorio kloonattu, muutan vielä sähköpostin ja käyttäjänimen, jotten saa virhettä yrittäessäni ajaa 'git commit' komentoa, kuten aiemmin kävi.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/fcf476cd-9f29-417c-84fb-a40b966eca4b)

Yritän tehdä muutoksia ja ajaa ne läpi.

Katosessani tiedostojani repositoriossa huomaan, että viimeisen commitin muutokset eivät ole muuttuneet. Aloin epäilemään muistinko ajaa komentoa 'git push' session lopuksi.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/4a702bd4-f0a7-4738-b891-14e400a06b54)

Komento oli unohtunut ajaa ja nyt muutokset näkyvät muille myös ajettuani 'git pull' komennon.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/740fd91e-1ba2-42d8-89b1-3068abddd31a)

Koitan tehdä muutoksia uudella käyttäjällä.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/39f5d32c-9cbb-408e-ab90-8ab8b2954992)

Unohdin ottaa kuvan tekemistäni muutoksista, mutta sen pitäisi näkyä kun tarkastan asian toisella virtuaalikoneellani.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/8f1516bc-13c7-4320-8f1b-95ee38bd7ae8)

Muutos ja käyttäjä näkyvät oikein. Totean toisen käyttäjän lisäämisen onnistuneen.













































