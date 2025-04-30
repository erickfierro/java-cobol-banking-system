# Hybrid COBOL & Java Banking System

proyecto de demostración que integra programas COBOL legacy con un backend Java moderno y un frontend web, simulando la autenticación Bancaria y la consulta de saldos y movimientos.

## Tabla de Contenidos

## Características
- Arquitectura
- Requisitos Previos
- Instalación
- Compilación y Ejecución
- Uso
- Estructura del Proyecto
- Tecnologías Utilizadas
- Contribuciones
- Licencia

## Características

- Autenticación COBOL: módulo `login.cbl` valida usuario y contraseña (hash SHA‑256) en un archivo secuencial `USUARIOS.DAT`.
- Servicios REST en Java: Spring Boot expone endpoints seguros `(/api/login, /api/accounts, /api/transactions)` e invoca programas COBOL vía `ProcessBuilder`.
- Frontend Web: UI ligera con Thymeleaf (o React opcional) que permite iniciar sesión, consultar saldo y ver movimientos.
- Docker & Docker Compose: entornos COBOL y Java completamente contenerizados para facilitar despliegue y pruebas.
- CI/CD: ejemplos de GitHub Actions para compilar COBOL, ejecutar tests y arrancar el servicio Java.

## Requisitos Previos

- Java 17+ y Maven 3.6+
- GnuCOBOL (version 3.1 o superior)
- Docker y Docker Compose
- Sistema operativo Linux, macOS o Windows con soporte POSIX

## Instalación

1. Clona el repositorio:
```bash
git clone https://github.com/tu-usuario/FinBridge.git
cd FinBridge
```
2. Prepara los archivos de usuarios y cuentas de ejemplo en `cobol/data`:
- `USUARIOS.DAT`: registros con usuario y hash SHA‑256 de la contraseña.
- `CUENTAS.DAT`: registros de número de cuenta, usuario y saldo.

3. Configura variables de entorno si es necesario (puedes usar .env).

## Compilación y Ejecución

Opción A: Local (sin Docker)

1. Compilar COBOL:
```bash
cd cobol
cobc -x login.cbl -o login
cobc -x accounts.cbl -o accounts
cobc -x transactions.cbl -o transactions
cd ..
```
2. Ejecutar Java:
```bash
cd java
mvn clean package
mvn spring-boot:run
```

Opción B: Con Docker Compose
```bash
docker-compose up --build
```
- El servicio Java quedará accesible en http://localhost:8080.
- El contenedor COBOL compilará programas al arrancar

## Estructura del Proyecto
```
FinBridge/
├─ cobol/
│  ├─ data/
│  │  ├─ USUARIOS.DAT
│  │  └─ CUENTAS.DAT
│  ├─ login.cbl
│  ├─ accounts.cbl
│  ├─ transactions.cbl
│  └─ Dockerfile.cobol
├─ java/
│  ├─ src/
│  │  ├─ main/java/com/finbridge/
│  │  │  ├─ security/    # Filtro de login y JWT
│  │  │  ├─ controllers/ # API REST
│  │  │  └─ services/    # Llamadas a COBOL
│  │  └─ main/resources/templates # Vistas Thymeleaf
│  └─ pom.xml
├─ docker-compose.yml
└─ README.md
```

## Tecnologías Utilizadas

- COBOL: GnuCOBOL para lógica de negocio y acceso a ficheros.
- Java: Spring Boot (Spring Security, Web).
- Frontend: Thymeleaf (opcional: React).
- Contenedores: Docker y Docker Compose.
- CI/CD: GitHub Actions.

## Contributions

Contributions are welcome! If you have ideas to improve this project or find any errors, do not hesitate to open an [issue](https://github.com/erickfierro/java-cobol-banking-system/issues) or send a [pull request](https://github.com/erickfierro/java-cobol-banking-system/pulls)
