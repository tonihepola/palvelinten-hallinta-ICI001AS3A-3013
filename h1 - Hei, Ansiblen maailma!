# h1 - Hei, Ansiblen maailma!

a)
Päivitin järjestelmän sudo apt-get update komennolla jonka jälkeen latasin ssh:n sudo apt-get -y install ssh komennolla.
Laitoin ssh:n päälle sudo systemctl enable --now ssh komennolla.
Kokeilin ssh:n toimivuutta ssh localhost komennolla, kirjauduin salasanalla ja tarkistin vielä W:llä että olin kirjautuneena sisään.
Poistuin ssh:sta exit komennolla.

b)
Loin avaimen ssh-keygen komennolla, jonka jälkeen kopioin sen ssh-copy-id localhost komennolla.
Kokeilin avaimen toimivuutta ssh localhost komennolla.
Avain toimi, sillä ei tarvinnut kirjautua sisään enään salasanalla.

c)
Päivitin taas järjestelmän ennen ansiblen lataamista.
Latasin ansiblen sudo apt-get install ansible micro bash-completion tree komennolla.
Latasin siis ansiblen lisäksi micron ja bash-completionin.
Loin ansiblea varten tiedoston, jonne lisäsin micro hosts.ini tiedoston.
Hosts.ini:iin lisäsin localhost:in.
Kokeilin että ansible toimii ansible all -a 'uptime' -i hosts.ini komennolla.
Ansible valitti pythonista, poistin ilmoituksen lisäämällä [all:vars] ansible_python_interpreter=/usr/bin/python3.
Loin micro site.yml jossa annoin hosteille roolit "hello".
Tein rooleille oman tiedoston ja micro tiedoston jonne kirjoitin contentiksi "Hei maailma\n".
Tarkistin ansible-playbook site.yml komennolla että tiedostoon oli tullut muutos.
Ajoin tiedoston vielä ssh localhost cat /tmp/hello-ansible komennolla.
Hei maailma tulostui onnistuneesti.

x) 
- SSH on yleinen ja turvallinen kirjautumistapa.
- Avainpari luodaan ssh-keygen komennolla.
- Avain kopioidaan palvelimelle ssh-copy-id komennolla.
- Kirjautuminen onnistuu ilman salasanaa.
Kuinka todennäköistä on, että yksityinen avain joutuisi vääriin käsiin? 

- Ansible toimii SSH:n kautta.
- Komentoja voidaan ajaa useammalla koneella samaan aikaan.
- Rooleilla on omat tehtävät.
- Sisennykset tehdään välilyönnillä, ei TAB:illa.
- Mahdollista automatisoida järjestelmiä helposti.
Miksi sisennystä ei ole mahdollista tehdä TAB:illa?.

## Lähteet
Karvinen Tero 2026. SSH public key - Login without password. Luettavissa:
https://terokarvinen.com/ssh-public-key-login-without-password/
Luettu: 31.3.2026

Karvinen Tero 2026. Hello Ansible. Luettavissa: 
https://terokarvinen.com/hello-ansible/
Luettu: 31.3.2026
