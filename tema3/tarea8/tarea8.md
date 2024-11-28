### 1. **Generar un certificado SSL (opcional si ya tienes uno)**

Si no tienes un certificado SSL, puedes generar uno autofirmado para pruebas o utilizar un certificado de una Autoridad de Certificación (CA).

#### Generar un certificado autofirmado:
```bash
cd /etc/apache2/ssl
sudo openssl genrsa -out server.key 2048
sudo openssl req -new -key server.key -out server.csr
sudo openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt
```

Estos comandos generarán una clave privada (`server.key`) y un certificado (`server.crt`). Proporciona la información solicitada, como nombre de dominio (Common Name - CN).

---

### 2. **Instalar el módulo SSL en Apache**
Asegúrate de que el módulo SSL esté habilitado:
```bash
sudo a2enmod ssl
sudo systemctl restart apache2
```

---

### 3. **Configurar el VirtualHost con SSL**

Edita el archivo de configuración de tu sitio web (por ejemplo, `/etc/apache2/sites-available/prueba1.com.conf`):
```bash
cd /etc/apache2/sites-available
sudo nano prueba1.com.conf
```

```bash
<VirtualHost prueba1.com:443>
    ServerName "prueba1.com"
    ServerAlias prueba1.com

    DocumentRoot /var/www/prueba1

    SSLEngine on
    SSLCertificateFile /etc/apache2/ssl/server.crt
    SSLCertificateKeyFile /etc/apache2/ssl/server.key

    <Directory /var/www/prueba1>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/prueba1-error.log
    CustomLog ${APACHE_LOG_DIR}/prueba1-access.log combined
</VirtualHost>
```

---

### 4. **Activar el sitio y reiniciar Apache**

Habilita el archivo de configuración del sitio y reinicia Apache:
```bash
sudo a2ensite prueba1.com.conf
sudo systemctl restart apache2
```

---

### 5. **Verificar configuración**
Asegúrate de que Apache esté funcionando correctamente:
```bash
sudo apachectl configtest
```

Luego, accede al sitio en tu navegador utilizando `https://prueba1.com`.
