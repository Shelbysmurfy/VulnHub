# RESOLUCIÓN DE LA MÁQUINA HACK ME PLEASE

Abrimos la máquina.

![image](https://github.com/user-attachments/assets/f94d714d-18fb-4c14-99c6-b6c941bca8ab)

Hacemos un arp-scan para saber la IP de esta.

![image](https://github.com/user-attachments/assets/f34394e9-4a10-425d-a921-1b00aa1d79c2)

Hacemos un nmap para poder ver los puertos que estan abiertos para la IP seleccionada.

![image](https://github.com/user-attachments/assets/89417ea3-0bef-49f2-ac64-b115916122b4)

Ahora hacemos un escaneo de los puertos que hemos visto que estan abiertos para saber servicios,versiones...

![image](https://github.com/user-attachments/assets/45406ef9-0098-4e37-ba4e-f2f347d95a6a)

Abrimos la web.

![image](https://github.com/user-attachments/assets/b158d14c-21dc-4bd7-af70-25c2b8e8c2e0)

Al no ver nada, inspeccionamos la página y encontramos un script llamado main.js

![image](https://github.com/user-attachments/assets/384dc7ce-2637-409e-8c3f-c322c4399b0b)

Lo abrimos y encontramos una pista.

![image](https://github.com/user-attachments/assets/bef83b10-e760-4d44-a4f9-1efcd879e92b)

Lo abrimos y encontramos un login con el servicio SeedDMS

![image](https://github.com/user-attachments/assets/b142cc0d-fbeb-4d60-9284-b409620a2f08)

Al no tener nada hacemos fuerza bruta pero no encontramos nada, así que vamos a un github para ver posibles directorios que puede tener la ruta pero que por fuerza bruta no los estamos viendo.

Y en la ruta /conf/settings.xml encontramos unas posibles credenciales del servicio mysql.

![image](https://github.com/user-attachments/assets/828ed907-c3d7-4d23-9dbc-7d9a530098a3)







