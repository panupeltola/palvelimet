# Ympäristö
* Windows 10
* Intel Core i7-10770K
* Nvidia GeForce 3080
* 32 GB RAM

  # a) Asenna Vagrant
  Koneelta löytyy jo tuorein versio Virtualboxista, joten aloitan asentamalla Vagrantin.
  Yksinkertaisen asennusohjelman jälkeen Vagrant on asennettu:
  
  ![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/8603b93d-b23b-4574-94ae-7fc2e8a4982e)

  Vagrant haluaa, että kone käynnistetään uudestaan, teen sen.

  ![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/68f2dd38-f22d-4238-92d3-2d7fcf8be229)

Seuraavaksi avaan komentokehoitteen haluamasdtani kansiosta, helpoimmaksi tavaksi tähän olen aikanaan oppinut valita Windowsin resurssinhallinnasta kansion polun ja kirjoittamalla sen tilalle cmd.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/6fe7c866-fd83-4d39-977d-f1af2e5744fe)

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/fd50ab20-68e3-427a-aab0-a31e2992f467)

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/ed656042-b76e-4de3-9d3a-7f5eff7fa16b)


Kansiossa ei ole vielä virtuaalikoneen luomista varten Vagrantfileä, joten luon sellaisen komennolla 'vagrant init debian/bullseye64'

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/4b94013d-5d5b-416c-a9ac-7b5071214a87)

Komento loi Vagrantfile nimisen tiedoston aktiivisena olleeseen kansioon. Tiedosto sisältää vain kommentteja, lukuun ottamatta luotavan koneen tyyppiä ja käyttöjärjestelmää.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/0f7c8985-ed64-4377-8078-d38e8930d6ac)

Vagrant on nyt asennettu tämän hetken tiedon mukaan onnistuneesti, sillä sain käytettyä 'vagrant init' komentoa, joka teki mitä piti.

# b) Yksi maankiertäjä.

Aloitetaan luomalla äsken alustettu kone 'vagrant up' komennolla

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/bbb8d7d0-2e39-46d0-bd00-e43cf227f813)
1/2
![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/0d2ba49d-5847-4f76-aec3-320f4e73e5e0)
2/2

Vagrant loi virtuaalikoneen ilman virheilmoituksia. Yritän ottaa koneeseen ssh yhteyden komennolla vagrant ssh.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/c899c8e7-daf3-4554-968d-77cf9795e1e5)

Yhteys luotu ilman virheitä. Varmistan vielä verkkoon yhdistymisen käyttämällä 'ping' komentoa verkon ulkopuoliseen palvelimeen: ('man ping')

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/5cbf734b-da59-42c1-b6a7-3a78cb8508cb)

Palvelin vastaa, joten verkko toimii.

# c) Oma orjansa
Aloitan asentamalla salt-minion ja salt-master paketit virtuaalikoneelle.
![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/02d977a5-faac-463f-9a9f-a1258545122a)

Paketteja ei löytynyt, joten seuraan saltproject.io sivuilta löytyviä ohjeita saltin asentamisesta Debianille (HashCorp) 

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/fda83cd1-6209-4d77-bed0-60f06fbce19a)

Unohdettuani 'sudo' komennon huomasin, että vagrantin automaattisilla käyttöoikeuksilla ei ole mahdollista luoda kansiota. Yritän uudestaan sudo oikeuksilla

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/b4a7a7a2-b934-4025-978c-7119495599e8)

Päivitän myös paketit ajantasalle lisätäkseni curl paketin. 'sudo apt-get update' ja lataan paketin komennolla 'sudo apt-get install curl'

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/ded7c683-c7df-4d95-be2c-98dfc32de697)

Lisään asennusohjeen mukaiset tekstit tuskan kautta, sillä en keksinyt keinoa liittää Windowsista kopioimaani tekstiä virtuaalikoneelle. Onneksi kirjoittamiset menivät ensi yrittämällä oikein ja sain lisättyä avaimen ja lähteen saltin paketeille, sekä asennettua paketit

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/5a92b1df-19a3-4f64-b7a4-ccf04f20d955)

Kokeilin komennolla 'salt '*' test.ping' vastaavatko orjat herralle. Vastaukseksi tuli virhe johtuen siitä, että mitään laitetta ei ole määritetty tämän verkon herra-orja arkkitehtuurissa orjaksi.

Komento salt '*' test.ping avaaminen:
* salt komento osoittaa komennon kuuluvaan salt ohjelmalle
* '*' valitsee komennon kohteeksi kaikki verkkoon liitetyt orjat
* test.ping tarkistaa saako herra vastauksia orjilta (HashCorp)

Selvitän ensin ovatko molemmat demonit käynissä.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/babbf413-0f01-4e9f-998b-4609a0489fcb)

Master on käynnissä.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/d0281b60-0c18-4ca8-a5c3-f15835ce57eb)

Minion on käynnissä ja antaa virhetilaksi Master hostnamen virheellisyyden.
Haen käynnissä olevan koneen IP-osoitteen komennolla 'hostname -I'
Lisään minionin konffi tiedostoon tietoa komennolla 'sudoedit /etc/salt/minion' ja lisään tiedostoon herran IP-osoitteen oikeaan paikkaan. (Karvinen, 2023)

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/5e3ec89c-efe7-42ac-b168-2f3ec0749796)

Tässä vaiheessa yritän herättää demonit uudelleen henkiin ulkomuistista komennolla 'sudo systemctl reboot salt-minion'. Tällä saan aikaan virtuaalikoneen kaatumisen.


![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/e8573249-60a4-4b0c-b0c4-1f16bf92713c)

Varmistan hostnamen olevan yhä sama, kuin konffitiedostoon määritetty ja jatkan harjoitusta.
Seuraavaksi etsin orjan avainta komennolla sudo salt-key


![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/4f220f99-d4d6-4b3c-b8cd-f31cb3fa1d7e)

Haun tehtyäni näin orjan avaimen hyväksymättömien avainten joukossa ja hyväksyin avaimen komennolla 'sudo salt-key -a'.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/57d5d060-4f61-40fe-a72d-b19509d86af1)

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/87900443-a12c-4d8e-ace2-0d6a44cdf79d)
Lopuksi testasin vielä herra-orja suhteen toimimista samaisella 'sudo salt '*' test.ping' komennolla ja tällä kertaa tuloksena näkyi käytössä oleva kone ja tila True.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/276e238f-c349-46da-bf8d-f05a1976da75)




















  

