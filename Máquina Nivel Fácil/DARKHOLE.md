# RESOLUCIÓN DE LA MÁQUINA DARKHOLE

Abrimos la máquina.

![image](https://github.com/user-attachments/assets/b8428983-41e4-4573-9685-6541d54c60f8)

Hacemos un nmap para poder ver los puertos que estan abiertos para la IP seleccionada.

![image](https://github.com/user-attachments/assets/908dffdf-21d1-47fb-93dc-212a07bc63ac)

Ahora hacemos un escaneo de los puertos que hemos visto que estan abiertos para saber servicios,versiones...

![image](https://github.com/user-attachments/assets/6ceff54e-aced-4f71-a7ad-427cea8b1e4f)

Abrimos la web y no hay nada interesante, solo un login.

![image](https://github.com/user-attachments/assets/eaf20ca2-1ee8-4fbe-8816-4ca370d891f3)

Hacemos fuerza bruta con dirsearch.

![image](https://github.com/user-attachments/assets/fdd452b3-9b8f-486c-a4d7-61d8640a7622)

Abrimos el register.php, y nos registramos, y seguidamente nos logueamos con las credenciales dadas anteriomente.

Vemos que podemos cambiar la contraseña, y también que nos han asignado un id.

![image](https://github.com/user-attachments/assets/111d3512-a554-49de-b422-23e572694961)

Viendo esto abrimos el burpsuite, y intentamos cambiar la contraseña, introduciendo un id diferente al nuestro, en este caso el 1, ya que si nos han asignado el 2, quiere decir que el 1 ya lo tiene alguien asignado y seguramente sea el usuario admin.

![image](https://github.com/user-attachments/assets/eb0105d6-10e7-45cc-b417-b6c895831048)

Al ver que la contraseña se ha cambiado correctamente intentamos loguearnos con el usuario admin y la contraseña dada.

Y efectivamente ganamos acceso a la máquina como usuario admin y como id = 1.

![image](https://github.com/user-attachments/assets/cef1758a-d5e0-4e05-9d79-9958d38a0dcd)

Vemos que podemos subir archivos, vamos a subir un archivo malicioso, pero nos salta este mensaje: 

![image](https://github.com/user-attachments/assets/fd61de25-ae80-4e98-a694-8c0462431bb3)

Tenia un archivo .phtml de otras máquinas donde lo había usado y me ha permitido subirlo, es decir el mensaje que sale es falso.

![image](https://github.com/user-attachments/assets/2da5f64b-9dde-4bfd-a905-69707013f56a)

Nos vamos al direcotorio /upload

![image](https://github.com/user-attachments/assets/6e953dd6-ee4f-41d6-b6cd-5222b30d38b0)

Nos ponemos en escucha con netcat y ganaremos acceso dándole un click al archivo.

![image](https://github.com/user-attachments/assets/fd53b36c-2533-466b-aeb0-0da65aa2186e)

Nos vamos al direcotorio /home y vemos que tiene un usuario john que tiene un binario ejecutable dentro llamado toto.

![image](https://github.com/user-attachments/assets/d10e3c33-8cda-4fd2-83da-6c05c91890fd)

Al ejecutarlo vemos esto: 

![image](https://github.com/user-attachments/assets/aa8636db-64cf-455d-a1ba-d458c372db0a)

Vamos a crear un archivo llamado id, donde dentro vamos a poner "bash -p", para que nos otorgue una bash de dorma privilegiada.

![image](https://github.com/user-attachments/assets/cc93f648-3219-47ed-bd7b-4b1209c5dba0)

Esto lo crearemos en u  directorio, en nuestro caso en el /tmp, por tanto tendremos que modificar el $PATH para que me detecte este id desde allí.

![image](https://github.com/user-attachments/assets/6b309b87-161d-4830-9a67-5dd9d987cc72)

De esta manera ahora cuando ejecutemos el archivo desde el directorio /tmp se nos dara acceso al usuario john.

![image](https://github.com/user-attachments/assets/3ecc7d46-931c-43ee-a9d7-e766cc334660)

Hacemos ls y podemos ver la flag del user.

![image](https://github.com/user-attachments/assets/57bb30a2-e5d9-4aee-9c85-015b55baf933)

Y si miramos el contenido de la password, vemos una contraseña.

![image](https://github.com/user-attachments/assets/1571e53f-f1d8-42ee-9c1c-4d882f0094e3)

Nos conectamos desde el servicio ssh como john con las credenciales obtenidas.

![image](https://github.com/user-attachments/assets/32241c8f-107c-4c07-b4d9-9c8e345b64c8)

Hacemos sudo -l y vemos esto: 

![image](https://github.com/user-attachments/assets/34780762-4836-4681-b8b6-e0a4696b4076)

Nos vamos al archivo file.py y le añadimos un contenido para que nos permita ganar acceso como root al ejecutarlo.

![image](https://github.com/user-attachments/assets/5e4117f0-ca13-47b0-a809-66daa9e58081)

Ejecutamos el script y ejecutamos el parámetro bash -p para que me la otorgue como el propietario, que en este caso ya es root.

![image](https://github.com/user-attachments/assets/bd68ad71-3da6-4c61-b86a-9ac9e5d41c16)

Y aquí tenemos la flag del usuario root.

![image](https://github.com/user-attachments/assets/bc737e76-c1ef-444c-a791-01d86ea765b6)








