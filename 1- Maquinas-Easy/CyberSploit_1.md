<p align="center">
  <a href="https://github.com/DenverCoder1/readme-typing-svg"><img src="https://readme-typing-svg.herokuapp.com?size=50&color=F7F400&width=480&height=80&lines=CYBERSPLOIT_1"></a>
</p>

<h1 align="center"></h1>

**[Descargar máquina]:**

Vulnhub: https://www.vulnhub.com/entry/cybersploit-1,506/


<h1 align="center"><img src="https://user-images.githubusercontent.com/75953873/174417901-a2431e6b-3849-46e3-a0e4-ed3f8ed73e85.png"></h1>

</br>

- *Paso 1:* Identificar la IP de la máquina host con NetDiscover. 
```
netdiscover -i wlan0 -r 192.168.1/24
```
![1](https://user-images.githubusercontent.com/75953873/174458235-8b46f051-22c5-4c9e-a193-a21d2b15f82a.png)

IP host: `192.168.1.5`

- *Paso 2:* Escanear todos los puertos que estén abiertos con Nmap. 
```
nmap -p- --open -sC -n -vvv 192.168.1.5
```
![2](https://user-images.githubusercontent.com/75953873/174458274-1cbb9500-5deb-43d7-a58c-1fa3ba579cc9.png)

Puertos abiertos: [22,80]

- *Paso 3:* Detección de servicios y sistema operativo. 
```
nmap -p 22,80 -A 192.168.1.5
```
![3](https://user-images.githubusercontent.com/75953873/174458453-68bb619f-8c2c-4657-a337-ae7bdbdb0fd3.png)

Servidor corriendo: **HTTP APACHE**
