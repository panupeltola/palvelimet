# x) 

Salt Vagrant - automatically provision one master and two slaves (Karvinen, 2023)

* Tekstissä käydään läpi saltin tilojen luominen erillisille tiloille sekä myös top.sls tiedoston luominen, jolla voidaan automatisoida tilojen ajamista

Rules of YAML (Salt Project)

* YAML on yhden tyyppinen syntaksi joka käyttää hyväkseen listoja, sanakirjoja ja normaaleja listoja.
* YAML toimii avain-arvo yhdistelmien avulla.
* Ylipäätään YAML syntaksi on erittäin tarkka ja välilyönneillä on paljon merkitystä.

Salt states (Salt Project)
* Saltin states komennoilla voidaan automatisoida ja erotella erittäin tehokkaasti verkon eri tarpeita ja laitteita toisistaan.
* Laaja määrä määrityksiä ja YAML syntaksin sallima listaus mahdollistaa monimutkaisten konfiguraatioiden yksinkertaistamista ja varmentamista sekä tarkentamista halutulle alustalle.
* Saltin kansiorakenteella on tarkka tarkoitus tiedostojen skaalan kannalta. Esimerkiksi onko jokin tiedosto tarkoitettu kaikille käytettäväksi vai moduulikohtaisesti.

Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port (Karvinen, 2018)

* Ohjeessa luodaan uusi moduuli ssh palvelimen ajamista ja määrittämistä varten
* Moduuli opastetaan tarkkailemaan juurikansioon tehtyä sshd_config tiedostoa ja muuttamaan sitä kaikilta laitteilta, mikäli se muuttuu herralla
* Lopuksi moduuli ajetaan






# a)
Aloitan luomalla Karvisen ohjeen mukaisesti verkkoympäristön yhdellä herralla ja kahdella orjalla.
Vagrantfile on jo määritetty aikaisempien tehtävien yhteydessä, joten en muuta sitä tässä vaiheessa.
Käynnnistän virtuaalikoneet Windowsin komentorivilttä komennolla 'vagrant up'

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/74943280-9195-4303-8f3f-d82832c20518)

Koneet käynnistymässä

Koneet saatu luotua, otan yhteyden herraan komennolla 'vagrant ssh' 

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/4dcc9780-e78d-4645-bfdb-12668174def8)

Varmistan, että orjakoneet näkyvät herralle komennolla 'sudo salt-key'

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/3da32574-43d5-49fa-b42a-2cc783d1daf2)

Koneet näkyvät joten hyväksyn niiden avaimet komennolla 'sudo salt-key -A' ja koetan yhteyden toimivuuden komennolla 'sudo salt '*' test.ping'

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/d744c008-d3e6-4f00-9b0e-ce61d8f5eb85)

Kaikki näyttäisi toimivan, joten ryhdyn kokeilemaan saltin 'state.apply' komennon toimintaa, mutta luon ennen sitä tilan.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/7203cef6-fdef-4981-8c5c-a26bd3bde9ce)

Loin ohjeen mukaisesti kansion /srv/salt/heimaailma/, luonnin yhteydessä totesin, että ilmeisesti sisennettyjä kansioita ei voi luoda kahta kerrallaan mikäli kumpaakaan niistä ei ole olemassa. (Karvinen, 2023)
Myöhemmin tajusin virheen johtuvan siitä etten käyttänyt komentoa 'mkdir -p /xxx'
Luon seuraavaksi tiedoston init.sls ja siirryn muokkaammaan sitä komennolla 'sudoedit init.sls'

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/84718d46-5f7e-46d4-ad51-569ef6c55950)

Yritän ensin luoda konfiguraatiotekstin muistista.
Tallennettuani init.sls tiedoston ajan tilan orjakoneille komennolla 'sudo salt '*' state.apply heimaailma'

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/8b040501-6e07-4c41-818c-5b453ffbeb1f)

Tilaviesteistä näen, että tiedostot ovat ainakin vastauksen mukaan luotu. Haluan vielä nähdä onko syntaksini ollut oikea ja sainko myös sisällön muutettua. Tarkastan sen komennolla 'sudo salt '*' cmd.run 'cat /tmp/heimaailma'

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/8a6bf42d-9126-43d0-8178-d6f58b752c27)

Koneet vastaavat oikean sisällön, joten oletan tilan toimivan.


# b)

Luon top.sls tiedoston Karvisen ohjeiden mukaisesti. (Karvinen, 2023)

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/e1f130d8-56c4-448b-9896-76d7c62fc187)

Yritän nyt ajaa moduulia heimaailma määrittelemättä sitä erikseen 'state.apply' komennon yhteydessä.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/c81f9300-0549-44bf-8c87-7605767016e9)

Sain vastaukseksi virheen ja nopealla silmäyksellä virhe voisi johtua niinkin pienestä ongelmasta kuin välilyönnin puutteesta "-heimaailma" moduulin osiossa. Katson onko korjauksen tarve ja ajan komennon uudestaan.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/59ecad28-92a1-48ad-bc36-d20592450383)

Tämä korjasi ongelman. Jos jotain tästä opimme, niin syntaksi on erittäin tarkka määrityksissä.
Koetan vielä lisätä toisen moduulin ja lisätä sen top.sls tiedostoon.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/55835513-78ba-482e-b39d-1bf0d7612f1d)

Luon uuden kansion ja lisään tilaksi tree paketin asennettuna olemisen.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/cd53a48e-e1fd-4b3d-964e-66d21b104588)

