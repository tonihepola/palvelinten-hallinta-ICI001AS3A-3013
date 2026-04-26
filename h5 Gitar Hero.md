### a) Online 	
Aloitin menemällä Githubiin, ja luomalla uuden repositoryn, painamalla oikeasta ylänurkasta   
`````  
+  
New repository  
`````
<img width="260" height="46" alt="Näyttökuva 2026-04-25 093057" src="https://github.com/user-attachments/assets/8459eb08-fec6-4308-8d7d-20a43764110e" />  
Lisäsin repositorylle nimen ja kuvauksen, joissa kummassakin oli vaadittu sana ”Sunshine”.  
Repository on oletuksena public, joten jätinkin sen niin.  
Laitoin vielä README:n päälle ja lisäsin GNU General Public License 3.  
Repository luotiin ”Create repository” kuvakkeesta.  
<img width="1038" height="850" alt="Näyttökuva 2026-04-25 093249" src="https://github.com/user-attachments/assets/81995173-e5ed-4bb3-be60-b983da31e1c5" />  


### b) Dolly 
Aloitin repositoryn kloonaamisen painamalla vihreää "Code" kuvaketta, valitsemalla sieltä "SSH" osion ja kopioimalla näkyvän tekstin.  
<img width="522" height="338" alt="Näyttökuva 2026-04-26 161448" src="https://github.com/user-attachments/assets/1a72ff8a-51f6-4c18-a567-a961a4d2c859" />  
Kloonasin repositoryn koneelleni komennolla "**git clone git@github.com:Donhebloi/Sunshine-varasto.git**".  
<img width="1186" height="168" alt="Näyttökuva 2026-04-26 162031" src="https://github.com/user-attachments/assets/11036ef0-ae89-4239-b669-d32821b3966d" />  
Siirryin "**cd**" komennolla Sunshine-varastoon ja lisäsin sinne tekstitiedoston "**micro aurinko.txt**".  
<img width="875" height="164" alt="Näyttökuva 2026-04-26 163007" src="https://github.com/user-attachments/assets/4b67de26-f4b0-4952-8a30-45476b920656" />  
Aloitin muutosten lisäämisen webpalvelimelle "**git add --all**" komennolla.   
Tallensin muutokset "**git commit**" komennolla.  
Lisäsin commit kommentiksi "Uusi tekstitiedosto varastoon".  
Sitten käytin vielä "**git push**" komentoa, että muutokset tulisivat webbiin näkyviin.  
<img width="915" height="309" alt="Näyttökuva 2026-04-26 163704" src="https://github.com/user-attachments/assets/8f8fa9a1-8e78-4aa8-8275-aa027f6abb4a" />  
Kävin vielä githubissa tarkistamassa että tulihan muutokset näkyville:  
<img width="1236" height="447" alt="Näyttökuva 2026-04-26 164247" src="https://github.com/user-attachments/assets/49602ee2-1497-4077-b658-c49eba15a73f" />  
<img width="559" height="242" alt="Näyttökuva 2026-04-26 164402" src="https://github.com/user-attachments/assets/e7803a13-5ce6-4a4d-bc43-477e38a6b6c8" />
Uusi tekstitiedosto ja sen sisältämä teksti näkyvät selaimessa niin kuin pitääkin.  


### c) Doh! 
Aloitin muokkaamalla "**aurinko.txt**" tiedostoa, lisäämällä sinne kaksi tekstiriviä.  
Aloitin muutosten lisäämistä "**git add --all**" komennolla, mutta en commitannut, enkä pushannut mitään.  
Palautin tekstitiedostoni viimeisempään tallennettuun tilaan, "**git reset --hard**" komennolla.  
Tarkistin vielä "**cat**" komennolla että muutokset poistuivat.  
<img width="871" height="361" alt="Näyttökuva 2026-04-26 165313" src="https://github.com/user-attachments/assets/daeace49-4fa4-4786-8d80-35a348d68070" />  


### d) Tukki  
Repositoryn lokeja pystyy tarkastelemaan "**git log --patch**" komennolla.  
Komento näyttää commit-historian, tarkat tiedostokohtaiset muutokset, kuka on tehnyt muutokset ja milloin.  
<img width="1319" height="869" alt="Näyttökuva 2026-04-26 170444" src="https://github.com/user-attachments/assets/e7d49a16-3b5b-4b87-9aa3-57968983f764" />  
Lokitiedoista näkee:  
````
Mikä commit  
Author, eli tekijä  
Päivämäärän, milloin commit suoritettu  
Commitin kommentti  
Mitä commit sisältää  
Tässä tapauksessa kaksi tekstiriviä, "Paistaako aurinko?" ja "Paistaa niin että soi!"
````
Nimeni ja sähköpostiosoite näkyvät oikein, mutta jos haluaisin muuttaa niitä, niin voisin tehdä sen komennoilla:  
````
git config --global user.name "Nimi"
git config --global user.email "sähköposti@email.com"
````


