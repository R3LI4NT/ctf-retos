<p align="center">
  <a href="https://github.com/DenverCoder1/readme-typing-svg"><img src="https://readme-typing-svg.herokuapp.com?size=50&color=F7F400&width=300&height=80&lines=ANDROID_4"></a>
</p>

<h1 align="center"></h1>

**[Descargar máquina]:**

Vulnhub: https://www.vulnhub.com/entry/android4-1,233/

<h1 align="center"><img src="https://user-images.githubusercontent.com/75953873/179633430-0029a8f7-b789-49a2-80be-12f04ed9357f.png"></h1>

</br>

- *Paso 1:* Identificar la IP de la máquina host con ArpScan. 
```
arp-scan --interface eth0 -l
```
![2](https://user-images.githubusercontent.com/75953873/179633673-54c343f6-fe1c-49bd-a070-a2ccdb4cf488.png)

IP host: `192.168.25.139`

- *Paso 2:* Escanear todos los puertos que estén abiertos con Nmap. 
```
nmap -p- --open -sC -n -vvv 192.168.25.139
```
![3](https://user-images.githubusercontent.com/75953873/179633819-76e89cc3-3e47-4f1c-9d4c-bcd153f748b9.png)

Puertos abiertos: [8080,22000,5555]

- *Paso 3:* Detección de servicios y sistema operativo. 
```
nmap -p 8080,22000,5555 -A 192.168.25.139
```
![4](https://user-images.githubusercontent.com/75953873/179634411-2134bb33-54f8-45c7-a0be-b6dbb9824153.png)

Servidor web (puerto **8080**): `http://192.168.25.139:8080`

![5](https://user-images.githubusercontent.com/75953873/179634788-bc82e682-c166-43c9-bd67-366001b12fd5.png)

Servicio vulnerable (puerto **22000**): `Dropbear`

O.S: `Android` **--> Kernel Linux**
