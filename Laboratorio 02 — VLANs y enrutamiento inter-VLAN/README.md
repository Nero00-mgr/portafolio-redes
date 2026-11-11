# Laboratorio 02 — VLANs y enrutamiento inter-VLAN

## 1. Objetivo

Diseñar una red empresarial segmentada mediante VLANs, configurar enlaces troncales y permitir la comunicación entre distintas VLANs utilizando un router.

## 2. Escenario

Una empresa está ampliando su infraestructura de red. Actualmente dispone de una red básica donde los equipos se conectan mediante switches y un router.

La empresa necesita separar lógicamente los dispositivos de distintos departamentos para mejorar la organización de la red y facilitar la aplicación de políticas de seguridad en el futuro.

| Área | Vlan_ID | Equipos | Capacidad requerida|
|---|---|---|---:|
| Administración | 10 | 5 PCs |50 dispositivos |
| Operaciones | 20 | 6 PCs |25 dispositivos |
| Servidores | 30 | 2 PCs + 1 Servidor | 10 dispositivos |

Tendrás disponibles:
- 1 router Cisco.
- 3 switches administrables Cisco.
- 13 dispositivos finales, incluyendo el servidor.
- Cableado Ethernet necesario.
