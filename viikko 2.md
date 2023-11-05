# Viikon 2 tehtävät

# x)

Slater 2017: What is the definition of "cattle not pets"
* Palvelinkoneista tehdään joissain tapauksissa verkon toiminnan kannalta korvaamattomia
* Niiden rakentamiseen käytetään valtava määrä aikaa ja energiaa, sekä yhdelle koneelle jää suuri määrä vastuuta verkon toiminnan kannalta
* Tällaisia verkkoja kutsutaan artikkelissa lemmikeiksi, joita varjellaan ja pidetään uniikkeina.
* Vastakohdaksi nostetaan palvelinkoneiden pitämistä tuotantokarjana.
* Nopeasti uusittavilla ja ylipäätään suurella määrällä saadaan luotettavuutta verkkoon, missä yhden koneen puuttuminen ei ole välttämättä edes huomattavissa
* Uudet palvelinkoneet voidaan luoda automaatiolla.
* Nopeasti vaihtuvat koneet eivät kuitenkaan toimi tekstin mukaan hallituissa ympäristöissä.
(Slater, 2017)

Karvinen 2017: Vagrant Revisited – Install & Boot New Virtual Machine in 31 seconds  
* Ohjeessa opetetaan luomaan uusi virtuaalikone käyttäen Vagrant ja Virtualbox ympäristöä
* Ensimmäisessä osassa päivitetään linuxin pakettitiedot ja asennetaan Vagrant sekä Virtualbox
* Toisessa osiossa alustetaan virtuaalikone, käynnistetään se ja otetaan siihen SSH-yhteys
* Lopuksi virtuaalikone tuhotaan
(Karvinen, 2017)
  
Toisen osion komennot

* 'vagrant init' = Luo virtuaalikoneen luomiseen käytettävän Vagrantfilen, mikäli sellaista ei vielä ole työkansiossa. Koneelle voi myös antaa paljon muita arvoja kuin koneen tyypin, esimerkiksi nimen. 
* Mikäli työkansiossa on jo Vagrantfile, komento ei luo uutta
* 'vagrant up' = Luo Vagrantfilen määrittämän virtuaalikoneen tai koneet
* 'vagrant ssh' = Ottaa SSH-yhteyden virtuaalikoneeseen
* Mikäli 'vagrant up' komennolla olisi luotu useampi virtuaali kone tämä komento yhdistäisi vakiovaihtoehdoksi määritettyyn koneeseen
 (HashCorp)

Karvinen 2023: Salt Vagrant - automatically provision one master and two slaves
* Ohjeessa kuvataan verkkoympäristön luominen käyttäen valmista konfigurointitiedostoa
* Konfigurointitiedostossa luodaan kaksi konetyyppiä, joiden pohjalta luodaan kolme konetta. Kaksi orjaa ja yksi herra.
* Yhdellä herrakoneella voidaan hallita kahta orjaa saltin avulla
* Ohjeessa käydään läpi Karvisen ohjeen "Run Salt Command Locally" (Karvinen, 2021) komentoja
* Tämän lisäksi koneista kerätään keskitetysti tietoa.
* Lopussa luodaan ja ajaetaan automaatioon johtavaa komentoa.
* Tämän ohjeen avulla saa erittäin helposti luotua kolmen koneen toimiva ympäristö, jota käytän myös tämän viikon myöhemmissä tehtävissä.
(Karvinen, 2023)

  


# Ympäristö
* Windows 10
* Intel Core i7-10770K
* Nvidia GeForce 3080
* 32 GB RAM
* Virtualbox 7.0.12

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

# d) Asenna Saltin herra-orja arkkitehtuuri toimimaan verkon yli
Käytän tähän Tero Karvisen ohjeessa "Salt Vagrant - automatically provision one master and two slaves" valmiiksi määritettyä verkkoympäristöä. (Karvinen, 2023)
Muokkaan aiemmin luotua Vagrantfileä Windowsin notepad sovelluksella sisältämään ohjeen teksti.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/8cd9315d-1c57-4517-8eb6-bd3ccc8ec125)

