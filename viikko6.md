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










