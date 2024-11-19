La instalación de **vsFTPd** (Very Secure FTP Daemon) en Ubuntu es sencilla. Sigue estos pasos:

---

### **1. Actualizar los repositorios**
Primero, asegúrate de que el sistema esté actualizado:

```bash
sudo apt update && sudo apt upgrade -y
```

---

### **2. Instalar vsFTPd**
Ejecuta el siguiente comando para instalar el servidor:

```bash
sudo apt install vsftpd -y
```

---

### **3. Verificar el estado del servicio**
Después de la instalación, verifica que el servicio está en ejecución:

```bash
sudo systemctl status vsftpd
```

Si no está activo, puedes iniciarlo con:

```bash
sudo systemctl start vsftpd
```

Y habilitarlo para que se inicie automáticamente al arrancar el sistema:

```bash
sudo systemctl enable vsftpd
```

---

### **4. Configuración básica de vsFTPd**
Edita el archivo de configuración principal:

```bash
sudo nano /etc/vsftpd.conf
```

#### Cambios comunes:
- **Habilitar el acceso de usuarios locales:**
  Busca la línea:

  ```plaintext
  #local_enable=YES
  ```

  Y descoméntala:

  ```plaintext
  local_enable=YES
  ```

- **Permitir la escritura (para usuarios locales):**
  Busca:

  ```plaintext
  #write_enable=YES
  ```

  Y descoméntala:

  ```plaintext
  write_enable=YES
  ```

- **Opcional: Configurar un directorio específico para usuarios locales:**
  Agrega esta línea al final del archivo para que cada usuario esté confinado a su directorio personal:

  ```plaintext
  chroot_local_user=YES
  ```

Guarda los cambios (Ctrl + O, Enter y Ctrl + X).

---

### **5. Reiniciar el servicio**
Aplica los cambios reiniciando el servicio:

```bash
sudo systemctl restart vsftpd
```

---

### **6. Prueba del servidor FTP**
- Usa un cliente FTP como **FileZilla** o el comando `ftp` desde otro sistema.
- Intenta conectarte usando las credenciales de un usuario local de tu máquina.

---

### **7. Seguridad adicional (Opcional)**
Para habilitar conexiones seguras (FTP sobre TLS), edita el archivo `/etc/vsftpd.conf` y agrega o descomenta las siguientes líneas:

```plaintext
rsa_cert_file=/etc/ssl/certs/ssl-cert-snakeoil.pem
rsa_private_key_file=/etc/ssl/private/ssl-cert-snakeoil.key
ssl_enable=YES
```

Después, reinicia el servicio con:

```bash
sudo systemctl restart vsftpd
```

---

Con estos pasos, tendrás **vsFTPd** configurado y funcionando en tu sistema Ubuntu.