Tutkiessani Karvisen ohjetta siitä miten virtuaalikoneet ovat määritetty huomaan pari asiaa. Vagrantfilessä määritetään kaksi eri tyyppiä master ja minion.
Minionille lähetetään tiedostossa määritetty herran IP-osoite saltin minion konfiguraatiotiedostoon samalla tavalla, kirjoittamalla se /etc/sudo/minion/ tiedostoon.
Tämän lisäksi jokaiselle koneelle ajetaan käsittääkseni koneen tyypin mukaiset määritetyt komennot käynnistyksen yhteydessä.
Määrityksen yhteydessä annetaan myös valmiiksi koneille nimet "tmaster", "t001" ja "t002".



Tämän jälkeen käynnistän ympäristön samalla tavalla kuin edellisessä tehtävässä komennolla 'vagrant up'


![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/689e6091-dfa4-4a4f-84c5-6e7a0a28f7a6)

Koneet käynnistyivät ilman virheilmoituksia.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/81855fb8-eb24-4254-b6ba-b379f1c14179)

Edellisen harjoituksen perusteella oppimastani nopein tapa nähdä ovatko koneet määritetty oikein on varmistaa se herrakoneelta 'sudo salt-key' komennolla.
Mikäli kaksi orjaa näkyvät luettelossa hyväksymättöminä avaimina on yhteyden muodostaminen onnistunut.
Kokeilen testin vuoksi mihin koneeseen verkossa komento 'vagrant ssh' yhdistää.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/7bf8f70c-1d93-48ea-a2c2-2adc6f40bc4b)

Komento yhdisti "tmaster" koneeseen. Tämä johtuu Vagrantfilessä tmasterin konfiguraatiossa olevasta komennnosta 'primary: true do |tmaster|', mikä tekee tmaster koneesta oletusen niissä komennoissa, missä pitää valita kone tai ryhmä, mutta sitä ei ole erikseen komennolla määritetty. (HashCorp)

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/237849e0-e9a0-4496-8a85-508e43019a41)

'sudo salt-key' Komento näyttää molemmat orjat luettelossa. Hyväksyn niiden avaimen ja varmistan verkon toimivuuden 'sudo salt '*' test.ping' komennolla.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/759b1c9c-1e90-4ae5-9af8-acb92d48d921)


Molemmat koneet antavat vastaukseksi 'True', joten oletan tässä vaiheessa verkon toimivan.


# e) Aja useita idempotentteja (state.single) komentoja verkon yli

Testaan komentoja ajamalla niitä herrakoneelta orjille.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/2db7d261-c287-4a49-b99b-d6466bfbf913)

Yrittäessäni ajaa komentoa 'sudo salt-call '*' state.single pkg.installed tree' tuli virheeksi sama virhe kuin edellisessä tehtävässä, missä master kone on väärin konfiguroitu minionille. Tämän ei pitäisi kuitenkaan olla mahdollista, sillä molemmat orjat on yhdistetty jo tmasteriin onnistuneesti. Tutkin onko komento väärä ja yrittääkö salt-call asentaa ohjelmaa myös tmasterille, mikä ei ole orjana millekkään.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/c3e2f8e2-7d2f-457b-bfdf-b0ba711ef3d5)

Yrittäessäni muokata minion tiedostoa tmaster koneella sain tiedon, ettei koko tiedostoa löydy. Googlasin siis 'salt-call' komennon ja  totesin komennon olevan ongelman etsimiseen nykyisessä kontekstissa, eikä koneiden hallintaan tarkoitettu. Tämän hoitaa komento 'salt'. (HashCorp)

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/188d5083-d047-438f-8c50-eed767893c6f)

t001 

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/eb70af02-40f1-443d-9800-ab4678b7c315)

t002


Sain komennolla 'sudo salt '*' state.single pkg.installed tree' tarkastettua koneiden idempotentin paketin 'tree' asennettuna olemisen osalta. (Karvinen, 2021)

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/7562ed0e-9166-401d-8c52-7415abae56d9)

