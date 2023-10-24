Komennolla vagrant up törmäsin seuraavaan ongelmaan
he IP address configured for the host-only network is not within the

allowed ranges. Please update the address used to be within the allowed

ranges and run the command again.



  Address: 192.168.12.100

  Ranges: 192.168.56.0/21



Valid ranges can be modified in the /etc/vbox/networks.conf file. For

more information including valid format see:



  https://www.virtualbox.org/manual/ch06.html#network_hostonly

Yritin korjata asiaa vaihtamalla ip osoitteet Vagrantfilessä 192.168.56.255 muotoon
Ratkaisu ohitti yhden ongelman, mutta seuraavassa vaiheessa tuli uusi virhe:
There was an error while executing `VBoxManage`, a CLI used by Vagrant

for controlling VirtualBox. The command and stderr is shown below.



Command: ["startvm", "1f4d8956-4905-44d7-8f32-af5f7ad59a52", "--type", "headless"]



Stderr: VBoxManage: error: VT-x is not available (VERR_VMX_NO_VMX)

VBoxManage: error: Details: code NS_ERROR_FAILURE (0x80004005), component ConsoleWrap, interface IConsole


17:59
Hetken asiaa mietittyäni totesin, että olin jo tehnyt alustuksen virtuaalikoneille ja yritän asentaa sen uudestaan ja edetä Salt Vagrant ohjeen mukaisesti
Sama ongelma toistui vaikka asensin molemmat ohjelmat uudestaan. Myöskään ensimmäisen virhekoodin määrittämää hakemistoa /etc/vbox ei löydy
18:07
Ongelma vaikuttaa johtuvan virtualisoinnin estosta virtuaalikoneessani. Yritän muuttaa asetuksia BIOSista.

18:16
Muutettuani virtualboxin asetuksista mahdollisuuden virtualisoida virtuaalikoneella sain vihdoin vagrant up komennon päättymään muuhun kuin virheeseen.
Päästyäni sisään minulla ei näkynyt hyväksyttäviä avaimia ja huomasin, että olin unohtanut vaihtaa kaikki IP-osoitteet konfigurointitiedostosta.
Korjaan ja yritän uudestaan.
Korjatessa kaikki hajosi kun Virtualbox kaatui. Ei anna tehdä mitään koska en ole ilmeisesti sama käyttäjä.
Asennan virtuaalikoneen uudestaan ja yritän myöhemmin.
