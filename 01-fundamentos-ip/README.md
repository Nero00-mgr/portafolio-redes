# Laboratorio 01: Diseño de direccionamiento IPv4 mediante VLSM

## 1. Objetivo

Diseñar un esquema de direccionamiento IPv4 para una pequeña empresa, dividiendo una red `/24` en subredes de distintos tamaños mediante VLSM (*Variable Length Subnet Mask*).

El objetivo es asignar direcciones IP de manera ordenada, evitar solapamientos entre subredes y definir los gateways de cada segmento.

## 2. Escenario

Se dispone de la red `192.168.1.0/24` y se requiere segmentarla para tres áreas:

| Área | Capacidad requerida |
|---|---:|
| Administración | 50 dispositivos |
| Operaciones | 25 dispositivos |
| Servidores | 10 dispositivos |

Se utilizará VLSM para asignar a cada área una máscara adecuada a su necesidad.

## 3. Fundamentos técnicos

IPv4 utiliza direcciones de 32 bits. El prefijo CIDR indica cuántos bits identifican la red; los bits restantes se utilizan para las direcciones de host.

Para calcular la cantidad convencional de direcciones utilizables se aplica:

`Hosts utilizables = 2^h - 2`

Donde `h` representa la cantidad de bits disponibles para hosts. Se descuentan las direcciones de red y broadcast.

Las subredes se asignan desde la de mayor requerimiento hasta la de menor requerimiento, respetando los límites de cada bloque.

## 4. Diseño de subredes

| Área | Red / Prefijo | Máscara | Rango de hosts utilizables | Broadcast | Hosts utilizables |
|---|---|---|---|---|---:|
| Administración | `192.168.1.0/26` | `255.255.255.192` | `192.168.1.1 - 192.168.1.62` | `192.168.1.63` | 62 |
| Operaciones | `192.168.1.64/27` | `255.255.255.224` | `192.168.1.65 - 192.168.1.94` | `192.168.1.95` | 30 |
| Servidores | `192.168.1.96/28` | `255.255.255.240` | `192.168.1.97 - 192.168.1.110` | `192.168.1.111` | 14 |

## 5. Asignación de gateways

Se establece como criterio utilizar la primera dirección IP utilizable de cada subred como gateway.

| Área | Gateway propuesto |
|---|---|
| Administración | `192.168.1.1` |
| Operaciones | `192.168.1.65` |
| Servidores | `192.168.1.97` |

Estas direcciones deberán configurarse en las interfaces correspondientes del router o dispositivo de capa 3 cuando se implemente la topología.

## 6. Cálculos realizados

### Administración

- Dispositivos requeridos: 50.
- Bits de host: 6.
- Prefijo: `/26`.
- Direcciones totales: `2^6 = 64`.
- Hosts utilizables: `64 - 2 = 62`.
- Máscara: `255.255.255.192`.

La subred `/27` solo permitiría 30 hosts utilizables, por lo que no satisface el requerimiento.

### Operaciones

- Dispositivos requeridos: 25.
- Bits de host: 5.
- Prefijo: `/27`.
- Direcciones totales: `2^5 = 32`.
- Hosts utilizables: `32 - 2 = 30`.
- Máscara: `255.255.255.224`.

### Servidores

- Dispositivos requeridos: 10.
- Bits de host: 4.
- Prefijo: `/28`.
- Direcciones totales: `2^4 = 16`.
- Hosts utilizables: `16 - 2 = 14`.
- Máscara: `255.255.255.240`.

## 7. Validaciones del diseño

- Las tres subredes pertenecen al bloque original `192.168.1.0/24`.
- Los bloques están alineados con los límites correspondientes a sus prefijos.
- No existe solapamiento entre las subredes asignadas.
- Los gateways propuestos pertenecen a los rangos de hosts utilizables.
- La capacidad de cada subred cubre la cantidad de dispositivos requerida.

El espacio desde `192.168.1.112` hasta `192.168.1.255` permanece sin asignar y puede reservarse para futuras ampliaciones, siempre que se planifique adecuadamente.

### 7.1 Validación mediante simulación

El diseño fue implementado en Cisco Packet Tracer utilizando un router, tres switches y equipos finales distribuidos en las áreas de Administración, Operaciones y Servidores.

Se configuraron las direcciones IPv4 y máscaras correspondientes en los equipos finales y en las interfaces físicas del router. Se realizaron pruebas de conectividad mediante `ping` para verificar la comunicación entre los equipos seleccionados.

Las capturas de la topología, configuración IP y resultados de conectividad se encuentran en la carpeta [`evidencias`](evidencias/).

La implementación permitió aplicar los cálculos VLSM en una topología simulada y comprobar el funcionamiento de la conectividad básica configurada.

## 8. Conclusiones

El uso de VLSM permite asignar subredes de diferentes tamaños según las necesidades de cada área, aprovechando el espacio de direccionamiento disponible.

La planificación previa de las redes, las máscaras y los gateways facilita la administración, el crecimiento y la resolución de problemas en una infraestructura de red.

## 9. Estado del laboratorio

- **Diseño y cálculos VLSM:** completados.
- **Implementación en Cisco Packet Tracer:** completada.
- **Asignación de direcciones IPv4 y máscaras:** completada.
- **Configuración de interfaces físicas del router:** completada.
- **Pruebas de conectividad básica:** realizadas y documentadas mediante capturas.

## 10. Herramientas y tecnologías

- **Cisco Packet Tracer:** diseño e implementación de la topología de red.
- **IPv4 y CIDR:** planificación del direccionamiento.
- **VLSM:** división de la red en subredes de distintos tamaños.
- **Cisco IOS:** configuración de direcciones IP en interfaces físicas del router.
- **`ipconfig`:** comprobación de la configuración IP de los equipos finales.
- **`ping`:** pruebas de conectividad entre equipos.

Los cálculos y el diseño se desarrollaron como ejercicio de planificación de direccionamiento IPv4. La implementación y las evidencias de simulación se incorporarán en una siguiente etapa.
