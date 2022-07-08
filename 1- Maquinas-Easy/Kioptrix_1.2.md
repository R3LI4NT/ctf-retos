<p align="center">
  <a href="https://github.com/DenverCoder1/readme-typing-svg"><img src="https://readme-typing-svg.herokuapp.com?size=50&color=F7F400&width=390&height=80&lines=KIOPTRIX_1.2"></a>
</p>

<h1 align="center"></h1>

**[Descargar máquina]:**

Vulnhub: https://www.vulnhub.com/entry/kioptrix-level-12-3,24/

<h1 align="center"></h1>

</br>

- *Paso 1:* Identificar la IP de la máquina host con Arp-Scan. 
```
arp-scan --interface wlan0 -l
```
![1](https://user-images.githubusercontent.com/75953873/177891939-07f2e077-4b7a-4f04-9e6f-80c2e43d1a13.png)

IP host: `192.168.1.4`

- *Paso 2:* Escanear todos los puertos que estén abiertos con Nmap. 
```
nmap -p- --open -sC -n -vvv 192.168.1.4
```
![2](https://user-images.githubusercontent.com/75953873/177892039-39832af6-5bbd-4ba1-9581-85abf27bffa0.png)

Puertos abiertos: [22,80]

- *Paso 3:* Detección de servicios y sistema operativo. 
```
nmap -p 22,80 -A 192.168.1.4
```
![3](https://user-images.githubusercontent.com/75953873/177892640-8cd728ec-bbdd-4f6c-a2ec-2d1a55a17fa4.png)

Servidor corriendo: **HTTP Apache**

O.S: **Linux**

URL: `http://192.168.1.4`
