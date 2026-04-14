a)  
Päivitin eka järjestelmän **sudo apt-get update** komennolla, jonka jälkeen latasin apache2 **sudo apt-get install apache2** komennolla.  
Tein webbi sivua varten oman hakemiston, **mkdir -p /home/toni/sivu** ja tiedoston **micro /home/toni/sivu/index.html**, jonne kirjoitin vain:  
```
<h1>Toimiiko, toimiiko</h1>
```
Annoin oikeudet käyttäjille komennoilla:  
```
chmod ugo+x /home/toni/
chmod ugo+x /home/toni/sivu/
chmod ugo+r /home/toni/sivu/index.html
```
Konfiguroin apachea sudo micro **/etc/apache2/sites-available/example.com.conf.** Tänne lisäsin oman sivun tiedot. 
Tein symbolisen linkin **sites-available** ja **sites-enabled** välille:  
````
sudo ln -s /etc/apache2/sites-available/example.com.conf /etc/apache2/sites-enabled/example.com.conf
````
Kokeilin konfiguraatiotani **sudo apache2ctl configtest** komennolla jonka jälkeen tulostui "Syntax OK"  
<img width="770" height="92" alt="Näyttökuva 2026-04-11 151713" src="https://github.com/user-attachments/assets/e9ecd2af-7252-43d0-9006-550e127db06a" />  
Käynnistin apachen kokonaan uudelleen, **sudo systemctl stop apache2, sudo systemctl enable apache2** ja **systemctl restart apache2**.    
En ole ihan varma oliko tuo turhaan, että olisiko tämä toiminut pelkästään **systemctl restart apache2** komennolla.    
Tämän jälkeen kokeilin sivuni toimivuutta, "http://localhost"  
<img width="774" height="448" alt="Näyttökuva 2026-04-11 142244" src="https://github.com/user-attachments/assets/c3089a57-9877-44d1-bc5a-b79f420573e4" />

b)  
Aloitin sammuttamalla apachen, **sudo systemctl stop apache2** komennolla.  
Latasin nginx samalla tavalla kuin apachen, eli ekaksi päivitin järjestelmän **sudo apt-get update** ja sen jälkeen **sudo apt-get install nginx**.  
En tehnyt uutta käyttäjäsivua, vaan käytin samaa **/home/toni/sivu**, mutta muokkasin vähän **micro /home/toni/sivu/index.html** kirjoittamalla sinne "Toimiiko, nginx"  
Muokkasin nginx:n konfigurointia **sudo micro /etc/nginx/sites-available/default**.  
Vaihdoin sieltä **root /var/www/html;** tähän, **root /home/toni/sivu;**.  
Laitoin samat oikeudet niin kuin apachessa, eli: 
````
chmod ugo+x /home/toni
chmod ugo+x /home/toni/sivu
chmod ugo+r /home/toni/sivu/index.html
`````
Kokeilin konfiguraatiota **sudo nginx -t komennolla**:  
<img width="994" height="74" alt="Näyttökuva 2026-04-11 151358" src="https://github.com/user-attachments/assets/12bdd7a3-8d67-40de-89e9-4740933b8ff5" />  
Tämän jälkeen tein saman kuin apachen kanssa, eli käynnistin nginx kokonaan alusta, **sudo systemctl stop nginx, sudo systemctl enable nginx** ja **sudo systemctl restart nginx**.  
Kokeilin toimiiko nginx, "http://localhost".  
<img width="808" height="475" alt="Näyttökuva 2026-04-11 150206" src="https://github.com/user-attachments/assets/f6119d0f-7462-4c6c-aa0a-9b1f1c71a472" />  

c)  
Loin nginx roolit:
````
mkdir -p roles/nginx/tasks
mkdir -p roles/nginx/handlers
mkdir -p roles/nginx/files
````
Tein roles/nginx/tasks/main.yml sisällön:  
<img width="600" height="337" alt="Näyttökuva 2026-04-12 134612" src="https://github.com/user-attachments/assets/b1cb812b-d610-4782-bfce-d887f7b8b7c7" />  
Tein roles/nginx/handlers/main.yml sisällön:   
<img width="410" height="159" alt="image" src="https://github.com/user-attachments/assets/5b6c2471-99ea-4fad-ba8e-ec1905fca2b1" />  
Tein roles/nginx/files/default sisällön. Kopioin omaa tiedostoa varten **/etc/nginx/sites-available/default** tiedostosta konfiguraation mutta muutin siitä rootin.   
Aikaisemmin se oli **root /var/www/html;**, mutta muutin sen **root /home/toni/sivu;**.  
<img width="598" height="344" alt="Näyttökuva 2026-04-12 135314" src="https://github.com/user-attachments/assets/dec408ce-bc2e-49ec-a69f-80443b9f650d" />  
Tämän jälkeen lisäsin vielä nginx roolin site.yml:ään.  
Ajoin playbookin jotta näkisin että onko virheitä tai onko mikään muuttunut:   
<img width="1472" height="123" alt="Näyttökuva 2026-04-12 132441" src="https://github.com/user-attachments/assets/5174a0b9-55de-4ec5-af7f-3ee47897c645" />  
Kokeilin sitten sivuani **http://localhost**, sivu avautui niin kuin pitikin ja oma "Toimiiko, nginx" teksti näkyi siellä. Refreshasin sivun vielä useampaan otteeseen varmuuden vuoksi.  
Ajoin vielä kerran playbookin varmistaakseni että kaikki toimii: 
<img width="1476" height="113" alt="Näyttökuva 2026-04-12 132533" src="https://github.com/user-attachments/assets/17d97b28-d237-4b14-922c-175bb8d28165" />  

x)
Apache installed with Ansible:  
Apache ladataan sudo apt-get install apache2 komennolla
Apache otetaan käyttöön package-file-service mallin mukaisesti.  
Ensin asennetaan, sitten muokataan konfiguraatiotiedostoja, sitten käynnistetään palvelu.  
Palvelu pitää käynnistää uudelleen, jotta konfiguraatio muutokset alkaisivat toimimaan.  
Roolirakenne on tasks, handlers, files.  
Onko mahdollista suorittaa ilman handleria?  

Handlers: running operations on change:  
Handlerit suoritetaan vain, jos jokin tehtävä tekee muutoksen.  
Vähentää turhia toimenpiteitä.  
**Notify** kutsuu handleria.  
Yksi tehtävä voi kutsua useampaa handleria.  
Handleri suoritetaan vain kerran, vaikka sitä kutsuttaisiin monta kertaa.  
Handlerien suoritusjärjestys määräytyy handlers osiossa, eikä notify osiossa.  
Milloin handleria kannattaa käyttää ja milloin ei? 

Ansible-doc service:  
Hallitsee palveluita.  
Toimii eri järjestelmissä.  
Enabled:  
Käynnistyykö palvelu automaattisesti bootissa vai ei  
Arvot: True/false  
Name: Palvelun nimi  
State: Kertoo palvelun tilasta.  
Started: Käynnissä  
Stopped: Pysäytetty  
Restarted: Käynnistää uudelleen  
Reloaded: Lataa uudelleen  
Esim:
````
- name: Start service httpd, if not started
  ansible.builtin.service:
    name: httpd
    state: started
````
Service moduulilla voi optimoida omaa palvelua.
