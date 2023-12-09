# Moduulin idea

Moduulin tarkoituksena on luoda mielikuvitusystävälleni luomaani git repositorioon pääsy, sekä asentaa VSCodium ja sen vaatimat asetustiedostot. Suunnitellussa moduulissa kaikkea ei voi tehdä täysin automatisoidusti.
Tähän tiedän jo näin alussa olevan ongelmana käyttäjän nimi ja sähköposti git palveluun. Ne täytän käsin.
Tämän lisäksi ystävälleni luodaan pieni määrä komentoja gitin käyttöä varten. Koneelle asennetaan myös UFW palomuuuri ja varmistetaan sen olevan käytössä.

# VSCodiumin asentaminen


![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/41844f0c-b45b-400e-98ed-d40e62f8b9e4)



Aloitan asentamalla VSCodiumin sivuilta löytyvien ohjeiden mukaisesti avaimen ja lähteen kuntoon. Jotta ohjelman voisi asentaa, minulla pitää olla julkinen avain oikeassa sijainnissa ja latauksen lähde luettelossa.
Ensin yritän viedä avaimen kohteeseen.


![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/08de8298-4dd2-47ba-bce8-6e7e73e835f6)

Tämän jälkeen luon yksinkertaisen init.sls tiedoston ja varmistan, että gpg avain siirtyy näin myös orjakoneille.

Siirrän suoraan ladatun gpg avaimen 'dd' komennolla salt moduulin kansioon. Tämä onnistuu pienen vinoviivojen opettelun jälkeen.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/6302cc83-f97b-4a30-84af-af652eb35b3d)


Nyt varmistan siirtyykö tiedosto sisältöineen orjakoneille jos ajan tilan git komennolla 'sudo salt '*' state.apply git'

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/075592b2-f8e8-4519-b7f6-1c7d8b5efea0)


Yrittäessäni ajaa sain vain erroria, lopulta tajusin virheen olevan puuttuvissa kaksoispisteissä tiedosto ID:n jälkeen.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/0c27f98d-d731-48ed-ad17-ac63c2206ee2)

Ajettuani uudestaan sain tiedoston perille.


![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/46904a49-cc8f-4ff6-bcfc-64b8d48dc6f8)

Nyt kun tiedän, että polku toimii vaihdan seuraavaksi oikean sourcen tiedostoon ja katson meneekö se perille.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/8a55173a-0ad6-48d9-86c9-2ea9a2ce221e)


Tiedoston ajo onnistui, katsotaan toimiiko tiedosto.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/a68d3215-e95c-403f-ba46-4e8e906c42f9)

Tiedosto tullut perille.

Seuraavaksi haluan asentaa ohjeen mukaisen listan. Lataan sen ensin herra koneelle.
Ajan sivuilta löytyneen komennon ja katson sen jälkeen saanko asennettua ohjelman herrakoneelle ennen kuin edes yritän sitä muille.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/192a04d8-f50f-4e2f-95ae-ebc988eb719a)


![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/a846d30c-dd1d-4843-bb4f-74bb73e318b4)


VSCodiumin asentaminen onnistui. Lisään nyt lähteen myös moduulin kansioon ja yritän ajaa tiedostot perille. Teen myös oman kansion moduulin osille, ettei kaikki loju samassa kansiossa.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/744cfdd7-2103-4d70-8bfd-21ddfca53007)

Päivitetään lista ja ohjelma init.sls tiedostoon.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/1e026226-eca2-43e0-9905-c1889a3b7bac)


Seuraavaksi yritän ajaa tilan komennolla 'state.apply'

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/143ad523-629c-4b6b-be57-2733bafc15cb)

Vaikuttaa onnistuneen, seuraavaksi koittaa tuomionpäivä ja yritän asentaa pakettia. Yritän tehdä sen ensin vain komennolla 'sudo salt '*' state.single pkg.installed codium'

Ohjelma asentui ja toimii hiukan enemmän resursseja omaavassa virtuaalikoneessani. Vagrantin avulla tehdyt debianit päättivät tässä vaiheessa käytännössä luovuttaa, joten en niitä turhaan pidä jatkossa mukana.
Jos yksi kone toimii se riittää tässä tapauksessa.

Poistan tässä vaiheessa VSCodiumin ja lisään sen tilaan.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/2f85d871-780c-4483-971b-7f4dd0a0e200)

Haluan myös nyt luoda kansion, johon tietoja tallentaa.


Unohduin hiukan testailemaan asioita, mutta alla saamani lisäys init.sls tiedostoon. Lisäsin siihen rivit
/home/koodaus/:
  file.directory
/home/koodaus/tännekaikki.txt:
  file.managed

Näillä riveillä saan kotikansioon luotua uuden kansion ja sinne placeholder tiedoston sisään.

# Git komennot

Saatoin löytää ongelmaan ratkaisun tietojen muuttamisesta lisäämällä ne komentoon ja pyytämällä inputin käyttäjältä. Ei paras tapa, mutta ainakin saan muutettua ne etähallitusti.
Tämä ratkaisu ei siis idempotentti, mutta parempaa en tähän keksinyt, sillä joka askelta ei tässä tietääkseni voi automatisoida.

