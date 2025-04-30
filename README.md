# Hybrid COBOL & Java Banking System

proyecto de demostración que integra programas COBOL legacy con un backend Java moderno y un frontend web, simulando la autenticación Bancaria y la consulta de saldos y movimientos.

Tabla de Contenidos

Características
Arquitectura
Requisitos Previos
Instalación
Compilación y Ejecución
Uso
Estructura del Proyecto
Tecnologías Utilizadas
Contribuciones
Licencia

Características

Autenticación COBOL: módulo login.cbl valida usuario y contraseña (hash SHA‑256) en un archivo secuencial USUARIOS.DAT.
Servicios REST en Java: Spring Boot expone endpoints seguros (/api/login, /api/accounts, /api/transactions) e invoca programas COBOL vía ProcessBuilder.
Frontend Web: UI ligera con Thymeleaf (o React opcional) que permite iniciar sesión, consultar saldo y ver movimientos.
Docker & Docker Compose: entornos COBOL y Java completamente contenerizados para facilitar despliegue y pruebas.
CI/CD: ejemplos de GitHub Actions para compilar COBOL, ejecutar tests y arrancar el servicio Java.
