# RESOLUCIÓN DE LA MÁQUINA DARKHOLE 2

Abrimos la máquina.

![image](https://github.com/user-attachments/assets/ecbe12b0-9af9-4553-ac5c-f45724fa44d7)

Hacemos un arp-scan para saber la IP de esta.

![image](https://github.com/user-attachments/assets/a0604088-af4b-496a-978f-07dbae0b6265)

Hacemos un nmap para poder ver los puertos que estan abiertos para la IP seleccionada.

![image](https://github.com/user-attachments/assets/7d6c0c5b-0e03-4193-871d-be0918733244)

Ahora hacemos un escaneo de los puertos que hemos visto que estan abiertos para saber servicios,versiones...

![image](https://github.com/user-attachments/assets/9e966ad2-9bdf-41b3-926a-fcec2193cb0f)

Abrimos la web y no hay nada interesante, solo un login.

![image](https://github.com/user-attachments/assets/fabf6b78-cba9-4954-ae76-ddec75f0b6e6)

Hacemos fuerza bruta con dirsearch.

![image](https://github.com/user-attachments/assets/9767f204-1865-47c8-8ab8-59fc2c5d9a02)

Nos traemos la ruta de la web, junto al .git a nuestra máquina para poder trabajar mejor.

![image](https://github.com/user-attachments/assets/69ad0224-ce09-4174-9351-869dbab45b19)

Entramos en los logs (git logs --oneline) y vemos esto: 

![image](https://github.com/user-attachments/assets/a2764d58-595f-40d0-a7dd-d5a025d2ec1e)

Nos copiamos el código del que habla sobre que han puesto unas credenciales defaults para ver el código que han ejecutado por detrás.

![image](https://github.com/user-attachments/assets/103877b3-3c76-4f48-93ca-d0498bdeed71)

![image](https://github.com/user-attachments/assets/7ac56908-690d-4452-b468-4a610c0549f1)

Usamos las credenciales que vemos en el código y podemos entrar correctamente.

![image](https://github.com/user-attachments/assets/1a0d86ed-e28f-4acf-922e-824c8f299822)

![image](https://github.com/user-attachments/assets/b100adb6-9c81-4a05-81de-35259a0bad84)

Nos metemos en el burpsuite y vamos a hacer SQLI.

![image](https://github.com/user-attachments/assets/c7287775-92d2-4d79-a5ae-0f6d24c94a2c)

Usamos el comando order by 6, que significa el numero de tablas que tiene, y nos da como respuesta "200 OK", para ello tendremos que hacer (Ctrl + u), pra urlencodear lo que estamos poniendo.

![image](https://github.com/user-attachments/assets/133ef8ea-1395-4a86-a962-ff06fd4ed54b)

Hacemos un (union select), y indicamos el número de columnas que antes hemos sacado que habían.

Para ello tendremos que cambiar el id, para poner una plantilla que esté vacía.

![image](https://github.com/user-attachments/assets/a7f00868-dbf0-4f4d-8ff3-77658ff32253)

En una de las columnas introducimos el parámetro "database()", y nos muestra la base de datos activa.

![image](https://github.com/user-attachments/assets/316419e5-40eb-4ff4-9af3-543a8b425a7a)

Ahora indicando la base de datos darkhole_2 y buscando las tablas que hay, encontramos la users y la ssh.

![image](https://github.com/user-attachments/assets/faf95524-d9ec-4df4-ae07-2445fa1a24d7)

Indicamos la tabla ssh y buscamos por columnas.

![image](https://github.com/user-attachments/assets/a6c8d329-48a2-4d5e-9f03-3fd015816de4)

Y indicando que queremos ver el user y la pass sacamos unas credenciales.

![image](https://github.com/user-attachments/assets/4159c09b-2f31-4e2e-be36-11aeb6cc64f5)

Entramos al servicio ssh con las credenciales obtenidas.

![image](https://github.com/user-attachments/assets/58cde5b3-b05a-4269-be1d-229654c98142)

En el directorio /home/losy, encontramos la flag del user.

![image](https://github.com/user-attachments/assets/aaffc6af-be96-4866-99ff-c63c171aa8c4)

Vemoa que hay el puerto 9999 abierto en la máquina víctima.

![image](https://github.com/user-attachments/assets/89f58a11-61e7-4658-85c0-20c004a1f8a4)

Y hacemos un local port forwarding desde ssh para que el puerto 9999 de la máquina víctima se convierta en nuestro puerto 9999.

![image](https://github.com/user-attachments/assets/40f4fc66-ca31-4c44-938c-d63e145b3b0d)

![image](https://github.com/user-attachments/assets/308976df-9d36-44c3-975b-2898dc8e5b3f)

En el directorio /opt tenemos esta información: 

![image](https://github.com/user-attachments/assets/6b1e12b4-6a85-4979-97ae-aebccab05459)

Por tanto usando el parámetro "cmd", ahora podemos ejecutar comandos.

![image](https://github.com/user-attachments/assets/82542985-2714-48d0-97fd-5ce1ddcf214e)

Vamos a hacer una reverse shell.

![image](https://github.com/user-attachments/assets/c3c451f5-9e38-47b8-8721-974fd0ea9545)

En el directorio /home/losy vemos el archivo bash_history.

![image](https://github.com/user-attachments/assets/0c486e2a-09b4-40e0-8d73-acd5d3ac25a4)

En el encontramos esto: 

![image](https://github.com/user-attachments/assets/320ba7ae-c7d6-44a6-a342-f4d0c8e8c62d)

Y usandola para poder ejecutar el sudo -l nos funciona correctamente.

![image](https://github.com/user-attachments/assets/948615bb-9af6-486a-9d67-3e7b4e27d65e)

Y ya somos root.

![image](https://github.com/user-attachments/assets/e16a7077-2fe1-4caf-b8c5-c6bab3e89a73)









