# Instalar servidor DNS en ubuntu

### Instalación y configuración de un servidor DNS Bind9 en Ubuntu 20.04

En esta guía aprenderemos a instalar y configurar nuestro propio servidor DNS utilizando Bind9. Un servidor DNS traduce nombres de dominio (como `www.networld.cu`) en direcciones IP (éj. `192.x.x.x`), lo que facilita la navegación para los usuarios y permite a los ordenadores comunicarse mediante direcciones IP.

Esta configuración es útil si estás brindando servicios en tu red y deseas que los clientes utilicen nombres de dominio en lugar de direcciones IP.

#### Información inicial del sistema:
- **Nombre de host**: `ns1`
- **FQDN**: `ns1.networld.cu`
- **Dirección IP**: `[la ip de tu ordenador]`

#### Archivos de configuración involucrados:
- `/etc/bind/named.conf.options`
- `/etc/default/named`
- `/etc/bind/named.conf.local`
- `/etc/bind/zonas/db.networld.cu` (lo crearemos)
- `/etc/bind/zonas/db.[la ip de tu ordenador sin el último número]` (lo crearemos)

---
### Pasos de configuración

#### 1. Comprobar actualizaciones del sistema
```bash
sudo apt update
sudo apt upgrade
```

#### 2. Instalar Bind9 y Nano
```bash
sudo apt install bind9 bind9-utils nano
```

#### 3. Verificar que Bind9 esté en funcionamiento
```bash
systemctl status bind9
```
Es normal ver errores o advertencias, ya que aún no hemos configurado el servidor.

#### 4. Permitir el acceso al puerto de Bind9 en el firewall
```bash
sudo ufw allow bind9
```
Esto debería devolver: **Rules Update**.

#### 5. Configuración básica de Bind9
Edita el archivo `/etc/bind/named.conf.options`:
```bash
sudo nano /etc/bind/named.conf.options
```
Asegúrate de que contenga lo siguiente:
```plaintext
listen-on { any; };
allow-query { localhost; [la ip de tu ordenador sin el último número].0/24; };
forwarders {
    8.8.8.8;
    8.8.4.4;
};
dnssec-validation no;
```
- **`listen-on`**: Define la dirección donde Bind9 escuchará. Usa `any` si no estás seguro.
- **`allow-query`**: Especifica desde qué redes o IPs se pueden realizar consultas.
- **`forwarders`**: Indica servidores DNS a los que reenviar consultas no resueltas localmente.
- **`dnssec-validation`**: Desactiva la validación de DNSSEC.

#### 6. Obligar el uso de IPv4
Edita el archivo `/etc/default/named`:
```bash
sudo nano /etc/default/named
```
Modifica la línea:
```plaintext
OPTIONS="-u bind -4"
```

#### 7. Comprobar la configuración y reiniciar Bind9
```bash
sudo named-checkconf
sudo systemctl restart bind9
systemctl status bind9
```

#### 8. Agregar zonas DNS
Edita el archivo `/etc/bind/named.conf.local`:
```bash
sudo nano /etc/bind/named.conf.local
```
Agrega las siguientes líneas:
```plaintext
zone "networld.cu" IN {
    type master;
    file "/etc/bind/zonas/db.networld.cu";
};

zone "[la ip de tu ordenador sin el último número al revés].in-addr.arpa" {
    type master;
    file "/etc/bind/zonas/db.[la ip de tu ordenador sin el último número]";
};
```
- **`zone "networld.cu"`**: Configura la zona directa.
- **`zone "[la ip de tu ordenador sin el último número al revés].in-addr.arpa"`**: Configura la zona inversa (PTR).

#### 9. Crear directorio y archivos de zonas
Crea el directorio para los archivos de zonas:
```bash
sudo mkdir /etc/bind/zonas
```

Crea el archivo de zona directa:
```bash
sudo nano /etc/bind/zonas/db.networld.cu
```
Contenido del archivo:
```plaintext
$TTL 1D
@ IN SOA ns1.networld.cu. admin.networld.cu. (
    1 ; Serial
    12h ; Refresh
    15m ; Retry
    3w ; Expire
    2h ) ; Negative Cache TTL

; Registros NS
@ IN NS ns1.networld.cu.
ns1 IN A [la ip de tu ordenador]
www IN A [la ip de tu ordenador]
```
- **`Serial`**: Incrementa este número manualmente tras modificar el archivo.
- **`admin.networld.cu.`**: Correo del administrador (sustituye `@` por `.`).

Crea el archivo de zona inversa:
```bash
sudo nano /etc/bind/zonas/db.[la ip de tu ordenador sin el último número]
```
Contenido del archivo:
```plaintext
$TTL 1D
@ IN SOA ns1.networld.cu. admin.networld.cu. (
    20210222 ; Serial
    12h ; Refresh
    15m ; Retry
    3w ; Expire
    2h ) ; Negative Cache TTL

@ IN NS ns1.networld.cu.
1 IN PTR www.networld.cu.
```

#### 10. Verificar los archivos de zona
```bash
sudo named-checkzone networld.cu /etc/bind/zonas/db.networld.cu
sudo named-checkzone [la ip de tu ordenador sin el último número al revés].in-addr.arpa /etc/bind/zonas/db.[la ip de tu ordenador sin el último número]
```
Ambos comandos deben devolver un **OK**.

#### 11. Reiniciar Bind9
```bash
sudo systemctl restart bind9
```

#### 12. Probar desde otra máquina
Ejecuta un ping al dominio configurado:
```bash
ping www.networld.cu
```

---
