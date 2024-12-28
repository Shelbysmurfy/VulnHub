# RESOLUCIÓN DE LA MÁQUINA SYMFONOS

Abrimos la máquina.

![image](https://github.com/user-attachments/assets/d3cdeef7-efce-47df-8edf-4d90be831cd8)

Usamos arp-scan para saber la IP de la máquina a la que nos estamos enfrentando.

![image](https://github.com/user-attachments/assets/b40f8f95-aa04-40ef-9908-c5ba9fc15910)

Hacemos un nmap para poder ver los puertos que estan abiertos para la IP seleccionada.

![image](https://github.com/user-attachments/assets/15d74f40-0c40-4d60-9945-1aa5a83cb9fa)

Ahora hacemos un escaneo de los puertos que hemos visto que estan abiertos para saber servicios,versiones...

![image](https://github.com/user-attachments/assets/ed3d285a-2a2d-4380-a153-d033c8d5d144)
![image](https://github.com/user-attachments/assets/37f37113-93be-4129-8c34-98fc68928c2d)

Ahora sabiendo que estamos tratando con sistemas SMB, usaremos enum4linux para recopilar información sobre estos.

![image](https://github.com/user-attachments/assets/a57cf03c-fde6-4324-a053-2a088a50386f)

Nos encontramos tanto directorios como usuarios.

![image](https://github.com/user-attachments/assets/522cfab3-35fb-4fae-a3d9-8c19e2824869)

![image](https://github.com/user-attachments/assets/3e3737e4-cd27-4d71-b22b-49e97b3e9da5)

Vemos que el directorio anonymous me devuelve ok, quiere decir que no hace falta contraseñas ni usuarios para poder entrar y ver que hay dentro.

![image](https://github.com/user-attachments/assets/2096e782-e672-4134-9150-1c8794c1f107)

Entramos al directorio con smbclient y vemos un archivo.

![image](https://github.com/user-attachments/assets/8f0bd11b-7cc5-4061-afdb-a92cb50f76db)

![image](https://github.com/user-attachments/assets/b8934a96-1f8d-4023-ab55-9ac04e98c807)

Sabiendo que esas són las contraseñas que usan los usuarios, y nosotros sabemos que hay un usuario llamado helios, vamos a intentar entrar con smbclient al directorio helios, con el usuario helios y alguna de las contraseñas dadas.

Entramos con la contraseña: qwerty, y vemos dos archivos.

![image](https://github.com/user-attachments/assets/648dcb10-d272-4f4d-8c2d-69d6537d16d7)

El research.txt muestra esto: 

![image](https://github.com/user-attachments/assets/1a651c9d-86fa-4d55-9e2e-b46a5fa16da8)

Y el todo.txt esto: 

![image](https://github.com/user-attachments/assets/0fb9664c-250e-4a8c-b790-0f9e18fc5224)

Ponemos el posible directorio que nos da en el archivo todo.txt y nos muestra esto: 

![image](https://github.com/user-attachments/assets/59cf9827-04bd-4109-a9ca-8d0bb3601412)

Vamos a hacer wpscan porque vemos que es un wordpress.

![image](https://github.com/user-attachments/assets/f30ef2ef-303b-4f6c-ac0d-71f69a653a79)

![image](https://github.com/user-attachments/assets/12fee351-099a-46b0-9137-ad8564abd01f)

Al ver el pluggin mail-masta vamos a buscar una vulnerabilidad con este que nos permitirá hacer un LFI.

![image](https://github.com/user-attachments/assets/a3f78363-a0db-4c0a-8334-c5bcc6264f65)

De esta manera podemos ver el /etc/passwd, en el cual vemos el usuario helios.

![image](https://github.com/user-attachments/assets/f9ec7c64-cb1c-45f0-91c8-2a5cfd4da676)

Cuando estamos explotando un LFI, tenemos que pensar que fácilmente también podremos explotar un Log Poisoning (puerto 25).

Con netcat entramos dentro del puerto 25.

![image](https://github.com/user-attachments/assets/fc227db4-1c95-49c7-b153-61b87cc512ff)

Introducimos un mail (MAIL FROM), también un usuario existente (RCPT TO), y por último añadimos un código php malicioso (DATA), le damos al enter y ponemos un punto para que se ejecute correctamente.

![image](https://github.com/user-attachments/assets/b9da1e27-eb86-49a6-b085-770834c5970c)

Nos vamos a la web y añadimos en la url (/var/mail/helios&cmd=id), y nos funciona correctamente, ponemos el directorio /var/mail, porque es donde se guarda lo que he hecho anteriormente por el puerto 25.

![image](https://github.com/user-attachments/assets/2d812834-9c84-4ed8-94a4-df8a418182ff)

Hacemos una reverse shell.

![image](https://github.com/user-attachments/assets/1b55f5fc-ef03-4867-b438-c776ba2dedd9)

Buscamos permisos SUID.

![image](https://github.com/user-attachments/assets/3c2ef4ce-813e-4a7a-9361-bad42524e910)

El archivo statuscheck tiene permisos de root.

![image](https://github.com/user-attachments/assets/6dfc2503-ab3e-4889-9ab7-ad45716b822a)

Al ejecutar este comando vemos que el usuario root ejecuta el curl.

![image](https://github.com/user-attachments/assets/94f0285f-2914-49bd-8bbf-9a997165206c)

Sabiendo que se ejecuta el curl, vamos a hacer path hijacking, para eso tendremos que ir al directorio /tmp y ejecutar estos comandos: 

![image](https://github.com/user-attachments/assets/298504d2-c4e1-4329-a376-3efd9fef17f3)

Y ahora ejecutando bash -p ya somos root.

![image](https://github.com/user-attachments/assets/d137b4e4-d3a0-4fac-be70-2763d2ead1f9)

![image](https://github.com/user-attachments/assets/d4b43389-e4de-443f-bf5c-e8cc6f2eed9a)













