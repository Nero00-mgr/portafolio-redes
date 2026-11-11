# Laboratorio 02 — VLANs y enrutamiento inter-VLAN

## 1. Objetivo

Diseñar una red empresarial segmentada mediante VLANs, configurar enlaces troncales y permitir la comunicación entre distintas VLANs utilizando un router.

## 2. Escenario

Una empresa está ampliando su infraestructura de red. Actualmente dispone de una red básica donde los equipos se conectan mediante switches y un router.

La empresa necesita separar lógicamente los dispositivos de distintos departamentos mediante VLANs, permitiendo la comunicación entre ellas a través de un router.

Se utilizará como bloque principal la red privada `10.10.1.0/24`, que será dividida mediante VLSM considerando las necesidades de cada departamento.

| Área | VLAN ID | Equipos implementados | Capacidad requerida |
|---|---:|---|---:|
| Administración | 10 | 5 PCs | 45 hosts |
| Operaciones | 20 | 6 PCs | 28 hosts |
| TI / Servidores | 30 | 2 PCs y 1 servidor | 12 hosts |

### Dispositivos de red

- 1 router Cisco.
- 3 switches administrables Cisco.
- 13 dispositivos finales, incluyendo un servidor.
- Cableado Ethernet.


## 3. Diseño de direccionamiento IPv4

Se seleccionó la red privada `10.10.1.0/24` como bloque principal para la infraestructura.

Mediante VLSM se dividió la red en tres subredes independientes, considerando los requerimientos de capacidad de cada departamento.

Se estableció como criterio utilizar la primera dirección IP utilizable de cada subred como gateway predeterminado.

| VLAN | Área | Red / Prefijo | Máscara | Gateway | Broadcast |
|---|---|---|---|---|---|
| 10 | Administración | `10.10.1.0/26` | `255.255.255.192` | `10.10.1.1` | `10.10.1.63` |
| 20 | Operaciones | `10.10.1.64/27` | `255.255.255.224` | `10.10.1.65` | `10.10.1.95` |
| 30 | TI / Servidores | `10.10.1.96/28` | `255.255.255.240` | `10.10.1.97` | `10.10.1.111` |

Las subredes no presentan solapamientos y permiten reservar direcciones para futuras ampliaciones.
