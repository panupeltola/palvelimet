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











  

