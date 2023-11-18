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
