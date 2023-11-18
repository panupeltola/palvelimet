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

Loin ohjeen mukaisesti kansion /srv/salt/heimaailma/, luonnin yhteydessä totesin, että ilmeisesti sisennettyjä kansioita ei voi luoda kahta kerrallaan mikäli kumpaakaan niistä ei ole olemassa.
Luon seuraavaksi tiedoston init.sls ja siirryn muokkaammaan sitä komennolla 'sudoedit init.sls'

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/84718d46-5f7e-46d4-ad51-569ef6c55950)

Yritän ensin luoda konfiguraatiotekstin muistista.
Tallennettuani init.sls tiedoston ajan tilan orjakoneille komennolla 'sudo salt '*' state.apply heimaailma'

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/8b040501-6e07-4c41-818c-5b453ffbeb1f)

Tilaviesteistä näen, että tiedostot ovat ainakin vastauksen mukaan luotu. Haluan vielä nähdä onko syntaksini ollut oikea ja sainko myös sisällön muutettua. Tarkastan sen komennolla 'sudo salt '*' cmd.run 'cat /tmp/heimaailma'

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/8a6bf42d-9126-43d0-8178-d6f58b752c27)

Koneet vastaavat oikean sisällön, joten oletan tilan toimivan.


# b)

Luon top.sls tiedoston Karvisen ohjeiden mukaisesti.

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












