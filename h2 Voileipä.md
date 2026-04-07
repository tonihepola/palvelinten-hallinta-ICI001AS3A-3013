# h2 - Voileipä

a)  
Tein ansiblea varten "anston" käyttäjän jolla voi käyttää sudoa ilman salasanaa.   
Käytin komentoja sudo adduser anston, sudo groupadd sudoless, sudo adduser anston sudo, sudo adduser anston adm ja sudo adduser anston sudoless.  
Avasin uuden välilehden terminaalissa ja lisäsin %sudoless ALL = (ALL) NOPASSWD: ALL, sudo visudo /etc/sudoers.d/sudoless:iin.  
Vaihdoin terminaalin välilehteä ja kokeilin että anston toimii niin kuin pitääkin.  
<img width="600" height="348" alt="sudo salasanaton" src="https://github.com/user-attachments/assets/a79b83ac-4a39-49ce-b16d-d257df2aed32" />  

b)  
Käytin tehtävässä olemassa olevaa anston käyttäjää. Tein käyttäjälle /roles/anston/tasks/main.yml tiedoston ja muokkasin site.yml tiedostoa lisäämällä sinne anston roolin ja "become: true"  
Tarkistin onko virheitä ajamalla playbookin ja kirjauduin ssh:lla sisään ilman salasanaa. <img width="700" height="671" alt="Näyttökuva 2026-04-07 133153" src="https://github.com/user-attachments/assets/40143c69-096f-4235-b52f-5749a73ab2b0" />
<img width="700" height="675" alt="Näyttökuva 2026-04-07 133245" src="https://github.com/user-attachments/assets/07917d73-2fba-4ca3-93d2-fb5b5288d08f" />

c)  
Asensin cowsay ja htop paketit ansiblella käyttäen apt-moduulia. 
Ajoin playbookin jotta näkisin tuliko mitään virheitä ja asentuivatko paketit onnistuneesti. 
Kokeilin vielä että toimivatko paketit. <img width="713" height="204" alt="Näyttökuva 2026-04-07 141357" src="https://github.com/user-attachments/assets/6220141c-52e8-493e-ba55-4a844a7d25a8" />
<img width="800" height="728" alt="Näyttökuva 2026-04-07 141519" src="https://github.com/user-attachments/assets/74325ce9-3db5-4df8-ad1b-9bf2fab7f77e" />
<img width="660" height="362" alt="Näyttökuva 2026-04-07 141559" src="https://github.com/user-attachments/assets/973c534c-33f6-414f-984d-48f00482d412" />

d)  
Tein localhostille "teksti.txt" tiedoston johon kirjoitin ansiblella käyttäen copy toimintoa.
Määritin anstonin omistajaksi sekä ryhmäksi ja laitoin "0640" oikeudet.
Symbolisesti oikeudet ovat -rw-r-----, eli omistajalla on luku ja kirjoitusoikeudet, ryhmällä on lukuoikeudet ja muilla käyttäjillä ei ole mitään oikeuksia.
<img width="800" height="75" alt="Näyttökuva 2026-04-07 143353" src="https://github.com/user-attachments/assets/b22492b7-b4df-40a3-9375-f04f5e87422c" />
<img width="650" height="102" alt="Näyttökuva 2026-04-07 143505" src="https://github.com/user-attachments/assets/b64cb0c1-a9bc-4f11-ad62-120c29f294e5" />

e)  
Käytin ansiblen "lineinfile" käskyä.
Käskyllä lisäsin yhden rivin tekstiä /etc/motd tiedostoon.
<img width="626" height="123" alt="Näyttökuva 2026-04-07 145944" src="https://github.com/user-attachments/assets/48eff7a2-89d8-4639-beda-396f733d97ed" />
<img width="1105" height="220" alt="Näyttökuva 2026-04-07 145828" src="https://github.com/user-attachments/assets/c57e1ce7-6bbe-44f3-b5f3-2cbb1411ebcf" />

