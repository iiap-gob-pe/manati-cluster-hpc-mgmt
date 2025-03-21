
### 🔁 **1. Habilitar uso de discos "no certificados" (bajo tu riesgo)**

#### ✅ ¿Funciona?
Sí, en muchos casos puedes forzar el uso de un disco con el mismo modelo físico (por ejemplo, `ST6000NM0034`) pero con diferente firmware (como `E0G5`), aunque esté marcado como **"Incompatible"** por el sistema.

#### ❗️Advertencias:
- Esto **puede invalidar soporte de NetApp** si tienes contrato activo.
- No es recomendable en ambientes productivos **críticos**.
- Necesitas verificar si tu arreglo tiene habilitada la opción de “**allow uncertified drives**”.

#### 🔧 Comando para forzar compatibilidad:
> ⚠️ Solo funciona en algunos firmware.

```bash
SMcli 172.16.3.239 -c "set storageArray driveFirmwareUpdateAllowUncertifiedDrives=true;" -p <password> -R admin
```

O:

```bash
SMcli 172.16.3.239 -c "set storageArray autoLoadFirmware=true;" -p <password> -R admin
```

🔁 Luego de esto, puedes intentar **reinsertar el disco incompatible** (Slot 12) y ver si ya es reconocido como utilizable.

---

### 🧠 **2. Contactar a NetApp o distribuidor oficial para obtener discos reemplazo o RMA**

- Aunque el modelo esté fuera de stock comercial, **NetApp puede tener unidades de reemplazo para clientes registrados**.
- Puedes abrir un caso con soporte técnico si tienes contrato, o buscar en su red de **VARs** (Value Added Resellers).
- Pregunta por discos "certified refurbished" si es una opción viable.

---

### 💻 **3. Migración a un nuevo grupo RAID con discos modernos**

Si ya tienes otros discos nuevos (por ejemplo, `ST6000NM0115` u otros modelos SAS de 6 TB):

- Puedes armar **un nuevo volumen RAID** en paralelo.
- Migrar los datos desde el volumen actual (si está operativo).
- Retirar gradualmente los discos antiguos.

Esta opción puede implicar más tiempo, pero es una buena forma de **modernizar sin poner en riesgo los datos**.

---

## 🔚 Resumen de Opciones

| Opción | Riesgo | Requiere contrato | ¿Solución inmediata? |
|--------|--------|-------------------|-----------------------|
| Forzar uso de disco no certificado | Medio | No | ✅ |
| Pedir disco a NetApp directamente | Bajo | Sí | ❌ depende |
| Migrar a nuevo RAID con otros discos | Bajo | No | ❌ requiere más planificación |

---

## ¿Qué haría yo en tu caso?

1. **Primero intentaría forzar el uso del disco con firmware `E0G5`** con los comandos mencionados.
2. Si no funciona, **reemplazaría con un disco nuevo** aunque no sea certificado, y monitorearía.
3. En paralelo, **empezaría a planificar la migración** a un arreglo nuevo con discos modernos y soporte.

---

¿Te gustaría que te genere un script completo para detectar discos incompatibles y probar activarlos? También puedo ayudarte con un plan de contingencia en caso de que ese volumen RAID no se recupere.