<p align="center">
  <a href="https://github.com/DenverCoder1/readme-typing-svg"><img src="https://readme-typing-svg.herokuapp.com?size=50&color=FF0000&width=200&height=70&lines=Prime_1"></a>
</p>

<h1 align="center"></h1>

**[Descargar máquina]:**

Vulnhub: https://www.vulnhub.com/entry/prime-1,358/

</br>

> Esta máquina está diseñada para aquellos que intentan prepararse para el examen OSCP. 

<h1 align="center"><img src="https://user-images.githubusercontent.com/75953873/173474426-a673d820-8b68-40c9-89f6-4686e436978f.png"></h1>

- *Paso 1:* Identificar la IP de la máquina host con NetDiscover. 
```
netdiscover -i eth0
```
![2](https://user-images.githubusercontent.com/75953873/173475187-1682b0c5-0c7e-410c-9455-98e8cd6c5e81.png)

IP host: `192.168.25.133`

- *Paso 2:* Escanear todos los puertos que estén abiertos con Nmap. 
```
nmap -p- --open -sC -n -Pn -vvv 192.168.25.133
```
![3](https://user-images.githubusercontent.com/75953873/173475468-fee78430-41f0-4a6f-a18d-5934250a6aac.png)

Puertos abiertos: [22,80]

- *Paso 3:* Escaneo agresivo para detectar servicios corriendo.
```
nmap -A 192.168.25.133
```
![4](https://user-images.githubusercontent.com/75953873/173476100-ae65ae3d-4a36-466c-aa98-fbc4fee2c738.png)

Servidor corriendo: **Apache**
