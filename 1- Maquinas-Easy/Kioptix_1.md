<p align="center">
  <a href="https://github.com/DenverCoder1/readme-typing-svg"><img src="https://readme-typing-svg.herokuapp.com?size=50&color=F7F400&width=320&height=80&lines=KIOPTRIX_1"></a>
</p>

<h1 align="center"></h1>

**[Descargar máquina]:**

Vulnhub: https://www.vulnhub.com/entry/kioptrix-level-1-1,22/

<h1 align="center"></h1>

</br>

- *Paso 1:* Identificar la IP de la máquina host con Arp-Scan. 
```
arp-scan --interface wlan0 -l
```
![1](https://user-images.githubusercontent.com/75953873/177676522-7542cd60-297b-4537-a657-a6e613e22122.png)

IP host: `192.168.1.104`

- *Paso 2:* Escanear todos los puertos que estén abiertos con Nmap. 
```
nmap -p- --open -sC -n -vvv 192.168.1.104
```
![2](https://user-images.githubusercontent.com/75953873/177677054-4379065b-7b00-4c1a-a2b7-63688488f52e.png)

Puertos abiertos: [22,80,111,139,443]

- *Paso 3:* Detección de servicios y sistema operativo. 
```
nmap -p 21,22,80 -A 192.168.1.104
```
