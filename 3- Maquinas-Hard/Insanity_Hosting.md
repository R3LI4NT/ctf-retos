<p align="center">
  <a href="https://github.com/DenverCoder1/readme-typing-svg"><img src="https://readme-typing-svg.herokuapp.com?size=50&color=FF0000&width=530&height=80&lines=INSANITY_HOSTING"></a>
</p>

<h1 align="center"></h1>

**[Descargar máquina]:**

Vulnhub: https://www.vulnhub.com/entry/insanity-1,536/

<h1 align="center"></h1>

</br>

- *Paso 1:* Identificar la IP de la máquina host con Arp-Scan. 
```
arp-scan --interface wlan0 -l
```
![1](https://user-images.githubusercontent.com/75953873/177059310-4e781fd1-10e5-4204-a0e4-1cb0101ea678.png)

IP host: `192.168.1.10`

- *Paso 2:* Escanear todos los puertos que estén abiertos con Nmap. 
```
nmap -p- --open -sC -n -vvv 192.168.1.10
```
![2](https://user-images.githubusercontent.com/75953873/177059371-cdbe2b44-c0bb-47bc-843e-443e7f8e38a6.png)

Puertos abiertos: [21,22,80]

- *Paso 3:* Detección de servicios y sistema operativo. 
```
nmap -p 21,22,80 -A 192.168.1.10
```
![3](https://user-images.githubusercontent.com/75953873/177059471-f34e40d9-8d65-4731-9ea1-15efd130ca17.png)

Servidor corriendo: **HTTP Apache**

Servicio FTP: permite el inicio de sesión anónimo.

O.S: Linux (**CentOS**)

URL: `http://192.168.1.10`

- *Paso 4:* Loguearse al servicio FTP. 
```
ftp 192.168.1.10
```
Usuario: `anonymous`

Contraseña: `anonymous`

![4](https://user-images.githubusercontent.com/75953873/177059681-c67a449f-966c-4557-857a-fb6b689ee742.png)
