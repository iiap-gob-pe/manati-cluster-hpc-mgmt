
```markdown
# Guía Básica de Uso de SMcli para Gestión de Almacenamiento NetApp E-Series

## 📘 Introducción

`SMcli` (Storage Manager Command Line Interface) es la herramienta de línea de comandos utilizada para gestionar sistemas de almacenamiento **NetApp E-Series**, como E2700, E2800 o E5700, entre otros. Forma parte del software **SANtricity Storage Manager**.

Esta herramienta permite realizar tareas de administración, monitoreo y mantenimiento directamente desde la terminal, sin necesidad de una interfaz gráfica. Es ideal para entornos de servidores, automatización de tareas o administración remota.

---

## ⚙️ Requisitos

- Acceso a un servidor Linux/Unix o Windows con conectividad a la red SAN.
- `SMcli` instalado (se incluye con el paquete de SANtricity).
- Acceso de administrador al arreglo de almacenamiento NetApp.
- IP o nombre del arreglo de almacenamiento.

---

## 🚀 Comandos Básicos

### 1. Ver el estado de salud del arreglo

```bash
SMcli 172.16.3.239 -c "show storageArray healthStatus;" -p <password> -R admin
```

### 2. Mostrar el perfil del arreglo

```bash
SMcli 172.16.3.239 -c "show storageArray profile;" -p <password> -R admin
```

### 3. Listar los discos físicos

```bash
SMcli 172.16.3.239 -c "show allDrives;" -p <password> -R admin
```

### 4. Listar volúmenes existentes

```bash
SMcli 172.16.3.239 -c "show allVolumes;" -p <password> -R admin
```

### 5. Obtener el estado de la batería y fuentes de poder

```bash
SMcli 172.16.3.239 -c "show storageArray batteries;" -p <password> -R admin
SMcli 172.16.3.239 -c "show storageArray powerSupplies;" -p <password> -R admin
```

---

## 📤 Ejecutar Scripts

Puedes automatizar tareas usando archivos de script con comandos:

```bash
SMcli <IP> -f /ruta/script.txt -p <password> -R admin
```

Ejemplo de contenido de `script.txt`:
```text
show storageArray healthStatus;
show allVolumes;
```

---

## 📦 Generar Paquete de Soporte

Puedes generar un paquete de soporte técnico:

```bash
SMcli <IP> -c "save storageArray supportData file=\"/tmp/supportdata.7z\";" -p <password> -R admin
```

---

## 🧪 Prueba de Alertas

```bash
SMcli -alertTest
```

---

## 🔒 Autenticación

Para mayor seguridad, puedes establecer el rol de acceso:

- `-R admin` para acceso completo.
- `-R monitor` para solo lectura.

---

## 📚 Recursos

- [Documentación oficial de NetApp SMcli](https://docs.netapp.com/us-en/e-series-cli/index.html)
- Manual local: `man SMcli` o `SMcli -?`

---

## ✅ Recomendaciones

- Siempre valida los comandos en un entorno de pruebas antes de ejecutarlos en producción.
- Mantén actualizado tu software SANtricity.
- Automatiza reportes críticos vía `cron` para monitoreo regular.

---

## 🧰 Ejemplo de Script Automatizado con Cron

Para monitorear el estado de salud diariamente:

```bash
0 6 * * * /opt/netapp/smcli 192.168.1.10 -c "show storageArray healthStatus;" -p tu_clave -R admin >> /var/log/netapp_health.log 2>&1
```

---

```

¿Te gustaría que también genere ejemplos de comandos para crear o modificar volúmenes RAID con `SMcli`? ¿O prefieres centrarte en monitoreo y diagnóstico?