# Inventario de Activos y Análisis de Clasificación de Seguridad

Este documento ha sido elaborado desde la perspectiva de un Analista Senior de Ciberseguridad con el objetivo de estructurar, categorizar y evaluar los riesgos asociados a los activos conectados en el entorno de una oficina doméstica que opera actividades comerciales independientes. La gestión de activos constituye la piedra angular de cualquier estrategia de defensa profunda, permitiendo identificar la superficie de ataque y priorizar los esfuerzos de mitigación basándose en el impacto al negocio.

---

## 1. Matriz de Inventario de Activos de Red

A continuación, se presenta la tabla formal de inventario que integra tres activos críticos adicionales al entorno de red, detallando sus vectores de conectividad, propiedad, ubicación física, observaciones técnicas y su correspondiente nivel de sensibilidad regulado por el impacto potencial en la Confidencialidad, Integridad y Disponibilidad (Tríada CIA).

| Activo | Acceso a la Red | Propietario | Ubicación | Notas de Seguridad | Sensibilidad |
|--------|----------------|-------------|-----------|---------------------|-------------|
| Portátil de Desarrollo Principal | Continuo (Wi-Fi / Ethernet cifrado) | Consultor / Desarrollador Principal | Escritorio de la Oficina Doméstica | Almacena código fuente, llaves SSH privadas, tokens de API y credenciales de acceso a entornos de producción. | Restringido / Crítico |
| Servidor NAS y Base de Datos Local | Continuo (Enlace dedicado por Ethernet) | Consultor / Desarrollador Principal | Armario Técnico (Junto al Router) | Contiene copias de seguridad automatizadas, repositorios históricos y bases de datos locales para pruebas de arquitectura. | Confidencial |
| Electrodoméstico Inteligente (Cocina IoT) | Ocasional (Wi-Fi 2.4 GHz) | Uso Doméstico Compartido | Cocina | Firmware comercial cerrado con actualizaciones infrecuentes. Riesgo potencial de vector de movimiento lateral si se vulnera. | Público / Bajo |

---

## 2. Análisis Técnico de Sensibilidad y Justificación de Riesgos

Para determinar las clasificaciones anteriores, se ha evaluado el impacto operativo, financiero y reputacional en caso de un incidente de seguridad comprometedor:

### A. Portátil de Desarrollo Principal (Nivel: Restringido)

**Confidencialidad:** Extremadamente alta. Una exfiltración de datos expondría propiedad intelectual de terceros, secretos comerciales y las llaves de acceso que permiten administrar infraestructuras en la nube.

**Integridad:** Crítica. Si un actor malicioso modifica el código fuente alojado localmente, podría introducir vulnerabilidades de cadena de suministro (Supply Chain Attacks) antes de que el código sea empujado a repositorios remotos.

**Disponibilidad:** Alta. La pérdida o cifrado (Ransomware) de esta estación de trabajo paralizaría las operaciones comerciales del día a día de inmediato.

### B. Servidor NAS y Base de Datos Local (Nivel: Confidencial)

**Confidencialidad:** Alta. Alberga la redundancia de los datos históricos del negocio. Aunque los datos de pruebas estén anonimizados, los esquemas de bases de datos revelan la estructura lógica del software desarrollado.

**Integridad:** Alta. Los respaldos deben permanecer inmutables. La alteración de los archivos de copia de seguridad invalidaría la estrategia de recuperación ante desastres.

**Disponibilidad:** Moderada a Alta. Aunque el trabajo en tiempo real ocurre en el portátil, la pérdida del NAS elimina la capacidad de recuperación rápida ante fallos de hardware.

### C. Electrodoméstico Inteligente IoT (Nivel: Público)

**Confidencialidad:** Baja. Los datos transmitidos se limitan a telemetría básica del dispositivo y estados de uso doméstico que no impactan al negocio.

**Integridad:** Baja. Una alteración de los comandos del dispositivo afecta únicamente su funcionamiento físico local, sin comprometer registros corporativos.

**Disponibilidad:** Baja. La inoperabilidad de la conexión de red del electrodoméstico no tiene repercusión alguna sobre la continuidad del negocio o las actividades profesionales.

---

## 3. Recomendaciones Estratégicas de Hardening para el Entorno Doméstico

Como analista senior, la identificación de activos es valiosa únicamente si se acompaña de controles proactivos. Se sugieren las siguientes acciones inmediatas de mitigación:

**Segmentación de Red (VLANs):** Configurar el router principal para aislar los dispositivos de categoría "Público" (como el electrodoméstico inteligente y accesos de invitados) en una red virtual (VLAN) totalmente independiente de la red donde operan el portátil de desarrollo y el servidor NAS. Esto bloquea el movimiento lateral de un atacante.

**Cifrado en Reposo:** Implementar cifrado de disco completo (como LUKS o BitLocker) en el Portátil de Desarrollo y esquemas RAID cifrados en el NAS para proteger la información contra robos físicos.

**Autenticación Robusta:** Imponer el uso de llaves criptográficas físicas o aplicaciones de autenticación multifactor (MFA) para cualquier acceso administrativo al servidor local y consolas de gestión de red.
