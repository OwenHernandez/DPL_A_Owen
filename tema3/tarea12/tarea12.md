# Instalar en Lamp nuestra página implementada en xampp

### 1. Crear la base de datos
entrar en mysql y crear la ddbb 'prueba'
```sql
  create database prueba;
```

### 2. Crear las tablas o exportar la del xampp y ponerla en la de lamp
En el phpmyadmin puedes ir a la base de datos y exportarla y luego importarla en el de lamp

### 3. Copiar los archivos que estan en el xampp y ponerlos en el lamp

```
  cp /opt/lampp/htdocs/php/nombre_del_fichero.php /var/www/html/nombre_del_fichero.php
```
Cambiar lo que haga falta en terminos de hostname, username, contraseña y database de la conección y todo debería de funcionar
