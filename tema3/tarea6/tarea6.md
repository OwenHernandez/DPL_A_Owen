# Formulario de inserción de datos

El index.php

```html
<form action="insert.php" method="post">
    <h2>Formulario para insertar datos</h2>
    <label for="name">Nombre: </label>
    <input type="text" name="name"/><br>
    <label for="email">Email: </label>
    <input type="text" name="email"/><br>
    <input type="submit" value="Enviar"/>
</form>
```

El insert.php (asegurarse de que el fichero php se llama igual que el "action" del form, con la ruta relativa)

```php
<?php 
    $connection = mysqli_connect(
        'localhost',
        'root',
        '1q2w3e4r',
        'prueba'
    );

    echo '<pre>';
    
    $name = $_POST['name'];
    $email = $_POST['email'];
    
    $delete = 'insert into users(name, email) values("'. $name.'", "'.$email.'");';

    $return_delete = mysqli_query($connection, $delete);
    if ($return_delete) {
        echo "bien";
    } else {
        echo "mal";
    }
    mysqli_close($connection);
```

# Formulario de actualización de datos

El index.php

```html
<form action="update.php" method="post">
    <h2>Formulario para actualizar datos</h2>
    <label for="id">Digame el id del usuario que desea actualizar:</label>
    <input type="text" name="id"><br>
    <label for="name">Nombre: </label>
    <input type="text" name="name"/><br>
    <label for="email">Email: </label>
    <input type="text" name="email"/><br>
    <input type="submit" value="Enviar"/>
</form>
```

El update.php (asegurarse de que el fichero php se llama igual que el "action" del form, con la ruta relativa)

```php
<?php 
  $connection = mysqli_connect(
      'localhost',
      'root',
      '1q2w3e4r',
      'prueba'
  );

  echo '<pre>';
  
  $id = $_POST['id'];
  $name = $_POST['name'];
  $email = $_POST['email'];
  
  $delete = "update users set name = '$name', email = '$email' where id = $id;";

  $return_delete = mysqli_query($connection, $delete);
  if ($return_delete == 1) {
      echo "bien";
  } else {
      echo "mal";
  }
  mysqli_close($connection);
```

# Formulario para borrar datos

El index.php

```html
<form action="delete.php" method="post">
    <h2>Formulario para borrar datos</h2>
    <label for="id">Digame el id del usuario que desea borrar:</label>
    <input type="text" name="id"><br>
    <input type="submit" value="Enviar"/>
</form>
```

El delete.php (asegurarse de que el fichero php se llama igual que el "action" del form, con la ruta relativa)

```php
<?php 
  $connection = mysqli_connect(
      'localhost',
      'root',
      '1q2w3e4r',
      'prueba'
  );

  echo '<pre>';
  
  $id = $_POST['id'];
  
  $delete = "delete from users where id = $id";

  $return_delete = mysqli_query($connection, $delete);
  if ($return_delete) {
      echo "bien";
  } else {
      echo "mal";
  }
  mysqli_close($connection);
```
