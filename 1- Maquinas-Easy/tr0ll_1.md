<p align="center">
  <a href="https://github.com/DenverCoder1/readme-typing-svg"><img src="https://readme-typing-svg.herokuapp.com?size=50&color=F7F400&width=200&height=80&lines=TR0LL_1"></a>
</p>

<h1 align="center"></h1>

**[Descargar máquina]:**

Vulnhub: https://www.vulnhub.com/entry/tr0ll-1,100/

</br>

- *Paso 1:* Identificar la IP de la máquina host con NetDiscover. 
```
netdiscover -i wlan0 -r 192.168.1/24
```
![1](https://user-images.githubusercontent.com/75953873/176079905-f35a37e9-416f-45a8-8f7e-3c49899c7252.png)

IP host: `192.168.1.4`

- *Paso 2:* Escanear todos los puertos que estén abiertos con Nmap. 
```
nmap -p- --open -sC -n -vvv 192.168.1.4
```
![2](https://user-images.githubusercontent.com/75953873/176080128-62ec0641-3cfa-479f-8d07-737fc130d1aa.png)

Puertos abiertos: [21,22,80]

- *Paso 3:* Detección de servicios y sistema operativo. 
```
nmap -p 21,22,80 -A 192.168.1.4
```
![3](https://user-images.githubusercontent.com/75953873/176081118-60dbaddd-22c5-48c2-9232-a18565c084e1.png)

Servidor corriendo: **HTTP Apache**

Servicio FTP: permite el inicio se sesión anónimo.

O.S: **Linux**

URL: `http://192.168.1.4`

![4](https://user-images.githubusercontent.com/75953873/176081949-b1bb16cd-4a6f-4c5a-9abf-136aa5cc5c53.png)

- *Paso 4:* Loguearse al servicio FTP. 
```
ftp 192.168.1.4
```
Usuario: `anonymous`

Contraseña: `anonymous`

Copiar el archivo `lol.pcap` hacia el directorio local:
```
get lol.pcap
```
![5](https://user-images.githubusercontent.com/75953873/176082571-6e2485ce-3890-4e4e-a022-40aeebc2310c.png)
