# h4 Pizza Fantasia

a)  
Valitsin demoniksi postgresql.  
Päivitin ensin pakettilistan **sudo apt-get update komennolla**.    
Sitten latasin itse demonin, **sudo apt-get -y install postgresql** komennolla.  
Latauksen jälkeen tarkistin että demoni on käynnissä **systemctl status postgresql** komennolla.  
<img width="1183" height="96" alt="Näyttökuva 2026-04-20 101743" src="https://github.com/user-attachments/assets/9d7c1d63-d2e7-4b41-996d-661df54d7a3d" />  
Kokeilin vielä että pääsen käsiksi postgressiin **sudo -u postgres psql** komennolla.  
<img width="685" height="127" alt="Näyttökuva 2026-04-20 103306" src="https://github.com/user-attachments/assets/9d7f05ff-66e8-4fef-b14f-8c233867b35d" />
Tein testitietokannan **sudo -u postgres createdb testi** komennolla ja tarkistin tuliko se näkyviin tietokantalistaan **sudo -u postgres psql -c ”\l”** komennolla.  
<img width="1212" height="432" alt="Näyttökuva 2026-04-20 103817" src="https://github.com/user-attachments/assets/c227bd13-7bed-464c-a697-ff76ceb7d795" />  
Testitietokanta näkyy listassa viimeisenä.  

b)  
Tein postgresql roolit:
````
mkdir -p roles/postgresql/tasks
mkdir -p roles/postgresql/handlers
mkdir -p roles/postgresql/files
````
Tein **micro roles/postgresql/tasks/main.yml** jonne lisäsin apt ja servicen.  
<img width="366" height="274" alt="Näyttökuva 2026-04-20 110523" src="https://github.com/user-attachments/assets/1d8cbce5-2789-4696-b8a1-64eb58029067" />  
Eli **apt** asentaa demonin ja **service** käynnistää sen.  
Sitten tein handlerin, **micro roles/postgresql/handlers/main.yml**:  
<img width="438" height="163" alt="Näyttökuva 2026-04-20 111255" src="https://github.com/user-attachments/assets/3fbc1eeb-6e3b-428b-b809-897f65cde1d1" />
Lisäsin roolin site.yml:ään:  
<img width="406" height="213" alt="Näyttökuva 2026-04-20 112723" src="https://github.com/user-attachments/assets/85a15fa2-2f41-47f7-8d91-d09c40a937ca" />  
Ajoin playbookin jotta näkisin tuliko muutoksia tai epäonnistuiko jokin:  
<img width="1183" height="116" alt="Näyttökuva 2026-04-20 113032" src="https://github.com/user-attachments/assets/55905ed3-fa2b-4936-8c65-bfef4c2924eb" />  
Kokeilin vielä uudestaan **systemctl status postgresql** komennolla että palvelu toimii:  
<img width="1357" height="98" alt="Näyttökuva 2026-04-20 113308" src="https://github.com/user-attachments/assets/1a645797-c848-48b3-8409-0e5b730b2a7a" />  

