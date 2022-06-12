<p align="center">
  <a href="https://github.com/DenverCoder1/readme-typing-svg"><img src="https://readme-typing-svg.herokuapp.com?size=50&color=3CF700FF&width=400&height=70&lines=Mr.Robot_1"></a>
</p>
  
<h1 align="center"></h1>

**[Descargar máquina]:**

Vulnhub: https://www.vulnhub.com/entry/mr-robot-1,151/

**[Online]:**

Root-Me: https://www.root-me.org/fr/Capture-The-Flag/CTF-all-the-day/test?lang=es

<h1 align="center"></h1>

</br>

- *Paso 1:* Escanear todos los puertos que están abiertos con Nmap. 
```
nmap -p- --open -sC -n -Pn -vvv ctf14.root-me.org
```
![1](https://user-images.githubusercontent.com/75953873/173256530-9e554740-e9d2-450e-8e1a-209d773c7247.png)

Puertos abiertos: [22,80,443]

- *Paso 2:* Enumerar directorios web con Dirb. 
```
dirb http://ctf14.root-me.org /usr/share/dirb/wordlists/small.txt
```
![2](https://user-images.githubusercontent.com/75953873/173256804-380ff8a7-8b69-4153-8ee8-8c1eb7c8eb0d.png)

URL objetivo: http://ctf14.root-me.org/license

![3](https://user-images.githubusercontent.com/75953873/173256860-82d25cc3-6a8c-4e59-97a8-cbe263df5162.png)

Credenciales ofuscadas a base64: **ZWxsaW90OkVSMjgtMDY1Mgo=**

- *Paso 2:* Decodificar credenciales con Python y Bash.

`Python:`
```python
import base64
key = 'ZWxsaW90OkVSMjgtMDY1Mgo='
print(base64.b64decode(key))
```

`Bash:`
```
echo 'ZWxsaW90OkVSMjgtMDY1Mgo=' | base64 -d
```
![4](https://user-images.githubusercontent.com/75953873/173257252-c7dac9d3-f612-44ff-b31b-9d9baf5d297e.png)

Usuario: `elliot`

Contraseña: `ER28-0652`