Lisään moduulin top.sls tiedostoon ja ajan komennon 'sudo salt '*' state.apply'

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/3ae20766-715e-45cc-a5b9-aeb24a97b6d4)

Tällä kertaa salt ajoi molemmat moduulit.

# c)

Kohtien b ja c välissä on vaihtunut päivä ja Vagrantin avulla luodut virtuaalikoneet on luotu uudestaan, joten aikaisempien kohtien tiedostoja ei enää ole olemassa.

Luon uuden tiedoston state.apply toiminnolla ja haluan nähdä, että se menee oikeaan kansioon.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/4410ba2f-f328-4c2d-873d-095b516eaf2d)

Ajan komennon komennon 'sudo salt '*' state.apply apache'

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/b9d883c2-2ec0-4f14-bc93-8b279574ccde)

Sain ilmoitukseksi virheen, yritän lisätä kansiopolun alkuun vielä yhden vinoviivan jos ongelma korjautuisi sillä. 

Sama virheviesti tuli yhä. Epäilen ongelmaksi sitä, että koneille ei ole asennettu apache2 palvelinta, yritän asentaa sen ensin.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/fb465803-2cab-46dc-b690-419a37d4e296)

Asennettuna ja esimerkki vastauksesta, asennus onnistui.
Ajoin myös 'sudo salt '*' state.apply apache' komennon uudestaan.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/a0e5f31f-869e-405d-8fe7-3792cd13301d)

Tällä kertaa virhe on poistunut.
Varmistan vielä, että tiedostojen sisältö on muuttunut komennolla 'sudo salt '*' cmd.run 'cat /var/www/html/testi.txt''

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/c36893cd-51bb-4204-9dd6-114310d20773)

Molemmat koneet antavat vastaukseksi oikean vastauksen. Poistan testitiedoston ja apachen laitteilta.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/b396a880-85bd-408d-9597-88b358cac6b5)

Testitiedosto poistettu

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/a987abb4-6d63-4b9c-87a5-5d05cf6a31dc)

Apache poistettu

Seuraavaksi yritän automatisoida apache2 palvelimen luomisen, käynnistämisen ja tiedon muuttamisen.
Loogisesti ajateltuna järjestyksen on myös oltava tämä.


![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/ec99fce8-8a05-41f7-ae42-380d602ad7f1)

Määritetty init.sls tiedosto.

Ajan komennon 'sudo salt '*' state.apply apache'

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/d09a85e7-d907-4044-9891-47d6637e88a0)

t002

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/15e78ac7-0b5a-4a78-a8cf-e0163f62b048)

t002 yhteenveto

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/0cb76b4a-d95e-46d9-9d90-61e174891e10)

t001 yhteenveto

Varmistan vielä, että palvelimet ovat pystyssä ja niiden sisältö on muutettu komennolla sudo salt '*' cmd.run 'curl 127.0.0.1'

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/ebc78720-6539-4e5a-b582-1ae7254f08fd)


Vastaus näyttää muutetun sisällön, totean määrityksen onnistuneeksi.




# d)

Luon uuden moduulin nimeltä ssh ja lisään siihen

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/ece281fe-7a08-4f0d-85a3-45ebf336082f)

Yritin saada tehtävää tehtyä, mutta en saanut watch komentoa toimimaan vaikka syntaksin ja saltin ohjeiden mukaan sen pitäisi olla oikein.


![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/94bb5937-5be4-4cbd-84b2-013d1656f224)

Löysin tässä vaiheessa karvisen sivuilta ohjeen ongelman ratkaisuun ja päivitin init.sls tiedoston.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/c545eabe-7522-49c6-b111-55d582e43430)


Ajettuani komennon sain seuraavan virheen:

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/b26392ef-fd22-470e-9a16-1bf3003bda41)

Kopioin samassa tiedostossa näytetyn ohjeen sshd_config tiedoston luomiselle.
Loin sen mukaan tiedoston ja ajoin komennon 'sudo salt '*' state.apply ssh' uudelleen saaden seuraavan virheen.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/dca7dedd-6c4a-42fd-b043-bca1d954ec61)


Huomasin, että minulla on virheellinen id file.managed polussa (on sshd vaikka pitäisi olla ssh)

Korjasin virheen ja ajoin komennon uudelleen.


![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/1c612e73-8100-4ec2-8b65-c627e3085612)


Vihdoin vihreää ja komento saatiin ajettua läpi.

Katsoin vielä mitä tapahtuu jos muutan sshd_config tiedostossa jotain ja ajan tiedoston uudelleen.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/39b9711d-dfb3-42b6-a5d7-2748142a0d0f)

Muutos ajettiin läpi myös muille koneille.


# Lähteet:

T. Karvinen, 2023, Salt Vagrant - automatically provision one master and two slaves, https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file, luettu 18.11.2023
T. Karvinen, 2023, Infra as Code 2023, https://terokarvinen.com/2023/configuration-management-2023-autumn/, Luettu 18.11.2023
T. Karvinen, 2018, Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port, https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh, luettu 19.11.2023
Salt Project, Rules of YAML, https://docs.saltproject.io/salt/user-guide/en/latest/topics/overview.html#rules-of-yaml, luettu 19.11.2023
Salt Project, State Modules, https://docs.saltproject.io/salt/user-guide/en/latest/topics/states.html#state-modules, Luettu 19.11.2023


