c)  
Ensiksi etsin oikean konfiguraatiotiedoston.  
Etsin sen menemällä **/etc/postgresql** ja käyttämällä **ls** komentoa, kunnes löysin **/etc/postgresql/17/main/postgresql.conf**.  
Kopioin **/etc/postgresql/17/main/postgresql.conf** omaan **/postgresql/files** tiedostoon, **sudo cp /etc/postgresql/17/main/postgresql.conf ~/ansible/roles/postgresql/files/** komennolla.  
Muokkasin konfiguraatiotiedostoa **micro roles/postgresql/files/postgresql.conf**, muuttamalla sieltä vain **listen_adresses**.  
Oletuksena **listen_adresses** on "listen_addresses = localhost", mutta muutin sen "listen_addresses = '*'".  
Eli nyt postgresql kuuntelee kaikkia IP-osoitteita, ei pelkästään localhostin.  
<img width="1008" height="102" alt="Näyttökuva 2026-04-20 115452" src="https://github.com/user-attachments/assets/911cde90-4635-487d-963f-932f72092039" />  
Lisäsin sitten copyn **micro roles/postgresql/tasks/main.yml**:ään.  
<img width="792" height="479" alt="Näyttökuva 2026-04-20 120442" src="https://github.com/user-attachments/assets/74ec4bdc-b648-4a57-ae50-6730390d3726" />
Tarkistin playbookilla että muutokset tulivat voimaan:  
<img width="1331" height="111" alt="Näyttökuva 2026-04-20 120749" src="https://github.com/user-attachments/assets/1c3fc5c6-0081-406d-9cac-b280f4fe8a50" />
Tarkistin myös **grep** komennolla että muutos tuli käyttöön:  
<img width="1291" height="49" alt="Näyttökuva 2026-04-20 120935" src="https://github.com/user-attachments/assets/fcd9f263-18f2-459a-82f3-7ebafd298237" />
Jälleen kerran tarkistin palvelun statuksen **systemctl status postgresql**:  
<img width="1348" height="106" alt="Näyttökuva 2026-04-20 121150" src="https://github.com/user-attachments/assets/e3fb56cc-80a9-4952-9296-e9c0aeeef3b7" />  

d) 
Poistin postgresql **sudo apt-get purge postgresql -y** komennolla:  
<img width="1091" height="319" alt="Näyttökuva 2026-04-20 122336" src="https://github.com/user-attachments/assets/9fa25263-0145-4d92-9316-c389798fb74a" />  
Tarkistin sitten postgressin statuksen, **systemctl status postgresql**:  
<img width="769" height="55" alt="Näyttökuva 2026-04-20 123941" src="https://github.com/user-attachments/assets/f2b3083b-c225-4c4f-a5fd-4a3186792e3d" />  
Postgresql:ää ei löytynyt enää, ajoin playbookin jotta se korjaisi tilanteen, ja saisin postgressin takaisin.  
<img width="1334" height="113" alt="Näyttökuva 2026-04-20 124317" src="https://github.com/user-attachments/assets/ca7a6fc4-1c93-4fde-967c-2359b1497ae3" />  
Tarkistin sitten statuksen uudestaan jotta näkisin sainko postgressin takaisin, vai en:  
<img width="1368" height="229" alt="Näyttökuva 2026-04-20 124526" src="https://github.com/user-attachments/assets/c59e6516-b37b-48ee-9f2d-b34b1b084b34" />  
Tarkistin myös että muuttamani konfiguraatio on voimassa **sudo -u postgres psql -c "SHOW listen_addresses;"** komennolla.  
Normaalisti näkyisi "localhost", mutta nyt näkyy muuttamani "*" merkki.  
<img width="1101" height="121" alt="Näyttökuva 2026-04-20 171914" src="https://github.com/user-attachments/assets/bdd2b697-7213-4ec2-baca-44a6eb8d415f" />  

e)  
Ajoin playbookin uudestaan ja nyt kaikki oli ok, mikään ei ollut changed eikä failed:  
<img width="1331" height="105" alt="Näyttökuva 2026-04-20 125315" src="https://github.com/user-attachments/assets/a7998ca1-4928-40ce-8c71-c8718456b5ee" />  

x)  
4.12.1 Size and Complexity of Some DSLs:  
DSL-kielet voivat olla hyvin laajoja ja monimutkaisia.  
Salt: 510 funktiota ja dokumentaatio on yli 20000 riviä.  
Salt käyttää Jinja2 mallia luodakseen YAML koodia, joka sitten muutetaan pythoniksi.  
Puppet: 113 funktiota ja kontrollirakenteet eroavat yleisistä ohjelmistokielistä.  
Puppet käyttää omia konsepteja kontrollirakenteissa.  
Ovatko näin suuret DSL:t oikeasti hyödyllisiä vai ovatko ne vain turhan monimutkaisia?  

4.12.2 Use of DSL Functions in Case Configuration:  
Funktioita on paljon, mutta vain pieni osa on kovassa käytössä.  
Yleisimmät ovat: package-file-service, exec, group ja augeas.  
Idempotenssi jää käyttäjän vastuulle jos käyttää exec:iä.  
Kontrollirakenteissa käytetään "if" ja "case".  
Onko DSL:issä mitään ns. turhia funktioita, vai ovatko kaikki silti edes jotenkin hyödyllisiä?  

4.12.3.1 Dependencies Between Main Functions:  
Tärkeimmät funktiot:  
Demoneja varten package-file-service.  
Sovelluksia varten package ja file.  
Käyttäjän hallinnointia varten user ja group.  
Tiedostojen manipulointia varten file, directory ja symlink.  
File ja exec ovat tärkeimmät funktiot, joiden avulla muut funktiot tehdään.  
Järjestelmän pitäisi olla idempotentti, eli muutoksia tehdään vain jos järjestelmässä on jokin väärin.  
Kuinka pitkälle pääsee käyttämällä vain perusfunktioita, ilman että rakentaa uusia abstraktioita? 


## Lähteet
Hostman Team. 2025. Installing PostgreSQL on Debian. Luettavissa: https://hostman.com/tutorials/installing-postgresql-on-debian/. Luettu: 20.4.2026.  
Karvinen, T. 2016. Install PostgreSQL on Ubuntu - New user and database in 3 commands. Luettavissa: https://terokarvinen.com/2016/install-postgresql-on-ubuntu-new-user-and-database-in-3-commands/index.html. Luettu: 20.4.2026  
Karvinen, T. 2026. Apache installed with Ansible - quick notes. Luettavissa: https://terokarvinen.com/apache-ansible/. Luettu: 20.4.2026  
Karvinen, T. 2023. Configuration Management of Distributed Systems over Unreliable and Hostile Networks. Sivut 112-117. Luettavissa: https://westminsterresearch.westminster.ac.uk/download/4cc417566aa9af60fe3826d690719e390abdb7a3c8672f3d51b1eb4ca75e7624/1427236/karvinen-2023-configuration-management-of-distributed-systems.pdf. Luettu: 20.4.2026    
Kartones. s.a. PostgreSQL command line cheatsheet. Luettavissa: https://gist.github.com/Kartones/dd3ff5ec5ea238d4c546. Luettu: 20.4.2026
Postgresql man ja help sivut Linuxissa.
