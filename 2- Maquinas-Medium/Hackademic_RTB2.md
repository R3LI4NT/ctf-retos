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


