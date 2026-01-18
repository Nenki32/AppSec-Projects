# 🛡️ Cybersecurity

Aquí documento proyectos enfocados en la detección de amenazas, remediación de vulnerabilidades y la implementación de soluciones de seguridad defensiva (Blue Team).

🚀 Proyecto Destacado: Detección de Secretos con Nosey Parker (AppSec)

📋 Descripción

Implementación de un flujo de auditoría técnica para la identificación de credenciales hardcodeadas (secrets), tokens de API y llaves privadas en entornos de desarrollo y sistemas de archivos.

Herramientas: Nosey Parker, WSL (Ubuntu Linux), Git.

Enfoque: Prevención de fugas de información (Secret Leaks) y Hardening de repositorios.

⚠️ El Problema

En el ciclo de vida del desarrollo de software, es crítico evitar que credenciales sensibles lleguen a repositorios o entornos productivos. Las llaves hardcodeadas son uno de los vectores más utilizados por atacantes para realizar movimientos laterales y exfiltración de datos.

🛡️ Riesgo Identificado

Impacto: Compromiso de infraestructura cloud (AWS/Azure), acceso no autorizado a bases de datos y exposición de servicios de terceros.

Criticidad: Alta (basado en el potencial de escalada de privilegios).

🛠️ Acción Técnica 

1. Preparación del Entorno WSL2

Se configuró un entorno WSL ,Windows Subsystem for Linux, utilizando la distribución Ubuntu para ejecutar herramientas de seguridad nativas de Linux en un host Windows, garantizando compatibilidad y rendimiento.

2. Despliegue de Nosey Parker

Instalación y configuración de la herramienta para escaneo de alta velocidad basado en entropía:

Instalación de Nosey Parker en WSL
wget [https://github.com/praetorian-inc/noseyparker/releases/latest/download/noseyparker_x86_64.zip](https://github.com/praetorian-inc/noseyparker/releases/latest/download/noseyparker_x86_64.zip)
unzip noseyparker_x86_64.zip
chmod +x noseyparker
sudo mv noseyparker /usr/local/bin/

3. Proceso de Auditoría

Ejecución de escaneos profundos sobre repositorios locales buscando patrones de secretos conocidos (Live Secrets) y firmas de proveedores:

# Escaneo de un directorio o repositorio
noseyparker scan --datastore my_secrets_db /ruta/al/proyecto
# Reporte de hallazgos
noseyparker report --datastore my_secrets_db


✅ Resultado y Remediación

Detección: Se identifican tokens de API y claves privadas en archivos de configuración de entornos de prueba.

Remediación Realizada: Se procede a la rotación inmediata de secretos (invalidación y generación de nuevos tokens) y la limpieza del historial de Git mediante herramientas de reescritura de commits.

Prevención: Se implementaron recomendaciones de uso de .gitignore y sugerencias de integración de pre-commit hooks para automatizar la detección antes del push al repositorio.
