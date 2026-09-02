# Lab RSTP — Root Bridge y Roles de Puerto

**Curso:** Jeremy's IT Lab
**Fecha:** 
**Tema:** RSTP (802.1w) — root bridge, roles/estados de puerto, link types

---

## Topología

<img width="610" height="427" alt="image" src="https://github.com/user-attachments/assets/c899b2cf-a392-437d-a50e-576731e0c2df" />



---

## Consigna 1 — ¿Cuál es el root bridge?

> Which switch is the root bridge? Use the CLI to examine the port role/state of each interface on the root. What appears different than what you have learned about the root bridge? What is the cause of this?

### Mi predicción (antes de la CLI)
SW1. Las 4 prioridades son iguales (32769), así que desempata la MAC más baja.
0005.5E4E.714B es la más baja → SW1 es el root.

### Comando usado
Show spanning-tree

### Conclusion
Predicción correcta: SW1 es el root (Root ID = Bridge ID = 0005.5E4E.714B).
Lo raro: Fa0/3 aparece como Back/BLK, cuando el root debería tener TODOS los
puertos Designated. Causa: Fa0/2 y Fa0/3 van al mismo Hub0 (segmento compartido);
RSTP deja Fa0/2 como Designated y Fa0/3 como Backup para evitar el bucle en ese hub.
Por eso el tipo es Shr (Shared) y no P2p.
