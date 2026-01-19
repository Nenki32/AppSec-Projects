# 🛡️ Cybersecurity

Aquí documento proyectos enfocados en la detección de amenazas, remediación de vulnerabilidades y la implementación de soluciones de seguridad defensiva (Blue Team).

# 🚀Gobernanza y Gestión del SIEM (Ecosistema Wazuh)

Enfoque: Monitoreo centralizado (HIDS) y automatización de la flota de agentes.

1.1 Actualización y Escalabilidad del Stack (Manager/Indexers)

Problema: Desfase de versiones entre el Wazuh Manager y los Indexers, generando inconsistencias en el parseo de logs y pérdida de compatibilidad con nuevas reglas.

Riesgo: Degradación de la visibilidad y exposición del SIEM a vulnerabilidades no parcheadas.

Acción Técnica: Ejecución de Upgrading Path jerárquico (Indexer -> Server -> Dashboard) con snapshots preventivos. Implementación de actualizaciones remotas de agentes mediante paquetes WPK (Wazuh Packages), eliminando la necesidad de intervención manual por SSH/RDP.

Resultado: Disponibilidad del 99.9% durante mantenimiento y estandarización total de versiones.

1.2 Configuración de Políticas y Segmentación (SCA)

Problema: Políticas de monitoreo genéricas que generaban carga innecesaria en servidores con distintos roles (Web vs DB).

Acción Técnica: Configuración de agent.conf centralizados segmentados por etiquetas. Despliegue de políticas de Security Configuration Assessment (SCA) para verificar el hardening del SO en tiempo real (NIST/CIS).

Resultado: Precisión en las alertas según el perfil de riesgo y reducción drástica del ruido en los logs.

1.3 Optimización de FIM (File Integrity Monitoring)

Problema: Fatiga de alertas (Alert Fatigue) por cambios legítimos en archivos temporales detectados por el módulo syscheck.

Acción Técnica: Implementación de monitoreo en tiempo real vía inotify (Linux) y ReadDirectoryChangesW (Windows). Optimización de bloques <ignore> quirúrgicos y activación de check_all="yes" solo en rutas de configuración crítica.

Resultado: Reducción del 90% en falsos positivos, permitiendo foco total en cambios no autorizados en binarios de sistema.

# 💻Gestión de Vulnerabilidades y Remediación (AppSec)

Enfoque: Ciclo de vida completo del riesgo y defensa en profundidad.

2.1 Ciclo de Vida de la Remediación

Metodología: Detección (Vulnerability Detector) -> Validación manual (PoC) -> Re-cálculo de criticidad (CVSS) -> Remediación -> Verificación (Rescan).

Resultado: Establecimiento de un SLA de remediación para vulnerabilidades Críticas/Altas y reducción medible del riesgo acumulado.

2.2 Mitigación CVE-2025-13836 (DoS en Python)

Problema: Detección de vulnerabilidad en el módulo http.client de Python 3.12.3 en estaciones de trabajo.

Riesgo: Denegación de Servicio (DoS) por agotamiento de memoria virtual al procesar respuestas maliciosas.

Acción Técnica: Validación del uso de la versión vulnerable y actualización forzada al intérprete 3.14.2 (parche de diciembre 2025).

Hardening Adicional: Implementación de límites de lectura en el parámetro amount de la función .read() como medida de defensa en profundidad.

Resultado: Eliminación total del vector de ataque y cierre formal de la alerta en el SIEM.

# 🔑Detección de Secretos con Nosey Parker

Enfoque: Prevención de fuga de credenciales (Secrets Leaks) en entornos de desarrollo.

Implementación: Uso de Nosey Parker sobre WSL (Ubuntu Linux) para escaneo de alta velocidad basado en entropía.

Acción: Auditoría de repositorios locales buscando tokens de API, llaves privadas y "Live Secrets".

Remediación: Rotación de credenciales expuestas y limpieza de historial mediante herramientas de reescritura de commits.

Prevención: Configuración de .gitignore y recomendación de pre-commit hooks.

# 🎯Security Awareness & Ingeniería Social

Acción: Diseño de campañas de simulación de Phishing y cursos de capacitación interna.

Resultado: Mejora medible en la tasa de reporte de correos sospechosos y fortalecimiento de la cultura de seguridad
