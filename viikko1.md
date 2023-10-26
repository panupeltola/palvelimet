# Harjoitus viikko 1


## https://terokarvinen.com/2023/configuration-management-2023-autumn/

# Create a Web Page Using Github
Helposti tehty
Repository luotu ja uuden tiedoston perään vain .md ja homma rullaa
Ei aikaisempaa kokemusta käytöstä, mutta vaikuttaa yksinkertaiselta



# 26.10.2023 18.25
# Dell Windows 10 läppäri ja VirtualBox 7.0
Aloitin päivän lataamalla ja asentamalla Debianin virtuaalikoneen yrittääkseni uudelleen
En saanut Debiania toimimaan pitkän yrityksen jälkeen ja päätin käyttää tähän harjoitukseen Ubuntua, jonka kanssa olen tutumpi ja harjoitella Debiania paremmalla ajalla
Yrittäessäni lisätä sudo oikeuksia käyttäjälleni rootin kautta sain vain error viestin "command adduser not found"
Komenolla  /sbin/adduser username sudo sain vahvistuksen, että käyttäjäni olisi lisätty sudo ryhmään, mutta sudo toiminto ei silti toiminut.
Yrittäessäni ajaa ohjeessa ollutta koodia saltin asentamiseen sain virheen curl komennon puutteesta ja yrittäessäni asentaa sen pakettia terminaalini jumahti puuttuvan cd levyn pyytämis looppiin. Tässä vaiheessa päätin vaihtaa tutumpaan, sillä en kertausharjoituksien takia ehdi muina päivinä enää tätä tehtävää tehdä.
## https://medium.com/platform-engineer/how-to-enable-sudo-on-a-user-account-on-debian-494d3c75ee21
## https://milq.github.io/enable-sudo-user-account-debian/
## https://terokarvinen.com/2023/configuration-management-2023-autumn/




# Dell Windows 10 läppäri ja VirtualBox 7.0 Ubuntu 
Saltin asentaminen onnistui sivuilta löytyvän ohjeen avulla luoden ensin luottamuksen ohjelman avaimiin ja sen jälkeen asentamalla salt-minion paketin

komento sudo salt-call --local -info state.single pkg.installed alex4 varmistaa, että tietokone on tavoitetilassa, jossa jokaisesta verkkoon liitetystä koneesta löytyy paketti alex4 asennettuna.
Ensimmäisen kerran ajettuna komento asensi paketin, sillä se ei ollut vielä asennettuna ja komento vaatii sen idempotentin eli tavoitetilan saavuttamiseksi.
Komento sudo salt-call --local -l info state.single pkg.removed alex4 varmisti, ettei käyttöalueen koneissa ole tämän tyyppisiä aikaa tuhlaavia sovelluksia. 
Ajamalla komento toistuvasti voidaan siis varmistaa, että halutut paketit pysyvät asennettuina tai poistettuina.
Yhdellä komennolla ei kokeilun perusteella voi asentaa useita ohjelmia lisäämällä niitä välilyönnillä peräkkäin, kuten apt-get install komennosa

Komento sudo salt-call --local -l info state.single file.managed /tmp/moipanu luo rootin tmp kansioon uuden tekstitiedoston nimeltä moipanu, se ei sisällä tekstiä
Komento sudo salt-call --local -l info state.single file.managed /tmp/moipanu contents="testiä" muuttaa tiedoston sisältöä heittomerkkien välissä olevaan tietoon
Kokeilin myös, että komento luo uuden tiedoston, mikäli vanhaa ei ole olemassa tai se on poistettu
sudo salt-call --local -l info state.single file.absent /tmp/moipanu komennolla varmistetaan, että tiedostoa ei ole tai se poistetaan
Tässä komennossa contents lisäys ei muuttanut mitään ja tiedosto poistettiin riippumatta täsmäsikö teksti arvoon vai ei

service.running komennot varmistavat, että haluttu demoni on ajossa tai poissa ajosta jokaisella hallitulla koneella. enable=TRUE varmistaa demonin päällä olemisen ja enable=FALSE sen pois päältä olemisen

user.present ja user.absent varmistavat, että käyttäjä on tai ei ole olemassa. 

Komento cmd.run oli hiukan hankalampi ymmärtää alkuun.
Esimerkki sudo salt-call --local -l info state.single cmd.run 'pwd>>/tmp/kokeilu' creates="/tmp/testi"
Komennossa ehtona toimii "merkkien sisällä oleva testi, jossa komento creates tarkastaa onko kansiossa tmp kohdetta testi. Mikäli testi epäonnistuu päivitetään käyttäjän nykyinen työkansio tiedostoon kokeilu
Komento on yksinään turha, sillä se ei voi mitenkään saattaa konetta idempotenttiin.
## https://terokarvinen.com/2021/salt-run-command-locally/





# d)
sudo salt-call --local grains.item osfinger virtual palautti arvot:
local:

    ----------

    osfinger:

        Ubuntu-22.04

    virtual:

        VirtualBox


local:

    ----------

    cpu_model:

        Intel(R) Core(TM) i7-8665U CPU @ 1.90GHz

    num_cpus:

        3

    username:

        root




grains.items listaavat parametrit sai listattua komennolla sudo salt-call --local grains.ls | more
Tästä listasta valitsin itseä kiinnostavat asiat ja etsin niistä tiedot komennolla:
sudo salt-call --local grains.item cpu_model num_cpus username

Komennon tuloste näkyy yläpuolella.

Kaiken kaikkiaan salt vaikuttaa erittäin tehokkaalta työkalulta, jonka tehokas käyttö vaatii kuitenkin harjoitusta ja kokematon käyttäjä voi saada sillä lyhyessä ajassa hyvin paljon tuhoa aikaiseksi.

## https://docs.saltproject.io/en/latest/topics/grains/index.html
 




