# RESOLUCIÓN DE LA MÁQUINA ELECTION 

Abrimos la máquina.

![image](https://github.com/user-attachments/assets/3cb0b101-54f3-40a5-90b2-1ee7e7b4450d)

Usamos arp-scan para saber la IP de la máquina a la que nos estamos enfrentando.

![image](https://github.com/user-attachments/assets/132b297b-2ab3-43a7-b746-9c3f029d9ee1)

Hacemos un nmap para poder ver los puertos que estan abiertos para la IP seleccionada.

![image](https://github.com/user-attachments/assets/0a02e366-8e0a-40ff-8acb-84365258c465)

Ahora hacemos un escaneo de los puertos que hemos visto que estan abiertos para saber servicios,versiones...

![image](https://github.com/user-attachments/assets/835a904c-24db-4ba8-b5d2-e988bb9aefb1)

Abrimos la web y no hay nada interesante.

![image](https://github.com/user-attachments/assets/4c55b4ee-f113-4b61-8271-5ea9da6cceb1)

Hacemos fuerza bruta con dirsearch.

![image](https://github.com/user-attachments/assets/d563517b-4147-4c36-9b21-396fd58fd40a)

Abrimos el robots.txt y encontramos esto: 

![image](https://github.com/user-attachments/assets/82d80ce5-6461-44cb-9cf1-e90ebecec6ef)

Ponemos como directorio /election, que es una de las cosas que habíamos encontrado antes en el robots, y vemos esto: 

![image](https://github.com/user-attachments/assets/eb9e8936-9412-401c-80e1-e7ddef0769f4)

Hacemos fuerza bruta con dirsearch, con el directorio /election añadido.

![image](https://github.com/user-attachments/assets/d61901a8-56f3-4f2d-bd39-7ead7916480e)

En la ruta /admin/logs, encontramos un archivo que nos proporciona unas credenciales.

![image](https://github.com/user-attachments/assets/425a2c0c-2d61-4ca3-854f-b0bffd603eb9)

Entramos al servicio ssh con las credenciales obtenidas.

![image](https://github.com/user-attachments/assets/253a73ce-11c9-43df-9cda-fa38d03ad9f3)

En el direcotorio /home/love/Desktop, encontramos la flag del user.

![image](https://github.com/user-attachments/assets/e9c97625-9294-420f-a5bb-6cc6057a1e99)

Miramos los permisos SUID y nos encontramos con uno que nos parece interesante, del cual buscamos algun exploit disponible.

![image](https://github.com/user-attachments/assets/01348514-c410-4e8e-b04f-5051381e18d0)

Copiamos el código que proporciona y lo pegamos en un archivo dentro de el directorio /tmp, al archivo lo llamamos "exploitdervU.c".

![image](https://github.com/user-attachments/assets/15af15ac-2711-4f0d-9497-a8db9376dbad)

Seguidamente ejecutamos dos comandos para poder ejecutar el exploit y de esta manera ganar acceso como root.

![image](https://github.com/user-attachments/assets/dd6c7c1b-bf75-4a39-9fb0-8f48c2da513b)

Y ya tenemos la segunda flag, la del usuario root.

![image](https://github.com/user-attachments/assets/6a5c5896-ec6c-45e8-adbc-8f64b38467c1)



