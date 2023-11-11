# Host ympäristö:
* Windows 10
* Intel Core i7-10770K
* Nvidia GeForce 3080
* 32 GB RAM
* Virtualbox 7.0.12
* Debian 11 virtuaalikone

# a) Online

Aloitan tehtävän luomalla uuden GitHub repositorion tilini "Your repositories" ikkkunasta

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/ae9a69da-c6c7-4059-ac39-eff5ef2b62d0)

Varmistan, että nimi kelpaa ja luon lyhyen kuvauksen repositorion luonteesta.
Lisäksi varmistan, että hakemistoon luodaan readme tiedosto ja lisenssityyppi on oikea.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/9b244bef-80fa-4877-bd8a-3d17e5e080f2)


Repositorio luotu.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/37ee84d8-3eb7-4f46-8d38-760df129cab0)


# b) Dolly

Varmistan ensin, että virtuaalikoneelleni on asennettu git. Kuvaa ennen on ajettu komento 'sudo apt-get update' 

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/6fca1b14-7935-42f9-a5af-26fc0fe50080)


Ei päivitettävää eikä asennettavaa, joten uusin Git on asennettuna.

Aloitan yrittämällä luoda yhteyttä ssh linkillä GitHubin sivuilta.
GitHub kuitenkin ilmoittaa jo tässä vaiheessa, että SSH-salausavainta ei ole, joten nähdäkseni on turha mennä pidemmälle ennen kuin tämä ongelma on ratkaistu.

Luon SSH-avainparin komennolla 'ssh-keygen'

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/3462d4e5-3c75-4a61-84cd-8a183dfd5ae0)


Avaimet luotu.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/54f85f46-6449-4c7d-b4ef-295eefb8ba80)


Lisään avaimen GitHubin käyttäjän asetuksista kohdasta "SSH and GPG keys"
Lisään julkisen avaimeni tähän kohtaan.
Avain näkyy listassa.
![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/a011d211-8729-46ef-b9c0-11d4894ae012)

Yritän kopioida SSH-linkkiä uudelleen ja varoitus on poistunut.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/2f13b22d-29f9-42d8-9286-d97e453e777e)

Kopioin SSH-linkin ja kloonaan repositorion komennolla 'git clone git@github.com:panupeltola/gitgudwinter.git'.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/e69926e1-b7fa-41b9-9d29-5cb488e22f1d)

Pienen tuskailun jälkeen ymmärsin, että minun pitää olla luodussa hakemistossa, jotta voin käyttää gitin komentoja.
Siirryin oikeaan hakemistoon ja ajoin komennon 'git pull'.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/5e2f58fe-96e6-4bc2-a263-e7e9b2a6ba75)

Kansion sisältö komennolla 'ls' vastasi verkkoselaimen sisältöä.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/98fbd8da-e626-42b4-a919-b3fb600eac8d)

Luon testitiedoston test.py ja lisään sen sisään tekstin "jouluun on käytännössä kuukausi".


![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/02e48c28-9068-4ba6-b104-29c04b7b4b3b)

Tiedoston luonti

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/6b41c4f9-bcd1-4a3b-af1f-ce7b386e14f3)

Muokkaaminen microlla.

Nyt komennolla 'git status' näen tekemieni muutosten tilan. Näen, ettei test.py tiedostoa ole vielä tallennettu muutokseksi.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/a8344289-5af5-4590-a8da-c5cb1d44ca55)

Teen sen seuraavaksi komennoilla 'git add .' ja 'git commit'
![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/64f4aeca-3cd3-4133-9cd4-8201e702b31d)

Ajettuani komennon, tuli virhe, ettei käyttäjälleni ole vielä määritetty sähköpostia tai nimeä. Näille annettiin komennot virheviestissä. Lisään nämä ja yritän ajaa komentoa uudestaan.

![kuva](https://github.com/panupeltola/palvelimet/assets/148875059/eca000c7-b9db-47bf-8c8c-4687206416d4)
Ajettuani komennot terminaalini meni tilaan, mistä en päässyt takaisin ajamaan komentoja. Päätin käynnistää koneen uudelleen.


















