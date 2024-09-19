# Pasos para securizar el usuario root del Mysql

1. Ir a la carpeta donde esta ubicado el xampp (en mi caso esta en opt/lampp)

2. Ir a la carpeta de phpmyadmin

3. Ir al fichero llamado "config.inc.php" y modificar lo siguiente (de normal te aparecera así)

![imagen](https://github.com/user-attachments/assets/76456b55-a0d2-4309-8536-c67ef0b5e39d)

4. En los campos que dice "config" debe de poner "http" y donde dice "password", en las comillas vacias poner una contraseña y guardar el fichero

5. Reiniciar los servicios del xampp y ahora te deberia de pedir la contraseña para el usuario root en phpmyadmin

# Pasos para crear un usuario nuevo (para evitar usar root)

1. Ir al phpmyadmin y hacer un login con root

2. Ir a cuentas de usuarios y hacer click en donde dice "Agregar cuenta de usuario"

3. Rellenar el nombre y la contraseña con lo que se crea adecuado

4. Poner "localhost" en el nombre del host

5. Hacer click en "Crear base de datos con el mismo nombre y otorgar todos los privilegios" más abajo darle a "Datos" y "Estructuras", y algo más que se crea conveniente

6. Y hacer click en "Continuar" abajo del todo.
