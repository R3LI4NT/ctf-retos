<p align="center">
  <a href="https://github.com/DenverCoder1/readme-typing-svg"><img src="https://readme-typing-svg.herokuapp.com?size=50&color=3CF700FF&width=300&height=80&lines=TOMATO_1"></a>
</p>

<h1 align="center"></h1>

**[Descargar máquina]:**

Vulnhub: https://www.vulnhub.com/entry/tomato-1,557/

</br>

- *Paso 1:* Identificar la IP de la máquina host con NetDiscover. 
```
netdiscover -i eth0
```
![1](https://user-images.githubusercontent.com/75953873/174927688-71985557-4e9d-4790-acac-a8b1da611f48.png)

IP host: `192.168.1.10`

- *Paso 2:* Escanear todos los puertos que estén abiertos con Nmap. 
```
nmap -p- --open -sC -n -vvv 192.168.1.10
```
![2](https://user-images.githubusercontent.com/75953873/174929092-202e91f9-f6d3-428b-a8f9-a952095f67f8.png)

Puertos abiertos: [21,80,2211,8888]

- *Paso 3:* Detección de servicios y sistema operativo. 
```
nmap -p 21,80,2211,8888 -A 192.168.1.10
```
![3](https://user-images.githubusercontent.com/75953873/174928628-0721689f-2a13-42e2-992f-1356fa68f168.png)

Servidor corriendo: **HTTP Apache**

O.S: **Linux**

URL del servidor: `http://192.168.1.10`

![4](https://user-images.githubusercontent.com/75953873/174928906-0bf0a1e9-d580-4d8f-ae94-0c0bbb3a73b6.png)