x)  
Sudo without password  
Luodaan käyttäjä ja ryhmä, jolle annetaan oikeus käyttää sudoa ilman salasanaa.  
Kannattaa avata root välilehti terminaalissa ennen sudo muutoksien tekoa.  
Määritykset tehdään sudo visudo /etc/sudoers.d/sudoless:iin.  
Sinne lisätään %sudoless ALL = (ALL) NOPASSWD: ALL.    
Sudo määrityksiä muokatessa pitää olla varovainen ettei pistä sudoa kokonaan solmuun.  

 
Passwordless sudo with Ansible  
Ansiblella pystyy automatisoimaan sudon ilman salasanaa.  
SSH avain mahdollistaa salasanattoman kirjautumisen  
Kannattaa tehdä manuaalisesti ensin, sitten vasta yrittää automaatiota.  
Oikeuksia kannattaa käyttää oktaalimuodossa.  
Oikeuksia ei saa arvailla, ne pitää oppia tietoturvan kannalta.  
Kuinka turvallista on antaa koko ryhmälle täydet sudo-oikeudet ilman salasanaa?    

Munroe: Sandwich  
Humoristinen sarjakuva  
Sudo saa käyttäjän tekemään mitä vain

Ansible-doc copy  
Kopioi tiedostoja tai hakemistoja käyttäjän koneelta toiseen kohdekoneeseen.  
Content: Tiedoston sisältö  
Dest: Kohdepolku  
Src: Lähdetiedosto  
Owner: Tiedoston omistaja  
Group: Ryhmä  
Mode: Oikeudet  
```
Esim:  
- name: Kopioi tiedosto omistajan ja oikeuksien kanssa
  ansible.builtin.copy:
    src: /srv/tiedosto/foo.conf
    dest: /etc/foo.conf
    owner: foo
    group: foo
    mode: "0640"
 ```  
Ansible-doc apt  
Hallitsee apt paketteja.  
Name: Paketin nimi  
State: Kertoo paketin tilan  
Update_cache: Päivittää apt-pakettivaraston  
```
Esim:  
-name: Lataa apache  
 ansible.builtin.apt: 
  name: apache2  
  state: present  
```
Ansible-doc file  
Hallitsee tiedostoja, hakemistoja ja linkkejä.
Path: Tiedoston tai hakemiston polku  
Recurse: Rekursiivisesti määritetyt tiedostot asetetaan hakemiston sisälle  
Src: Linkin lähde  
State: Tiedostojen ja hakemistojen tilat  
Owner: Omistaja  
Group: Ryhmä  
Mode: Oikeudet  
```
Esim: 
- name: Vaihda tiedoston omistaja, ryhmä ja oikeudet
  ansible.builtin.file:  
    path: /etc/foo.conf  
    owner: foo  
    group: foo  
    mode: "0640"  
```
Ansible-doc user  
Luo, muokkaa ja poistaa käyttäjiä.  
Name: Käyttäjän nimi  
Create_home: Luo kotihakemisto  
Comment: Käyttäjän kuvaus  
Groups: Lisäryhmät missä käyttäjä on  
Shell: Käyttäjän komentotulkki  
State: Käyttäjän tila  
System: Voi tehdä järjestelmäkäyttäjän  
```
Esim:  
- name: Lisätään käyttäjä kotihakemiston kanssa
  ansible.builtin.user:
    name: joku
    create_home: yes  
 ```   

Ansible-doc authorized_key  
Lisää tai poistaa SSH-avaimia käyttäjältä.  
User: Käyttäjä jonka avain tiedostoa muokataan  
Key: Julkinen SSH-avain  
```
Esim:  
- name: Asetetaan valtuutettu avain tiedostosta  
  ansible.posix.authorized_key:
    user: timo  
    state: present
    key: "{{ lookup('file', '/home/timo/.ssh/id_rsa.pub') }}"
```
# Lähteet
Ansible Community Documentation. Luettavissa: https://docs.ansible.com/projects/ansible/latest/collections/ansible/builtin/index.html. Luettu 7.4.2026  
Karvinen, Tero 2026. Sudo without password. Luettavissa: https://terokarvinen.com/passwordless-sudo/. Luettu: 7.4.2026  
Karvinen, Tero 2026. Passwordless Sudo with Ansible. Luettavissa: https://terokarvinen.com/passwordless-sudo-with-ansible/. Luettu: 7.4.2026  
Ansiblen dokumentaatio Linuxissa  
