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