Loin alla olevan komentorivin

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/ebfcdca7-c7f7-4075-a980-98290a5a6da4)


SSH-avaimen luontia en keksi mitään tapaa automatisoida ja tässä tapauksessa oletetaan ystäväni sen osanneen lähettää, jotta saan sen lisättyä GitHub repositorioni avaimiksi.
Avain on myös sama kuin muita harjoitustehtäviäni tehneellä virtuaalikoneella, joten tässä tapauksessa vain oletetaan sen olevan kunnossa.
Uuden avaimen olisin luonus 'ssh-keygen' komennolla ja kopioinut GitHub hakemistoni "Deploy Keys" osioon.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/87eb528f-585c-47fa-8ac9-b7ee221c8ebe)

Komento kloonata repositorio oikeaan sijaintiin

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/cd0faeb9-861e-4cdc-8ba5-e4caa895c088)

Loin neljä komentoa, joista 'gitin' ohjaa git hakemiston juureen, 'kloonaa' kloonaa git hakemiston oikeaan kansioon, 'gpp' varmistaa, että pull tapahtuu aina ennen pushia ja 'lisaakayttaja' kysyy ja muuttaa gitin käyttäjän asetukset.
Nämä komennot on tuotu omaan kansioon, josta ohjaan ne eteenpäin toisen pään /usr/local/bin/ kansioon.
Lisään sen seuraavaksi init.sls tiedostoon.

Tila ajettu ja tiedostot päässeet perille.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/91340f54-4e35-46bc-9785-34e1cb592deb)

Yritän seuraavaksi ajaa komentoa orjalla.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/5acfd375-e8a1-4a62-9efb-6fecd02cccb2)

Arkkiviholliseni vinoviiva näyttäisi iskeneen jälleen, yritän korjata.


![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/4c05d0ca-519f-44f7-b958-0b44cd11f191)


Sain kaikki korjattua ja yrtitin ajaa niitä moduulin yhteydessä.

Ongelmaksi muodostui, että git ei tykkää kun sen kanssa käytetään sudo käyttäjää. Tästä syystä sain jatkuvaa erroria.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/adb447ce-5433-4668-892d-30af7e7c0cf4)

Lopulta kuitenkin sain ajettua komentoni läpi ja git hakemisto on kopioitu.

Yritän vielä ajaa toista komentoani lisaakayttaja ja katsoa saanko muutettua asetuksia, sillä sekään ei toimuinut saltin kautta.

Tällä kertaa ei ainakaan tullut virhettä.
Huomasin yrittäessäni luoda tiedostoa VSCodiumilla, että tiestoa ei voi luoda. Se johtunee käyttöoikeuksien puutteesta.
Siirrän git kansion sijainnin jos se auttaisi.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/3869b91c-9689-4b8a-9428-35705f613db4)

Asiaa tutkittuani tajusin, että ongelma on käyttöoikeuksien puutteesta johtuva ja annoin kansioon kaikille täydet oikeudet. Kansion ei pitäisi olla tietoturvalle vaarallinen, enkä keksi miten omistajaa saisi vaihdettua muuten. Yritän kloonata uudestaan.

Kloonaus ei vieläkään onnistunut automaationa. Tällä kertaa kuitenkin komento 'kloonaa' toimi suoraan ilman sudoa.
Koetan nyt luoda kansion VSCodiumilla ja viedä sen gittiin.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/43b200d1-f379-4169-b2c2-c71d39b30c0e)


Tiedosto saatu perille.

Haluan vielä yrittää saanko muutettua nimeäni tekemälläni 'lisaakayttaja' komennolla.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/5b61fb59-e1a1-45b3-96e2-bf0fb85f7b82)


Uusi tiedosto tehty.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/f8680f04-5061-494b-b899-d4284cfd31ee)

Uusi tiedosto ja nimi näkyvät muuttuneena.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/e7ba9183-2b97-4049-968e-4849a05f74fc)


# Loppupäätelmät

Halusin kokeilla hiukan erilaisia asioita ja miten ne toimivat Saltilla automatisoituina. Iso osa hallinnasta jäi käsin tehtäväksi ja 'cmd.run' komennon rajoitteet tulivat selkeästi vastaan. Itseäni auttoi kuitenkin paljon Saltin virheilmoitukset.
Nyt lopputilanteessa saavutin mitä halusin. Sain luotua palomuurilla suojatun koneen, missä on git, VSCodium ja UFW asennettuna. Lisäksi tein komentoja, jotka helpottavat ja varmentavat gitin käyttöä. Salt on erittäin voimakas työkalu, mutta esimerkiksi paketinhallinta virallisten lähteiden ulkopuolella on hyvin työlästä.

Lähteet:

T. Karvinen, 2023, Infra as Code 2023, https://terokarvinen.com/2023/configuration-management-2023-autumn/, Luettu 9.12.2023
T. Karvinen, 2021, Run Salt Command Locally, https://terokarvinen.com/2021/salt-run-command-locally/, Luettu 9.12.2023
Salt Project, salt.states.cmd, https://docs.saltproject.io/en/latest/ref/states/all/salt.states.cmd.html, luettu 9.12.2023
VSCodium, Install, https://vscodium.com/#install, luettu 9.12.2023






  
  









