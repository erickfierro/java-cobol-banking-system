# Hybrid COBOL & Java Banking System

Proyecto de demostración que integra programas COBOL legacy con un backend Java moderno y un frontend web construido con Tailwind CSS, simulando la autenticación bancaria y la consulta de saldos y movimientos usando bases de datos en lugar de archivos planos.

## Tabla de Contenidos

- [Características](#características)
- [Requisitos Previos](#requisitos-previos)
- [Instalación](#instalación)
- [Compilación y Ejecución](#compilación-y-ejecución)
- [Estructura del Proyecto](#estructura-del-proyecto)
- [Tecnologías Utilizadas](#tecnologías-utilizadas)
- [Contribuciones](#contributions)

## Características

- Autenticación COBOL con DB: módulo `login.cbl` valida usuario y contraseña (hash SHA-256) en la tabla `USUARIOS` de una base de datos relacional.
- Servicios REST en Java: Spring Boot expone endpoints seguros `(/api/login, /api/accounts, /api/transactions)` e invoca programas COBOL vía `ProcessBuilder`.
- Frontend Web con Tailwind: interfaz responsiva y moderna, separada en web/ con Node.js y PostCSS.
- Base de datos relacional: PostgreSQL (o DB2/Oracle) para almacenar usuarios, cuentas y transacciones.
- Docker & Docker Compose: orquesta contenedores de COBOL, Java, frontend y base de datos.
- CI/CD: GitHub Actions para compilar COBOL, construir frontend, ejecutar tests y desplegar servicios.

## Requisitos Previos

- Java 17+ y Maven 3.6+
- GnuCOBOL (version 3.1 o superior)
- Docker y Docker Compose
- Node.js 14+ y npm/yarn
- PostgreSQL (o DB2/Oracle) accesible desde la red
- Sistema operativo Linux, macOS o Windows con soporte POSIX

## Instalación

1. Clona el repositorio:
```bash
git clone https://github.com/tu-usuario/FinBridge.git
cd FinBridge
```
2. Configura la base de datos:
- Crea una BD finbridge y un usuario con privilegios.
- Ejecuta el script SQL en db/init.sql para crear tablas USUARIOS, CUENTAS y TRANSACCIONES.

3. Configura variables de entorno si es necesario (puedes usar .env).

4. Ajusta variables de entorno en .env:
```bash
DB_URL=jdbc:postgresql://db:5432/finbridge
DB_USER=fin_usr
DB_PASS=fin_pass
```

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
│  │  │  ├─ security/    # Filtro login, JWT
│  │  │  ├─ controllers/ # API REST
│  │  │  ├─ services/    # Invocaciones COBOL
│  │  └─ main/resources/static/  # se despliega web/dist
│  └─ pom.xml
├─ web/
│  ├─ src/
│  │  ├─ index.html
│  │  └─ styles/
│  │      └─ input.css
│  ├─ tailwind.config.js
│  ├─ postcss.config.js
│  ├─ package.json
│  └─ dist/             # artefacto tras npm run build
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
