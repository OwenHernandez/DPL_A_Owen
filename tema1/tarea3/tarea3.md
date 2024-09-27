## Crear una cuenta en GitHub

Ve a GitHub.

Haz clic en "Sign up" y sigue las instrucciones para crear una cuenta.

## Crear un repositorio llamado “banco”

Inicia sesión en tu cuenta de GitHub.

Haz clic en el botón "+" en la esquina superior derecha y selecciona "New repository".

Asigna el nombre "banco" y configura la visibilidad (público o privado).

Haz clic en "Create repository".

## Clonar el repositorio desde la línea de comandos

Abre tu terminal o línea de comandos.

Navega a la carpeta donde deseas clonar el repositorio:
```
cd ruta/deseada
```

Clona el repositorio usando el siguiente comando:

```
git clone https://github.com/tu_usuario/banco.git
```
(Reemplaza tu_usuario con tu nombre de usuario de GitHub).

## Crear un proyecto llamado “banco”

En otra carpeta, crea un nuevo proyecto llamado "banco". Puedes hacerlo desde la línea de comandos:

    
```
mkdir ruta/nueva_carpeta/banco
cd ruta/nueva_carpeta/banco
```

## Copiar la carpeta del proyecto del banco al repositorio clonado

Copia la carpeta del proyecto "banco" en la carpeta donde clonaste el repositorio:

    
```
cp -r ruta/nueva_carpeta/banco ruta/deseada/banco
```
## Hacer un commit y push desde Visual Studio

Abre Visual Studio y carga el proyecto del repositorio "banco".

En el panel de "Team Explorer", realiza un commit:

Escribe un mensaje de commit.

Haz clic en "Commit All".

Luego, haz clic en "Sync" y después en "Push" para subir los cambios a GitHub.

## Borrar del disco duro todo el código del banco

Puedes eliminar la carpeta del proyecto "banco" con:
```
rm -rf ruta/nueva_carpeta/banco
```
## Clonar el proyecto del banco de GitHub a local

En la terminal, navega a la carpeta donde deseas clonar el proyecto nuevamente.

Clona el repositorio:

```
git clone https://github.com/tu_usuario/banco.git
```
## Hacer una modificación del código y subirlo a GitHub

Navega a la carpeta del proyecto clonado:
```
cd banco
```
Realiza las modificaciones que necesites en tu código.

Guarda los cambios.

Desde Visual Studio, realiza un nuevo commit y luego haz un push para subir los cambios:

Haz clic en "Commit All".

Después, en "Sync", haz clic en "Push".
