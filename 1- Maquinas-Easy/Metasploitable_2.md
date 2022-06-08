<p align="center">
  <a href="https://github.com/DenverCoder1/readme-typing-svg"><img src="https://readme-typing-svg.herokuapp.com?size=50&color=F70000&width=500&height=70&lines=Metasploitable_2"></a>
</p>

<h1 align="center"></h1>

**[Descargar máquina]:**

Vulnhub: https://www.vulnhub.com/entry/metasploitable-2,29/

Sourceforge: https://sourceforge.net/projects/metasploitable/files/Metasploitable2/

**[Online]:**

Root-Me: https://www.root-me.org/fr/Capture-The-Flag/CTF-all-the-day/Metasploitable-2-13?lang=en

<h1 align="center"></h1>

</br>

- *Paso 1:* Escanear todos los puertos que están abiertos con Nmap. 
```
nmap -p- --open -sC -n -Pn -vvv ctf04.root-me.org
```
![1](https://user-images.githubusercontent.com/75953873/172515652-41a49316-c195-462f-a88b-bfba74051bf2.png)

Puertos abiertos: [21,22,23,25,53,80,110,139,445,3306,5900]

- *Paso 2:* Detección de servicios y su respectiva versión. 
```
nmap -p 21,22,23,25,53,80,110,139,445,3306,5900 -sV ctf04.root-me.org
```
![2](https://user-images.githubusercontent.com/75953873/172518304-45323ab6-0e48-425d-9bf4-5e3689b86200.png)

Objetivo: Puerto 80 -> Servicio FTP -> Versión -> vsFTPd 2.3.4

- *Paso 3:* Identificación de exploit y descarga. 
```
searchsploit vsFTPd 2.3.4
```
![3](https://user-images.githubusercontent.com/75953873/172518879-12b95d54-5dac-4f0d-918e-96860c1c5eed.png)

`Dato:` cada exploit esta enumerado y es irrepetible.

Exploit: 49757