### e) Gitanbile  
Kopioin ansible hakemistoni Sunshine-varastoon "**cp -r ~/ansible** ." komennolla.  
Tarkistin "**ls**" komennolla että hakemisto oli nyt kopioituna.  
Sitten lisäsin sen gittiin:  
````
git add --all
git commit ja kommentti "Lisätään ansible-kansio varastoon"
git push
````
<img width="994" height="648" alt="Näyttökuva 2026-04-26 173940" src="https://github.com/user-attachments/assets/b2d70ec2-9f2f-408c-a9a6-03a17702d05c" />  
Kävin githubissa tarkistamassa että tuliko kansio sinne näkyviin:  
<img width="1218" height="109" alt="Näyttökuva 2026-04-26 174626" src="https://github.com/user-attachments/assets/b8af6ea7-62c1-466f-a39e-34bc7e9e7842" />  
Tämän jälkeen kävin muokkaamassa vähäsen "Hello" roolia ansiblessa, lisäämällä sinne viestin.  

```
micro ansible/roles/hello/tasks/main.yml  
- name: Hello message  
  debug:  
    msg: Morjensta, morjensta  
```
<img width="496" height="88" alt="Näyttökuva 2026-04-26 180143" src="https://github.com/user-attachments/assets/8e75fa6b-4588-406e-8e69-ceb46ded0f43" />  
Muokkauksen jälkeen ajoin playbookin, "ansible-playbook site.yml -K"  
<img width="1709" height="98" alt="Näyttökuva 2026-04-26 180320" src="https://github.com/user-attachments/assets/a3b58825-ded2-4d46-8450-47fac68eb678" />  
Huomataan että playbook meni läpi, ja muutokset tulivat voimaan.  
Lisäsin sitten muutoksen gittiin:  

```
git add --all
git commit ja kommentti "Hello roolin muokkaus"
git push
```
<img width="1035" height="314" alt="Näyttökuva 2026-04-26 180514" src="https://github.com/user-attachments/assets/6acbf879-76ac-473e-81f7-aa8c25cda82a" />  
Kävin sitten githubissa tarkistamassa tuliko muutokset näkyviin:  
<img width="1197" height="107" alt="Näyttökuva 2026-04-26 181525" src="https://github.com/user-attachments/assets/b2133272-523b-4189-b352-558f34ed1fc2" />  
Etusivuilta heti näkyy että muutos onnistui, milloin muutos on tehty ja commitin kommentti.  
Kävin vielä kansion sisällä tarkistamassa sisällön:  
<img width="668" height="350" alt="Näyttökuva 2026-04-26 181557" src="https://github.com/user-attachments/assets/6e753d43-698c-4837-bbad-5ac5c36cb771" />  
Nähdään että Hello roolin lievä muokkaaminen onnistui.  


### f) Pari projektiin  
Pari projektiin on löytynyt.  

## Huom! Tehtävässä virhe
Huolimattomasti laitoin commit kommentit suomeksi, kun ne olisi pitänyt olla englanniksi.  
Virhe tajuttu vasta sen jälkeen kun tehtävä ja raportti olivat valmiita, mutta nyt on huomioitu tulevaisuutta varten.  

### x) Tiivistelmä  
Pro Git, 2ed:  
Git tallentaa tiedot snapshotteina, eli periaatteessa kuvina.  
Git toimii suurimmaksi osaksi paikallisesti, joka tekee siitä nopeamman ja mahdollistaa työskentelyn ilman nettiä.  
Git käyttää SHA-1 hashia, joka tekee siitä eheän.  
Gitin snapshottien takia, dataa on todella hankalaa menettää.  
Gitissä on kolme tilaa:  
````
Modified eli muokattu mutta ei vielä commitattu
Staged eli valittu committiin
Committed eli data on tallennettuna paikalliseen tietokantaan
````

Git komennot:  
git add --all, lisätään kaikki muutokset committia varten.  
git commit, tallentaa muutokset pysyvästi tietokantaan.  
git pull, etsii muutoksia ja yhdistää ne.  
git push, tekee muutokset.  


## Lähteet
Atlassian. s.a. Git Glossary. Luettavissa: https://www.atlassian.com/git/glossary#commands. Luettu 26.4.2026.  
Käytetty lähteenä komentoihin, komentojen selityksiin ja tiivistelmään.   
Atlassian. s.a. Git cheat sheet. Luettavissa: https://www.atlassian.com/git/tutorials/atlassian-git-cheatsheet. Luettu: 26.4.2026.  
Käytetty lähteenä komentoihin, komentojen selityksiin ja tiivistelmään.   
Chacon, S. Straub, B. 2014. Pro Git 2nd Edition. Apross. New York City. Luku 1.3. Luettavissa: https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F. Luettu: 26.4.2016.  
Käytetty lähteenä tiivistelmään.  

