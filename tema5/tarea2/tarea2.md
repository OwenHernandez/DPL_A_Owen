# Pasos para instalar y configurar **LDAP** en un servidor y un cliente en Linux (Ubuntu/Debian).  

---

## **1. Instalación y Configuración del Servidor LDAP**

### **Paso 1: Instalar el servidor OpenLDAP y sus herramientas**
```bash
sudo apt update
sudo apt install slapd ldap-utils -y
```
Durante la instalación, se te pedirá que configures la contraseña del usuario **admin** de LDAP.  

---

### **Paso 2: Configurar el dominio LDAP**
Después de la instalación, ejecuta:
```bash
sudo dpkg-reconfigure slapd
```
Configura lo siguiente:  
- **Omitir configuración de base de datos** → **No**  
- **Dominio DNS** → (Ejemplo: `midominio.com`)  
- **Nombre de la organización** → (Ejemplo: `MiEmpresa`)  
- **Contraseña del administrador LDAP**  
- **Base de datos a usar** → **MDB**  
- **Eliminar la base de datos al purgar slapd** → **No**  
- **Mover la base de datos anterior** → **Sí**  
- **Habilitar el acceso LDAP sobre TCP/IP** → **Sí**  

---

### **Paso 3: Verificar la instalación**
Ejecuta el siguiente comando para verificar la base de datos LDAP:
```bash
sudo ldapsearch -Q -LLL -Y EXTERNAL -H ldapi:/// -b dc=midominio,dc=com dn
```
Si LDAP está funcionando, deberías ver una lista con el dominio configurado.

---

### **Paso 4: Configurar la estructura LDAP**
Crea un archivo `ou.ldif` con la siguiente configuración:
```ldif
dn: ou=usuarios,dc=midominio,dc=com
objectClass: organizationalUnit
ou: usuarios

dn: ou=grupos,dc=midominio,dc=com
objectClass: organizationalUnit
ou: grupos
```
Carga la estructura en LDAP con:
```bash
sudo ldapadd -x -D "cn=admin,dc=midominio,dc=com" -W -f ou.ldif
```

---

### **Paso 5: Añadir usuarios LDAP**
Crea un archivo `usuario.ldif` con:
```ldif
dn: uid=jdoe,ou=usuarios,dc=midominio,dc=com
objectClass: inetOrgPerson
objectClass: posixAccount
objectClass: shadowAccount
cn: John Doe
sn: Doe
uid: jdoe
uidNumber: 1001
gidNumber: 1001
homeDirectory: /home/jdoe
loginShell: /bin/bash
mail: jdoe@midominio.com
userPassword: usuario[usar algo más seguro]
```
Agrega el usuario:
```bash
sudo ldapadd -x -D "cn=admin,dc=midominio,dc=com" -W -f usuario.ldif
```

### **Paso 6: Modificar usuarios LDAP**
Para modificar un usuario, necesitas crear un archivo `.ldif` con los cambios y aplicar la modificación
Crea un archivo `modificar_usuario.ldif` con el siguiente contenido:
```ldif
dn: uid=jdoe,ou=usuarios,dc=midominio,dc=com
changetype: modify
replace: mail
mail: nuevojdoe@midominio.com
```
Aplica el cambio con:
```bash
sudo ldapmodify -x -D "cn=admin,dc=midominio,dc=com" -W -f modificar_usuario.ldif
```

### **Paso 7: Eliminar usuarios LDAP**
Para eliminar un usuario, usa `ldapdelete`.

Eliminar el usuario `jdoe`:
```bash
sudo ldapdelete -x -D "cn=admin,dc=midominio,dc=com" -W "uid=jdoe,ou=usuarios,dc=midominio,dc=com"
```
Verifica que el usuario ha sido eliminado:
```bash
getent passwd jdoe
```
Si no muestra salida, el usuario ha sido eliminado correctamente (asegurate de ejecutar `ldapadd` del paso 5, para añadir nuevamente el usuario para continuar o crear otro).
---

## **2. Instalación y Configuración del Cliente LDAP**

### **Paso 1: Instalar los paquetes necesarios**
```bash
sudo apt install libnss-ldap libpam-ldap ldap-utils nscd -y
```
Durante la instalación, configura lo siguiente:  
- **URI del servidor LDAP** → `ldap://IP_DEL_SERVIDOR`  
- **Distinguished Name (DN) base** → `dc=midominio,dc=com`  
- **Versión de LDAP** → **3**  
- **Autenticación de root en LDAP** → **Sí**  
- **Contraseña del administrador LDAP**  

---

### **Paso 2: Configurar NSS y PAM para LDAP**
Edita el archivo `/etc/nsswitch.conf` y modifica las siguientes líneas:
```bash
passwd: compat ldap
group:  compat ldap
shadow: compat ldap
```

Edita `/etc/pam.d/common-session` y añade:
```bash
session required pam_mkhomedir.so skel=/etc/skel umask=077
```

---

### **Paso 3: Reiniciar servicios y probar**
Reinicia los servicios:
```bash
sudo systemctl restart nscd
```

Verifica si el usuario LDAP es reconocido:
```bash
getent passwd jdoe
```
Si LDAP está funcionando correctamente, verás la entrada del usuario en la salida del comando.

Puedes entrar al home de este usuario usando el comando:
```bash
sudo su - jdoe
```

---