t001

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/2850f0f9-099b-496f-b6cc-dd18aafc7269)

t002

Komento 'sudo salt '*' state.single pkg.removed tree' tarkasti koneiden idempotentin paketin puutteesta.

Asensin vielä "tree" paketin orjille ensimmäisellä komennolla varmistaakseni ohjelmiston asentumisen ja tarkastamalla sen orjilta.

Poistun tmaster koneesta komennolla exit ja kirjaudun sisään koneelle t001 komennolla vagrant ssh t001. Tässä on määritettävä koneen nimi, sillä aiemmin mainittuna komennon vakiokohde on tmaster ilman erillistä määritystä.

t001 näyttää seuraavaa komennolla 'sudo apt list tree' joka tarkastaa paketin tree asennettuna olemisen (Dancuk, 2022)

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/d6a23abb-4049-4e81-a521-d6bb684b3bf2)

Paketti näkyy asennettuna, tarkastan sen myös koneesta t002 samoilla askeleilla.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/c57d121f-3245-47a5-9363-cf5fc4432338)

Näkyy asennettuna.

Tarkastan vielä saman asian tmaster koneelta

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/446f7818-4a8a-4221-877c-386de9d36d33)

Pakettia tree ei ole asennettu, joten tästä voi päätellä, etteivät "salt '*'" komennot aja herralla samoja komentoja kuin orjilla


Yritän vielä muita komentoja:

'sudo salt '*' state.single sevice.running salt-minion

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/9d8a5a56-de2e-49ea-b0f7-e39a569f45ed)

t001

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/96e9a234-0ba3-4059-ab29-b2e6d09faf27)

t002


Komento toimii, koitan vielä miten koneet reagoivat.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/edddb040-b467-4999-903b-95c43803fce4)

Komento toimi, mutta koneet eivät vastanneet enää, sillä suljin salt-minion demonin.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/0fc5efcf-5b4f-4ac2-a8cf-7af0ef0b5b62)

Komennolla ei myöskään voinut enää palauttaa demonia toimintaan. Käynnistän sen orja koneilta erikseen komennolla 'sudo systemctl start salt-minion'.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/30cd2848-8a1a-4757-904b-176c778581c0)

Esimerkki t001 koneelta


![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/1d6fba1c-ad86-49f3-b763-817a93fcaddc)

Koneet saatu takaisin verkkoon

Komennot toimivat samalla tavalla, kuin viikon 1 tehtävissä testauksen jälkeen, joten luotan niiden toimivan oikein myös muissa tärkeimmissä komennoissa.


# f) Kerää teknistä tietoa orjista verkon yli (grains.item)

Ajan komennon 'sudo salt '*' grains.items' saadakseni tietoon halutut parametrit verkon orjista.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/3429d93c-7e0f-4f10-94f2-3de6f5523191)

t001 alku

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/37a8ba07-c377-4f02-ad86-09ef68d1e5e5)

t002 alku


Hetken komentoa 'sudo salt '*' grains.items osfinger' ihmettelin minkä takia vastaukseksi tuli aina koko lista ominaisuuksista vaikka pyysin vain yhtä.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/98f6900e-6e06-4653-962b-435b0d3bd10d)

Lopulta ymmärsin komennon olevan väärä ja todellisuudessa komennon tulee olla muotoa 'grains.item osfinger'. Yksi s kirjain muutti koko komennon toiminnan tässä tapauksessa (HashCorp)


![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/53f3112d-0572-4d20-bdf3-a681e8804787)


# g) Aja shell-komento orjalla verkon yli.

Käytän Salt Projectin esimerkkiä oppaana ja ajan komennon 'sudo salt 't001' cmd.run 'ls -l /etc''
Kohdistan komennon pelkästään koneelle t001 tässä tapauksessa kokeilun vuoksi

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/74919753-9571-4a30-bbb4-2046a777aa2a)


