<![CDATA[<!-- 
  ============================================================================
  📄 DOCUMENTO DE PORTAFOLIO PROFESIONAL — CIBERSEGURIDAD
  Autor: Brandon Rondon
  Clasificación del Documento: PÚBLICO (Apto para repositorio abierto)
  Última Revisión: Julio 2025
  ============================================================================
  ⚠️ AVISO: Este documento ha sido elaborado con fines demostrativos y de
  portafolio profesional. Todos los datos presentados son ficticios o han sido
  anonimizados. No se expone información real de infraestructura, credenciales,
  direcciones IP ni datos de clientes.
  ============================================================================
-->

<div align="center">

# 🛡️ Inventario de Activos de Red & Análisis de Clasificación de Seguridad

**Evaluación basada en la Tríada CIA (Confidencialidad · Integridad · Disponibilidad)**

![Cybersecurity](https://img.shields.io/badge/Cybersecurity-Asset%20Management-0A66C2?style=for-the-badge&logo=shield&logoColor=white)
![CIA Triad](https://img.shields.io/badge/Framework-CIA%20Triad-28A745?style=for-the-badge&logo=verified&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)

---

*Elaborado desde la perspectiva de un **Analista Senior de Ciberseguridad** para estructurar, categorizar y evaluar los riesgos asociados a los activos conectados en un entorno de oficina doméstica con actividad comercial independiente.*

</div>

---

## 📑 Tabla de Contenidos

- [Resumen Ejecutivo](#-resumen-ejecutivo)
- [Alcance y Metodología](#-alcance-y-metodología)
- [Marco de Referencia: Tríada CIA](#-marco-de-referencia-tríada-cia)
- [Matriz de Inventario de Activos de Red](#-matriz-de-inventario-de-activos-de-red)
- [Análisis Técnico de Sensibilidad por Activo](#-análisis-técnico-de-sensibilidad-por-activo)
  - [Portátil de Desarrollo Principal](#a-portátil-de-desarrollo-principal--nivel-restringido--crítico)
  - [Servidor NAS y Base de Datos Local](#b-servidor-nas-y-base-de-datos-local--nivel-confidencial)
  - [Electrodoméstico Inteligente IoT](#c-electrodoméstico-inteligente-iot--nivel-público--bajo)
- [Mapa de Riesgos Consolidado](#-mapa-de-riesgos-consolidado)
- [Recomendaciones Estratégicas de Hardening](#-recomendaciones-estratégicas-de-hardening)
- [Controles Alineados con Frameworks de la Industria](#-controles-alineados-con-frameworks-de-la-industria)
- [Conclusiones](#-conclusiones)
- [Disclaimer](#%EF%B8%8F-disclaimer)

---

## 📋 Resumen Ejecutivo

La gestión de activos constituye la **piedra angular** de cualquier estrategia de defensa en profundidad (*Defense in Depth*). Sin un inventario exhaustivo y una clasificación rigurosa, es imposible determinar la superficie de ataque real ni priorizar los esfuerzos de mitigación en función del impacto al negocio.

Este documento presenta un análisis completo del entorno de red de una oficina doméstica que soporta actividades comerciales independientes de desarrollo de software y consultoría tecnológica. El análisis cubre:

| Elemento | Detalle |
|:---------|:--------|
| **Activos inventariados** | 3 activos críticos conectados a la red |
| **Marco de evaluación** | Tríada CIA (Confidencialidad, Integridad, Disponibilidad) |
| **Niveles de clasificación** | Restringido/Crítico · Confidencial · Público/Bajo |
| **Controles propuestos** | Segmentación, cifrado, autenticación robusta, monitoreo |
| **Frameworks alineados** | NIST CSF · ISO 27001 · CIS Controls |

> **Hallazgo Principal:** El activo de mayor riesgo es el *Portátil de Desarrollo Principal*, cuya compromisión podría derivar en ataques de cadena de suministro (*Supply Chain Attacks*), exfiltración de propiedad intelectual y paralización operativa completa.

---

## 🔬 Alcance y Metodología

### Entorno Evaluado

```
┌─────────────────────────────────────────────────────────────┐
│                   OFICINA DOMÉSTICA                         │
│               (Actividad Comercial Independiente)           │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│   [Internet] ──► [Router/Firewall] ──┬── [VLAN Trabajo]    │
│                                      │    ├── Portátil Dev  │
│                                      │    └── Servidor NAS  │
│                                      │                      │
│                                      └── [VLAN IoT/Guest]   │
│                                           └── Smart Kitchen │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Metodología

1. **Descubrimiento de activos**: Enumeración completa de dispositivos conectados a la red local mediante escaneo pasivo y revisión de tablas ARP/DHCP del router.
2. **Clasificación de sensibilidad**: Evaluación de cada activo contra los tres pilares de la Tríada CIA, ponderando el impacto operativo, financiero y reputacional.
3. **Evaluación de riesgos**: Identificación de vectores de ataque y escenarios de amenaza por activo.
4. **Formulación de controles**: Propuesta de medidas de mitigación alineadas con frameworks internacionales.

---

## 🔺 Marco de Referencia: Tríada CIA

La **Tríada CIA** es el modelo fundamental en seguridad de la información. Cada activo es evaluado contra estos tres pilares para determinar su nivel de sensibilidad:

```
                    ╔══════════════════════╗
                    ║  CONFIDENCIALIDAD    ║
                    ║  (Confidentiality)   ║
                    ╚══════════╤═══════════╝
                               │
                    ┌──────────┴──────────┐
                    │   TRÍADA CIA        │
                    │   ═══════════       │
                    │   Modelo central    │
                    │   de evaluación     │
                    │   de seguridad      │
                    └──┬──────────────┬───┘
                       │              │
          ╔════════════╧═══╗   ╔══════╧═══════════╗
          ║  INTEGRIDAD    ║   ║  DISPONIBILIDAD   ║
          ║  (Integrity)   ║   ║  (Availability)   ║
          ╚════════════════╝   ╚═══════════════════╝
```

| Pilar | Definición | Pregunta Clave |
|:------|:-----------|:---------------|
| 🔒 **Confidencialidad** | Garantizar que la información sea accesible únicamente por personas autorizadas | *¿Qué ocurre si esta información es expuesta a un actor no autorizado?* |
| 🔐 **Integridad** | Asegurar la exactitud y completitud de los datos y los métodos de procesamiento | *¿Qué ocurre si esta información es modificada sin autorización o de forma inadvertida?* |
| ⚡ **Disponibilidad** | Garantizar que los usuarios autorizados tengan acceso a la información cuando lo necesiten | *¿Qué ocurre si este sistema o esta información deja de estar accesible?* |

---

## 📊 Matriz de Inventario de Activos de Red

La siguiente tabla integra los tres activos críticos del entorno, detallando sus vectores de conectividad, propiedad, ubicación, observaciones técnicas y nivel de sensibilidad:

| # | Activo | Acceso a la Red | Propietario | Ubicación Física | Notas de Seguridad | Sensibilidad |
|:-:|:-------|:-----------------|:------------|:------------------|:--------------------|:-------------|
| 1 | **Portátil de Desarrollo Principal** | Continuo (Wi-Fi 5 GHz / Ethernet cifrado) | Consultor / Desarrollador Principal | Escritorio de la Oficina Doméstica | Almacena código fuente, llaves SSH privadas, tokens de API y credenciales de acceso a entornos de producción. | 🔴 **Restringido / Crítico** |
| 2 | **Servidor NAS y Base de Datos Local** | Continuo (Enlace dedicado por Ethernet) | Consultor / Desarrollador Principal | Armario Técnico (Junto al Router) | Contiene copias de seguridad automatizadas, repositorios históricos y bases de datos locales para pruebas de arquitectura. | 🟠 **Confidencial** |
| 3 | **Electrodoméstico Inteligente (Cocina IoT)** | Ocasional (Wi-Fi 2.4 GHz) | Uso Doméstico Compartido | Cocina | Firmware comercial cerrado con actualizaciones infrecuentes. Riesgo potencial de vector de movimiento lateral si se vulnera. | 🟢 **Público / Bajo** |

### Leyenda de Niveles de Sensibilidad

| Nivel | Icono | Descripción | Impacto de Compromisión |
|:------|:-----:|:------------|:------------------------|
| **Restringido / Crítico** | 🔴 | Acceso estrictamente limitado. Requiere controles máximos. | Catastrófico: pérdida financiera, legal y reputacional grave. |
| **Confidencial** | 🟠 | Acceso limitado a personal autorizado. Requiere controles significativos. | Severo: afectación a la continuidad del negocio y recuperación ante desastres. |
| **Público / Bajo** | 🟢 | Sin impacto directo al negocio. Controles básicos de higiene. | Mínimo: sin repercusión en operaciones comerciales. |

---

## 🔍 Análisis Técnico de Sensibilidad por Activo

Para determinar las clasificaciones anteriores, se ha evaluado el **impacto operativo, financiero y reputacional** en caso de un incidente de seguridad comprometedor para cada uno de los tres pilares de la Tríada CIA.

---

### A. Portátil de Desarrollo Principal — Nivel: Restringido / Crítico

> **Veredicto:** Este es el activo de **mayor criticidad** en todo el entorno. Su compromisión representa un riesgo existencial para las operaciones del negocio.

#### Evaluación CIA Detallada

| Pilar CIA | Nivel de Impacto | Justificación |
|:----------|:-----------------|:--------------|
| 🔒 **Confidencialidad** | 🔴 **Extremadamente Alta** | Una exfiltración de datos expondría propiedad intelectual de terceros, secretos comerciales y las llaves de acceso que permiten administrar infraestructuras en la nube. La filtración de llaves SSH y tokens API otorgaría a un atacante acceso directo a entornos de producción de clientes. |
| 🔐 **Integridad** | 🔴 **Crítica** | Si un actor malicioso modifica el código fuente alojado localmente, podría introducir vulnerabilidades de **cadena de suministro** (*Supply Chain Attacks*) antes de que el código sea empujado (*pushed*) a repositorios remotos. Este vector es particularmente insidioso por su dificultad de detección. |
| ⚡ **Disponibilidad** | 🟠 **Alta** | La pérdida o cifrado por **ransomware** de esta estación de trabajo paralizaría las operaciones comerciales del día a día de forma inmediata. Cada hora de inactividad se traduce directamente en pérdida de ingresos y potencial incumplimiento de plazos contractuales. |

#### Vectores de Amenaza Identificados

```
Amenaza                          Probabilidad    Impacto     Riesgo
─────────────────────────────────────────────────────────────────────
Phishing / Spear-phishing         ALTA           CRÍTICO     🔴 ALTO
Malware / Ransomware              MEDIA          CRÍTICO     🔴 ALTO
Robo físico del dispositivo       BAJA           CRÍTICO     🟠 MEDIO
Acceso no autorizado (local)      BAJA           ALTO        🟡 MEDIO
Explotación de software sin       MEDIA          ALTO        🟠 MEDIO
  parches (0-day / N-day)
```

---

### B. Servidor NAS y Base de Datos Local — Nivel: Confidencial

> **Veredicto:** Activo de soporte crítico que garantiza la **resiliencia operativa**. Su compromisión no detiene las operaciones inmediatas, pero elimina la capacidad de recuperación ante desastres.

#### Evaluación CIA Detallada

| Pilar CIA | Nivel de Impacto | Justificación |
|:----------|:-----------------|:--------------|
| 🔒 **Confidencialidad** | 🟠 **Alta** | Alberga la redundancia de los datos históricos del negocio. Aunque los datos de pruebas estén anonimizados, los esquemas de bases de datos revelan la estructura lógica del software desarrollado, lo cual constituye propiedad intelectual valiosa para un competidor o atacante sofisticado. |
| 🔐 **Integridad** | 🟠 **Alta** | Los respaldos deben permanecer **inmutables**. La alteración silenciosa de los archivos de copia de seguridad (*backup poisoning*) invalidaría completamente la estrategia de recuperación ante desastres, dejando al negocio sin red de seguridad ante un incidente mayor. |
| ⚡ **Disponibilidad** | 🟡 **Moderada a Alta** | Aunque el trabajo en tiempo real ocurre en el portátil, la pérdida del NAS elimina la capacidad de **recuperación rápida** ante fallos de hardware. El RTO (*Recovery Time Objective*) se incrementaría de horas a días o semanas. |

#### Vectores de Amenaza Identificados

```
Amenaza                          Probabilidad    Impacto     Riesgo
─────────────────────────────────────────────────────────────────────
Acceso no autorizado vía red      MEDIA          ALTO        🟠 MEDIO
Fallo de hardware (discos)        MEDIA          ALTO        🟠 MEDIO
Ransomware propagado desde        MEDIA          CRÍTICO     🔴 ALTO
  otro activo comprometido
Corrupción de datos silenciosa    BAJA           ALTO        🟡 MEDIO
Robo físico                       BAJA           ALTO        🟡 MEDIO
```

---

### C. Electrodoméstico Inteligente IoT — Nivel: Público / Bajo

> **Veredicto:** Activo de **bajo impacto directo** al negocio, pero con potencial como **vector de movimiento lateral** hacia activos críticos si la red no está adecuadamente segmentada.

#### Evaluación CIA Detallada

| Pilar CIA | Nivel de Impacto | Justificación |
|:----------|:-----------------|:--------------|
| 🔒 **Confidencialidad** | 🟢 **Baja** | Los datos transmitidos se limitan a telemetría básica del dispositivo y estados de uso doméstico que no impactan al negocio. Sin embargo, los metadatos de red (horarios de actividad, patrones de uso) podrían revelar información sobre la rutina del propietario. |
| 🔐 **Integridad** | 🟢 **Baja** | Una alteración de los comandos del dispositivo afecta únicamente su funcionamiento físico local, sin comprometer registros corporativos. El riesgo se limita a molestias operativas del hogar. |
| ⚡ **Disponibilidad** | 🟢 **Baja** | La inoperabilidad de la conexión de red del electrodoméstico no tiene repercusión alguna sobre la continuidad del negocio o las actividades profesionales. |

#### ⚠️ Riesgo Indirecto Crítico

> [!WARNING]
> **Vector de Movimiento Lateral:** A pesar de su baja clasificación individual, los dispositivos IoT con firmware desactualizado son frecuentemente explotados como puntos de entrada (*pivot points*) para alcanzar activos de mayor valor en la misma red. Este riesgo se mitiga **exclusivamente** mediante segmentación de red (VLANs).

```
Amenaza                          Probabilidad    Impacto     Riesgo
─────────────────────────────────────────────────────────────────────
Explotación de firmware           ALTA           BAJO*       🟡 MEDIO*
  desactualizado
Uso como pivot para               MEDIA          CRÍTICO*    🟠 MEDIO*
  movimiento lateral
Botnet / DDoS participante        MEDIA          BAJO        🟡 BAJO
Interceptación de telemetría      BAJA           BAJO        🟢 BAJO

* El impacto se eleva a CRÍTICO si la red NO está segmentada.
```

---

## 🗺️ Mapa de Riesgos Consolidado

### Matriz de Calor de Riesgos (Probabilidad × Impacto)

```
IMPACTO →        BAJO          MEDIO         ALTO          CRÍTICO
─────────────────────────────────────────────────────────────────────
ALTA       │  IoT-Botnet   │             │             │ Laptop:     │
Probabilidad│              │             │             │ Phishing    │
           ├───────────────┼─────────────┼─────────────┼─────────────┤
MEDIA      │              │             │ NAS: Acceso  │ NAS:        │
           │              │             │ no autoriz.  │ Ransomware  │
           │              │             │ Laptop: 0day │ propagado   │
           ├───────────────┼─────────────┼─────────────┼─────────────┤
BAJA       │ IoT:         │ NAS:        │ NAS: Robo   │             │
           │ Telemetría   │ Corrupción  │ Laptop: Robo│             │
           │              │ silenciosa  │ físico      │             │
           └───────────────┴─────────────┴─────────────┴─────────────┘
                 🟢 BAJO       🟡 MODERADO    🟠 ALTO       🔴 CRÍTICO
```

### Resumen de Priorización

| Prioridad | Activo | Riesgo Dominante | Acción Inmediata |
|:---------:|:-------|:-----------------|:-----------------|
| **1** | Portátil de Desarrollo | Supply Chain Attack / Exfiltración | Cifrado total + MFA + EDR |
| **2** | Servidor NAS | Ransomware propagado / Backup Poisoning | Segmentación + Respaldos inmutables |
| **3** | Dispositivo IoT | Movimiento lateral | Aislamiento VLAN |

---

## 🔧 Recomendaciones Estratégicas de Hardening

Como analista senior, la identificación de activos es valiosa **únicamente** si se acompaña de controles proactivos. A continuación se detallan las acciones de mitigación organizadas por prioridad de implementación:

---

### 1. 🌐 Segmentación de Red (VLANs) — Prioridad: CRÍTICA

**Objetivo:** Eliminar la posibilidad de movimiento lateral entre activos de diferentes niveles de sensibilidad.

**Implementación:**

| VLAN | Nombre | Activos | Acceso Inter-VLAN |
|:----:|:-------|:--------|:-------------------|
| 10 | `VLAN_TRABAJO` | Portátil de Desarrollo, Servidor NAS | Permitido (controlado por ACL) |
| 20 | `VLAN_IOT_GUEST` | Electrodoméstico IoT, dispositivos de invitados | **Bloqueado** hacia VLAN 10 |

```
Reglas de Firewall Recomendadas (Pseudocódigo):
───────────────────────────────────────────────
ALLOW  VLAN_TRABAJO → Internet          [FILTRADO]
ALLOW  VLAN_TRABAJO → VLAN_TRABAJO      [PERMITIDO]
DENY   VLAN_IOT     → VLAN_TRABAJO      [BLOQUEADO]
ALLOW  VLAN_IOT     → Internet          [LIMITADO - Solo puertos necesarios]
DENY   VLAN_IOT     → VLAN_IOT          [AISLAMIENTO ENTRE DISPOSITIVOS]
LOG    ANY           → ANY              [REGISTRO COMPLETO]
```

> [!TIP]
> La mayoría de los routers empresariales de gama media-alta (como pfSense, OPNsense o MikroTik) soportan configuración de VLANs. En un entorno doméstico, un router con soporte para VLANs y un switch gestionable son inversiones de alto retorno en seguridad.

---

### 2. 🔒 Cifrado en Reposo — Prioridad: ALTA

**Objetivo:** Proteger la información contra accesos no autorizados derivados de robos físicos o accesos al hardware.

| Activo | Solución Recomendada | Algoritmo | Notas |
|:-------|:---------------------|:----------|:------|
| Portátil de Desarrollo | BitLocker (Windows) / LUKS (Linux) / FileVault (macOS) | AES-256-XTS | Activar TPM para arranque sellado. Almacenar clave de recuperación en ubicación segura **fuera del sitio**. |
| Servidor NAS | RAID cifrado (dm-crypt/LUKS) o cifrado nativo del NAS (Synology/QNAP) | AES-256 | Configurar desbloqueo automático por clave almacenada en HSM o dispositivo USB dedicado al arranque. |

> [!IMPORTANT]
> El cifrado en reposo **no protege** contra un atacante que obtenga acceso mientras el sistema está encendido y desbloqueado. Debe complementarse con políticas de bloqueo automático de pantalla (≤ 5 minutos de inactividad) y autenticación biométrica o por token.

---

### 3. 🔑 Autenticación Robusta y MFA — Prioridad: ALTA

**Objetivo:** Impedir el acceso no autorizado incluso si las credenciales son comprometidas.

**Controles recomendados:**

- **Llaves criptográficas físicas** (YubiKey, SoloKeys) para acceso SSH, consolas de administración y repositorios de código.
- **Autenticación multifactor (MFA)** basada en TOTP (aplicaciones como Aegis o Authy) para servicios en la nube y accesos remotos.
- **Gestión centralizada de credenciales** mediante un gestor de contraseñas offline o autoalojado (KeePassXC, Vaultwarden).
- **Rotación periódica** de tokens API y llaves SSH (mínimo cada 90 días).

```
Política de Autenticación Recomendada:
────────────────────────────────────────
Acceso al Portátil         → Biometría + PIN (arranque) + Contraseña (sesión)
Acceso SSH al NAS          → Llave SSH Ed25519 + Llave física FIDO2
Consola de Admin del Router→ Contraseña robusta (≥20 chars) + TOTP
Servicios Cloud (AWS/GCP)  → IAM con MFA obligatorio + Políticas de mínimo privilegio
```

---

### 4. 🛡️ Controles Complementarios Recomendados

| Control | Descripción | Activo(s) Aplicable(s) | Prioridad |
|:--------|:------------|:-----------------------|:---------:|
| **EDR/XDR** | Solución de detección y respuesta en endpoints para identificar comportamiento malicioso en tiempo real. | Portátil | 🔴 Alta |
| **Respaldos Inmutables** | Implementar respaldos con protección WORM (*Write Once Read Many*) o versionado inmutable. | NAS | 🔴 Alta |
| **Monitoreo de Red (IDS/IPS)** | Desplegar un sistema de detección de intrusiones (Suricata, Snort) en la interfaz del router. | Toda la red | 🟠 Media |
| **Actualizaciones Automatizadas** | Configurar actualizaciones automáticas de seguridad para el SO y software crítico. | Portátil, NAS | 🟠 Media |
| **DNS Seguro + Filtrado** | Utilizar un resolver DNS con filtrado de malware (Pi-hole + Unbound, NextDNS). | Toda la red | 🟡 Media |
| **Registro Centralizado (SIEM)** | Consolidar logs de todos los activos en un servidor centralizado para correlación de eventos. | Toda la red | 🟡 Media |
| **Escaneo de Vulnerabilidades** | Ejecutar escaneos periódicos (OpenVAS, Nessus Essentials) contra todos los activos. | Toda la red | 🟡 Media |

---

## 📐 Controles Alineados con Frameworks de la Industria

Las recomendaciones anteriores se mapean directamente a controles reconocidos internacionalmente:

| Recomendación | NIST CSF 2.0 | ISO 27001:2022 | CIS Controls v8 |
|:--------------|:-------------|:---------------|:-----------------|
| Inventario de Activos | **ID.AM-1, ID.AM-2** | A.5.9, A.5.10 | Control 1, 2 |
| Segmentación de Red | **PR.AC-5** | A.8.22 | Control 12.2 |
| Cifrado en Reposo | **PR.DS-1** | A.8.24 | Control 3.6 |
| Autenticación MFA | **PR.AC-7** | A.8.5 | Control 6.3, 6.4 |
| EDR / Monitoreo | **DE.CM-4** | A.8.7 | Control 10.1 |
| Respaldos Inmutables | **PR.IP-4** | A.8.13 | Control 11.2 |
| Gestión de Parches | **PR.IP-12** | A.8.8 | Control 7.4 |

---

## 📌 Conclusiones

1. **La gestión de activos no es un ejercicio pasivo**, sino un proceso continuo que debe revisarse ante cada cambio en la infraestructura (nuevo dispositivo, nueva conexión, cambio de proveedor).

2. **La Tríada CIA proporciona un marco objetivo** para priorizar inversiones de seguridad: los activos con puntuaciones altas en los tres pilares (como el Portátil de Desarrollo) deben recibir la mayor concentración de controles defensivos.

3. **Los dispositivos IoT representan un riesgo asimétrico**: individualmente son de bajo impacto, pero como vectores de pivoteo pueden comprometer activos de máxima criticidad si la arquitectura de red no contempla aislamiento.

4. **La defensa en profundidad es obligatoria, no opcional**: ningún control individual es suficiente. La combinación de segmentación + cifrado + autenticación robusta + monitoreo crea capas defensivas que obligan al atacante a superar múltiples barreras, incrementando exponencialmente el costo del ataque.

5. **La documentación y el inventario son controles de seguridad en sí mismos**: un activo no documentado es un activo no protegido.

---

## ⚖️ Disclaimer

> [!NOTE]
> **Documento de Portafolio Profesional**
> 
> Este documento ha sido elaborado con fines **demostrativos y educativos** para un portafolio profesional de ciberseguridad. Todos los datos, configuraciones, direcciones y escenarios presentados son **ficticios o han sido completamente anonimizados**.
> 
> - No se exponen credenciales, direcciones IP, nombres de dominio ni datos reales de infraestructura.
> - No se revelan vulnerabilidades explotables de sistemas en producción.
> - Las recomendaciones técnicas son genéricas y deben adaptarse al contexto específico de cada implementación.
> 
> **El autor no se responsabiliza del uso inadecuado de la información contenida en este documento.**

---

<div align="center">

**Elaborado por:** Analista Senior de Ciberseguridad  
**Fecha de Elaboración:** Julio 2026  
**Clasificación del Documento:** PÚBLICO  
**Versión:** 1.0  

---

*"La seguridad no es un producto, sino un proceso."* — **Bruce Schneier**

</div>
]]>
