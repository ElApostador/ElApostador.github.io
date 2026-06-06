# Auditoría de Seguridad y Cumplimiento (ISO 27001/2 & GDPR)

**Headline:** Diseño, ejecución y gestión de auditoría interna de controles lógicos y físicos para evaluar la madurez operativa y mitigar riesgos normativos.

---

### 1. El Desafío (Contexto de Auditoría)
La organización requería evaluar su postura de seguridad actual frente a amenazas crecientes (como incidentes de Ransomware y fugas de datos), buscando estructurar sus procesos internos bajo un marco normativo reconocido internacionalmente (ISO 27001) para garantizar la Confidencialidad, Integridad y Disponibilidad de sus activos.

### 2. La Acción (Ejecución del Plan Integral)
Se diseñó un plan de auditoría integral orquestado mediante tableros ágiles (Trello), segmentando la revisión en los dominios críticos de la norma ISO 27001:

* **Inventario y Clasificación de Activos (A.5 y A.8):** Relevamiento exhaustivo de hardware, software y mapeo topológico básico de red. Se identificaron y clasificaron los Datos de Carácter Personal (PII) bajo criterios GDPR.
* **Gestión de Identidad y Accesos - IAM (A.9):** Auditoría de usuarios, roles y permisos bajo el **Principio de Mínimo Privilegio**. Se revisaron políticas de contraseñas, implementación de Autenticación Multifactor (MFA) y procesos de desvinculación (revocación de accesos a ex-empleados).
* **Seguridad Física y Ambiental (A.11):** Inspección de los controles de acceso al cuarto de servidores (barreras, CCTV, sistemas UPS, controles ambientales) y revisión de prácticas de escritorio limpio (protección de documentos físicos y Custodia de Evidencia Legal).
* **Gestión de Incidentes y Continuidad (A.17):** Formulación de borradores y lineamientos para un Plan de Respuesta ante Incidentes (IRP) frente a robos y un Plan de Continuidad de Negocio (BCP) en caso de desastres físicos (incendios).

### 3. El Impacto (Resultados y Gobernanza)
La auditoría permitió visibilizar el nivel de madurez real del Sistema de Gestión de Seguridad de la Información (SGSI). A través de la elaboración de una matriz de riesgos (Probabilidad x Impacto), se logró priorizar las vulnerabilidades críticas y trazar un plan de acción (*roadmap*) para la remediación de brechas técnicas y procedimentales.

---

### 📋 Muestra de Gestión Documental (Tablero de Auditoría)

*(Nota: En un entorno de auditoría real, el registro estructurado de la evidencia es tan crítico como el hallazgo en sí).*

**Dominios Evaluados (Fragmento):**
1. **Controles Físicos:** ¿Quién ingresa al servidor? / Presencia de CCTV / Políticas de escritorio limpio.
2. **Roles y Accesos:** Control de carpetas compartidas / Detección de cuentas huérfanas / Implementación MFA.
3. **GDPR / Riesgo de PII:** Identificación de métodos de respaldo / Evaluación de canales de transmisión (Cifrado vs. Envío por mail en texto plano).

---
**Marcos y Estándares Aplicados:** *ISO/IEC 27001:2022 | ISO/IEC 27002 | GDPR | Gestión de Riesgos | Defensa en Profundidad | Controles Lógicos (MAC/DAC/RBAC).*