Komento palauttaa listan t001 /etc kansion sisällöstä.

Yritin myös liikkua komennoilla koneen t001 sisällä, mutta pwd pysyy koko ajan rootissa, eikä komennolla voi luoda ilmeisesti uusia kansioita (Ainakaan ne eivät näy orjakoneella)

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/cfc3caf6-0703-4375-8696-32b0a25559d3)


# h) Hello, IaC

Luodaan ensin vaadittava kansio /srv/salt/hello ja luodaan sen sisään tiedosto init.sls 
![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/66e5e0e7-d73d-47ab-b5c0-2a222cba1646)

Seuraavassa kohdassa lisään ajettavan init tiedoston sisään idempotenttitilan /tmp/infra-as-code tiedoston olemassa olosta. Tämä tapahtuu 'file.managed' komennolla.
Mikäli tiedostoa ei löydy se luodaan. (Karvinen, 2017)

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/b38058fe-1732-48fa-bbe0-b39669918c59)

Komentokehote ajetaan komennolla 'sudo salt '*' state.apply hello'. Tämä ajaa vain hello kehotteen ja kyseinen kehote pitää mainita joka kerta kun se halutaan ajaa.
'state.apply' komento toteuttaa tiedostot, jotka on konfiguroitu sen top.sls tiedostoon. (HashCorp)

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/8e8ebf87-b0c1-4e84-bddb-d02717aaf295)
t001

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/bdc78833-d2fe-4e12-b853-8acbdfa060d1)
t002

Kun komento on ajettu, siitä tulee vastaukseksi molemmilta koneilta saman tyyppinen viesti, kuin mitä aiemmin ajettuna 'file.managed' komennolla, eli state.apply' komennolla saadaan tämäkin automatisoitua.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/c2b1eb2b-1b7d-4401-a493-947ce0eeeb9b)

Lopuksi vielä varmistan tiedoston olemassa olon molemmilla koneilla ajamalla niille shell komennon 'ls /tmp/' saltin avulla komennolla 'sudo salt '*' cmd.run 'ls /tmp/''.
Molempien koneiden hakemistoissa näkyy tiedosto infra-as-code joten totean 'state.apply' komennon toimineen oikein



Lähteet:
* T. Karvinen, 2023, Infra as Code 2023, https://terokarvinen.com/2023/configuration-management-2023-autumn/, luettu 5.11.2023
* T. Karvinen, 2017, Vagrant Revisited – Install & Boot New Virtual Machine in 31 seconds, https://terokarvinen.com/2017/04/11/vagrant-revisited-install-boot-new-virtual-machine-in-31-seconds/, luettu 4.11.2023
* T. Karvinen, 2021, Run Salt Command Locally, https://terokarvinen.com/2021/salt-run-command-locally/, luettu 4.11.2023
* T. Karvinen, 2023, Salt Vagrant - automatically provision one master and two slaves, https://terokarvinen.com/2023/salt-vagrant/, luettu 4.11.2023
* Salt Project, salt.modules.grains, https://docs.saltproject.io/en/latest/ref/modules/all/salt.modules.grains.html, luettu 5.11.2023
* Salt Project, Running Commands on Salt Minions, https://docs.saltproject.io/en/latest/topics/execution/remote_execution.html, luettu 5.11.2023
* HashCorp, Multi-Machine, https://developer.hashicorp.com/vagrant/docs/multi-machine#specifying-a-primary-machine, luettu 4.11.2023
* HashCorp, Init, https://developer.hashicorp.com/vagrant/docs/cli/init, luettu 4.11.2023
* HashCorp, Up, https://developer.hashicorp.com/vagrant/docs/cli/up, luettu 4.11.2023
* HashCorp, SSH, https://developer.hashicorp.com/vagrant/docs/cli/ssh, luettu 4.11.2023
* M. Dancuk, How to List Installed Packages on Ubuntu, https://phoenixnap.com/kb/ubuntu-list-installed-packages, luettu 4.11.2023


















































  

