# TP N°5: Instalación y Gestión de MariaDB en GitHub Codespaces

### 🎓 Cátedra: Prácticas Profesionalizantes II
**Carrera:** Tecnicatura Superior en Análisis de Sistemas (ISFT N°151)  
**Alumno:** Bravo, David Hernán  
**Docente:** Sandra Machado

---

## 📋 Descripción del Proyecto
Este trabajo práctico documenta la estabilización y configuración de un entorno de desarrollo basado en contenedores para el manejo de **MariaDB**. El objetivo central fue superar los fallos de automatización de Codespaces mediante una solución de **Infraestructura como Código (IaC)**, garantizando un entorno resiliente y listo para trabajar.

## 🛠️ Especificaciones del Entorno
Para que el entorno no dependa de factores externos, se implementó la siguiente arquitectura:

| Componente | Detalle Técnico |
| :--- | :--- |
| **Imagen Base** | Ubuntu (vía Dockerfile personalizado) |
| **Motor DB** | MariaDB Server |
| **Orquestador** | GitHub Codespaces |
| **Herramientas** | SQLTools & Driver MySQL/MariaDB |

## 🚀 Resolución Técnica: Del Fallo a la Estabilidad

### 1. El problema (Plan A)
Intenté la instalación mediante las *Features* automáticas del `devcontainer.json`. Sin embargo, el motor de Codespaces arrojó un **Error 1302**, fallando al conectar con el registro externo de contenedores.

### 2. La Solución (Plan B)
Decidí bajar un nivel y tomar el control total. Eliminé las dependencias de terceros y creé un **Dockerfile** propio. Ahora, MariaDB se instala directamente sobre la imagen base, asegurando que el software esté presente sí o sí.

### 3. Automatización del Ciclo de Vida
Configuré el `devcontainer.json` con comandos clave para evitar tareas manuales repetitivas:
* **`postCreateCommand`**: Se encarga de arrancar el servicio y crear la base de datos `dev_db` ni bien nace el contenedor.
* **`postStartCommand`**: Garantiza que el servicio de MariaDB se inicie automáticamente cada vez que retomás la sesión, eliminando el "olvido" típico de los servicios en la nube.

## 💻 Comandos de Supervivencia
Podés operar la base de datos directamente desde la terminal con:

```bash
# Entrar a la consola de MariaDB como superusuario
sudo mariadb

# Comandos rápidos:
SHOW DATABASES;       -- Listar bases de datos
USE dev_db;            -- Seleccionar la base de trabajo
SELECT user, host FROM mysql.user; -- Ver usuarios configurados