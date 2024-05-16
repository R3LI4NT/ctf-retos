<p align="center">
  <a href="https://github.com/DenverCoder1/readme-typing-svg"><img src="https://readme-typing-svg.herokuapp.com?size=50&color=FF0000&width=230&height=80&lines=SummerVibes"></a>
</p>

<h1 align="center"></h1>

**[Descargar máquina]:**

Vulnhub: https://dockerlabs.es/

</br>

- *Paso 1:* Identificar la IP de la máquina y los puertos abiertos con Nmap.
```
nmap -p- --open -sS -sC -n --min-rate 3000 -vvv -Pn 172.17.0.2
```

![1](https://github.com/R3LI4NT/ctf-retos/assets/75953873/c868bf48-fac9-4e27-8f06-70c95e8f6add)

IP host: `172.17.0.2`

![2](https://github.com/R3LI4NT/ctf-retos/assets/75953873/1ad05973-db3b-4b88-b46e-75774fab1313)

Puertos abiertos: [22,80]

- *Paso 2:* Identificar las versiones de los servicios del puerto 80 y 22.
```
nmap -sV 172.17.0.2
```

![3](https://github.com/R3LI4NT/ctf-retos/assets/75953873/397179b4-b274-4f34-83c1-b35dabd2488f)

Versiones: 
- 22:OpenSSH 8.9p1

- 80:Apache httpd 2.4.52
