
# 🧪 Laboratorios de Pentesting (Práctica)

En este módulo se integran los conocimientos adquiridos en ejercicios prácticos que simulan escenarios reales. Cada laboratorio pone en práctica técnicas como fuerza bruta, explotación de servicios y escalada de privilegios.

---

## 📘 Presentación de la Parte Práctica

Cada ejercicio simula una situación real en entornos vulnerables. Tu objetivo será:

1. Obtener acceso inicial (a través de fuerza bruta, exploits, login anónimo, etc.)
2. Escalar privilegios a root o administrador
3. Documentar tu proceso

Recomendación: utiliza máquinas virtuales como Metasploitable, Vulnhub, o CTFs internas.

---

## 🔧 Ejercicio Práctico – Hacking WordPress + Escalada de Privilegios

### Escenario:
- WordPress vulnerable a fuerza bruta y plugins desactualizados

### Objetivo:
1. Enumerar usuarios con `wpscan`
2. Fuerza bruta de credenciales con `hydra`
3. Acceder al panel de administración
4. Subir una webshell (`.php`)
5. Escalar privilegios con `sudo -l` o `LinPEAS`

---

## 🛠️ Ejercicio Práctico – Hacking Fuerza Bruta + Escalada de Privilegios Binarios SUID

### Escenario:
- Servicio SSH expuesto
- Usuario con contraseña débil
- Escalada mediante binarios con permisos SUID

### Objetivo:
1. Enumerar usuarios con `enum4linux`
2. Ejecutar fuerza bruta con `hydra`
3. Acceder al sistema como usuario
4. Buscar binarios SUID:
```bash
find / -perm -4000 -type f 2>/dev/null
```
5. Ejecutar binarios con técnicas desde GTFOBins

---

## 💻 Ejercicio Práctico – Explotación FTP login Anonymous + Escalada de Privilegios Binarios SUID

### Escenario:
- FTP permite login como "anonymous"
- Archivo `.php` expuesto en `/var/www`
- Usuario vulnerable en el sistema

### Objetivo:
1. Conectarse con:
```bash
ftp 192.168.1.X
```

2. Descargar/visualizar archivos para detectar rutas o credenciales
3. Buscar archivos `writeable` en servicios web
4. Ganar acceso al sistema y escalar usando SUID

---

📌 Recomendaciones:

- Usa `LinPEAS` y `WinPEAS` tras comprometer el sistema
- Documenta todos los pasos, comandos y resultados
- Repite los ejercicios cambiando vectores para mejorar tu versatilidad

---

📚 Recursos:

- https://gtfobins.github.io/
- https://tryhackme.com/
- https://www.vulnhub.com/
- https://pentestmonkey.net/tools/web-shells

---

💡 “Practicar es la única forma de convertir el conocimiento en habilidad ofensiva.”
