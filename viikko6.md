# x) 

Halonen, Rajala ja Ollikainen 2023: Installing Windows 10 on a virtual machine

* Ohjeessa opastetaan asentamaan Windows 10 virtuaaliympäristöön
* Uutena tässä ohjeessa on host-only network adapterin käyttäminen.

LSB Workgroup, The Linux Foundation 2015: Filesystem Hierarchy Standard

* Erittäin looginen järjestelmä tiedon hallitsemiseen.
* Kappaleessa 3 selostettu hyvin ja lyhyesti kaikkien root kansioiden pääfunktio
* Kappalleessa 4 käyty käyttäjän hakemistoja löpi
* Itselle merkittävimmät kansiot ovat olleet /etc/, /tmp/ ja /srv/
* En ole natiivi linuxin käyttäjä, joten tullut oikeastaan vain tehtävien yhteydessä käytettyä. Tästä syystä muut eivät ole niin hyvin hallussa.


# a) Asenna Windows virtuaalikoneeseen

Käytän tässä tehtävässä ympäristönä Vagrantilla tehtyä verkkoympäristöä

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/b38efba7-56ad-466e-b793-63e0747cac99)

Virtuaalikone asennettu.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/d3a9dbab-f8c0-4a84-a749-d3b0155ed663)


# b) Asenna Salt Windowsille

Selvitän seuraavaksi mikä versio saltista minulla on herra koneella

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/963011be-94b5-463c-8f72-68f8cf6cd7b2)

Huomasin, että tätä versiota ei ole saltin repossa. Päivitän sen tmaster koneelle.
Lisäsin uuden lähteen ja avaimen keyringiin saltin sivuilta löytyvillä ohjeilla.
Tämän jälkeen päivitin uuden version komennoilla 'sudo apt update' ja 'sudo apt upgrade

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/faf3e6a0-ed62-4895-afa4-e04a4fd69655)


Tuorein versio asennettu.

Asennan seuraavaksi Saltin version 3006.4 virtuaalikoneella.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/533ededc-7d7b-4512-bc37-930a472208db)


Asennan tuoreen version

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/884a5387-d7c2-4bd3-a2b3-6031462ae140)


Määritän masterin IP-osoitteen master koneelta 'hostname -I' komennolla saamani komennon pohjalta.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/acdbbacb-b47e-4e1a-9aab-4b8819f67da3)


Käynnistän asennuksen jälkeen saltin.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/d2a1982a-7089-48c5-9210-ac8083e4527e)


Koetan 'salt-call --local' komentoa nähdäkseni toimiiko salt.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/de11f9a0-4fb9-4c70-af48-992987a9b5ce)


Salt asennettu.

Koetan vielä version.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/d109dd05-4e73-4498-a073-01b4058a89f9)


Ja master koneelta 'sudo salt-key'

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/f21df98b-ab5f-487f-bfec-454a47e98129)


'salt-key' ei löydä hakevaa konetta.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/78322d03-69df-4df0-ac12-900f70efb379)

Ping toimii koneiden välillä.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/c86f36c1-fd51-4a89-9cb3-ee9ccf6fdec9)


Yritän asentaa saltin uudelleen.

Lopputulos on sama, master ei löydä konetta.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/1bf4d9b6-6ed7-4edb-bd40-351574f19466)

Yritän vielä luoda koneet uudelleen.

Loin koneet uudelleen, mutta mikään ei tunnu toimivan.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/2e50e5dd-a529-4c44-98da-817d1324f781)

Olen yrittänyt nyt saada yhteyttä toimimaan useamman tunnin, eikä mikään tunnu auttavan. Luovutan tehtävän suhteen tältä erää. Valitettavasti myös seuraavat tehtävät jäävät tekemättä, sillä yhteys ei toimi.
Toivon oppivani yhteyden muodostamisen seuraavan luennon ohjeiden avulla.


Lähteet:

LSB Workgroup, The Linux Foundation 2015: Filesystem Hierarchy Standard, https://refspecs.linuxfoundation.org/FHS_3.0/fhs/index.html, luettu 3.12.2023
Halonen, Rajala ja Ollikainen, 2023 , Installing Windows 10 on a virtual machine, https://github.com/therealhalonen/PhishSticks/blob/master/notes/ollikainen/windows.md, luettu 3.12.2023
T.Karvinen, 2023, Infra as Code 2023, https://terokarvinen.com/2023/configuration-management-2023-autumn/, luettu 3.12.2023.
Saltproject, 2023, Windows Install guide, https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/windows.html, luettu 3.12.2023





















