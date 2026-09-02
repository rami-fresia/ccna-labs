# Lab RSTP — Root Bridge y Roles de Puerto

**Curso:** Jeremy's IT Lab
**Fecha:** 
**Tema:** RSTP (802.1w) — root bridge, roles/estados de puerto, link types

---

## Topología

<img width="610" height="427" alt="image" src="https://github.com/user-attachments/assets/c899b2cf-a392-437d-a50e-576731e0c2df" />

### Datos base de los switches

| Switch | Prioridad | MAC | Notas |
|--------|-----------|-----|-------|
| SW1 | 32769 | 0005.5E4E.714B | root |
| SW2 | 32769 | 00D0.5882.4834 | |
| SW3 | 32769 | 000C.8519.6EBA | |
| SW4 | 32769 | 00E0.A381.AD46 | |

> Hubs: Hub0 (entre PC1/PC2 y SW1), Hub1 (entre SW1 y SW3).

---

## Consigna 1 — ¿Cuál es el root bridge?

> Which switch is the root bridge? Use the CLI to examine the port role/state of each interface on the root. What appears different than what you have learned about the root bridge? What is the cause of this?

### Mi predicción (antes de la CLI)

SW1. Las 4 prioridades son iguales (32769), así que desempata la MAC más baja.
0005.5E4E.714B es la más baja → SW1 es el root.

### Comando usado
show spanning-tree


### Salida relevante
VLAN0001
Spanning tree enabled protocol rstp
Root ID Priority 32769
Address 0005.5E4E.714B
This bridge is the root


### Conclusión

Predicción correcta: SW1 es el root (Root ID = Bridge ID = 0005.5E4E.714B).

Lo diferente de lo esperado: Fa0/3 aparece en rol **Back** (Backup) y estado **BLK** (Blocking), cuando el root bridge debería tener TODOS sus puertos Designated y en Forwarding.

Causa: Fa0/2 y Fa0/3 van al mismo Hub0 (segmento compartido). Al tener dos puertos en el mismo segmento, RSTP deja Fa0/2 como Designated y Fa0/3 como Backup para evitar un bucle en ese hub. Por eso el Type es Shr (Shared) y no P2p.
