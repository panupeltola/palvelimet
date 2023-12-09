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

  
  









