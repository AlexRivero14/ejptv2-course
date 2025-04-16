
# 🔁 Pivoting con Metasploit

El pivoting permite utilizar una máquina comprometida como puente para acceder a redes internas o restringidas. Es una técnica fundamental en la fase de post-explotación cuando el objetivo está detrás de múltiples capas.

---

## 🗺️ Presentación del Mapa de Red

Antes de pivotear, es clave entender el entorno:
- ¿Qué subredes hay?
- ¿Qué máquinas son accesibles desde la comprometida?
- ¿Qué puertos están abiertos?

Usa herramientas como:
```bash
ip addr
route
netstat -rn
```

---

## 🪟 Pivoting en Entornos Windows

Supongamos que tienes una sesión `meterpreter` en una máquina Windows con acceso a otra subred.

### Crear una ruta:
```bash
run autoroute -s 192.168.2.0/24
```

### Usar socks proxy:
```bash
use auxiliary/server/socks_proxy
run
```

En Kali, configúralo con proxychains:
```bash
proxychains nmap -sT -Pn 192.168.2.100
```

---

## 🧪 Preparación del Laboratorio de Pivoting en Linux

Configura 3 máquinas:
- Kali (atacante)
- Host intermedio (conexión directa)
- Objetivo interno (sólo accesible desde el intermedio)

Verifica conexiones:
```bash
ping 192.168.2.1
```

---

## 🐧 Pivoting en Entornos Linux

Una vez dentro de una máquina Linux con acceso interno, puedes usar SSH, socat, o Metasploit.

### Usando socat:
```bash
socat TCP-LISTEN:1080,fork TCP:192.168.2.5:22
```

### Usando Metasploit:
```bash
use auxiliary/server/socks_proxy
```

---

## 🔐 Cómo Hacer Pivoting mediante SSH – [OPCIONAL]

SSH permite crear túneles para acceder a servicios internos.

### Reverso:
```bash
ssh -R 8080:localhost:80 user@servidor
```

### Directo (local port forwarding):
```bash
ssh -L 9999:192.168.2.10:3389 user@intermedio
```

Luego accedes a `localhost:9999` desde tu máquina atacante.

---

📌 Consejos:
- Enumera rutas disponibles desde cada host.
- Usa `autoroute`, `socks_proxy` y `proxychains` juntos para automatizar escaneo interno.
- Pivotear puede abrirte acceso a controladores de dominio, bases de datos, etc.

---

📚 Recursos útiles:

- https://book.hacktricks.xyz/pentesting/pivoting
- https://github.com/rapid7/metasploit-framework/wiki/Using-Metasploit
- man ssh, man socat

---

💡 “La clave no siempre está en la primera puerta que abres. A veces, tienes que cruzar pasillos.”
