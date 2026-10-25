# ⚡ Guión Rápido de Defensa — TP6 (1 a 1.5 min)

## 1. Qué es (15 seg)
> *"Desarrollamos una suite móvil para técnicos de telecomunicaciones en campo. Resuelve dos problemas: gestiona equipos mediante **sockets crudos (SNMP/SSH)** porque no tienen APIs web, y opera **100% Offline con patrón Outbox** para sincronizar con el NOC al recuperar señal."*

---

## 2. Demo en 4 Clicks (1 min)

1. **Escáner:** Pestaña **Escáner LAN** ➔ Tocar **Escanear**. Detecta equipos, fabricantes (Huawei, MikroTik, Cisco) y RTT.
2. **SNMP:** Pestaña **SNMP MIB** ➔ Tocar **Enviar GetRequest**. Muestra Uptime, tráfico, potencia óptica GPON y la trama ASN.1/BER en hexadecimal.
3. **SSH y Acta:** Pestaña **Instalación** ➔ Tocar **Cargar QR**, **Fijar GPS** y **Generar PDF**. Genera el acta digital con firma y geolocalización.
4. **Offline & Outbox:** En **Inicio** activar switch **Modo Offline**. Ir a **Outbox**: las acciones quedan en cola **PENDING**. Apagar modo offline, tocar **Sincronizar** y mostrar cómo pasan a **SYNCED** contra el backend.

---

## 3. Respuestas de 1 Renglón (si preguntan)

* **¿Por qué parser propio ASN.1/BER?** No hay stack SNMP nativo en JS; decodificamos tripletas TLV (RFC 1157/1213) directamente sobre sockets UDP.
* **¿Seguridad de claves SSH?** `CredentialVault` en hardware seguro (Android Keystore / iOS Keychain), nunca en texto plano (OWASP M02).
* **¿Cómo evitan duplicados al sincronizar?** Cada evento tiene UUID único (idempotencia) y resolución *Last-Write-Wins*.
* **¿Por qué APK nativo y no Expo Go?** Sockets TCP/UDP crudos requieren módulos nativos fuera del sandbox de Expo Go.

