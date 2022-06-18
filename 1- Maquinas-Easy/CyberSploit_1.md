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

- *Paso 4:* Enumeración: detección de archivos web con Dirb. 
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
