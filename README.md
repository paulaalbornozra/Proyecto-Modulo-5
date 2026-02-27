# 💳 AlkeWallet — Base de Datos MySQL

Proyecto de módulo 5: diseño, implementación y manipulación de una base de datos relacional para una billetera digital, desarrollado con **MySQL 8**.

---

## 📋 Descripción

AlkeWallet es una base de datos relacional que simula el backend de datos de una billetera digital. Permite gestionar usuarios, monedas y transacciones entre cuentas, aplicando buenas prácticas de modelado relacional, integridad referencial y transaccionalidad ACID.

---

## 🗂️ Estructura de la Base de Datos

El modelo relacional está compuesto por tres tablas principales:

### `moneda`
Almacena las divisas disponibles en el sistema.

| Campo             | Tipo         | Descripción                  |
|-------------------|--------------|------------------------------|
| `currency_id`     | INT (PK, AI) | Identificador único           |
| `currency_name`   | VARCHAR(60)  | Nombre de la moneda           |
| `currency_symbol` | VARCHAR(10)  | Símbolo (ej. CLP, USD, EUR)  |

### `usuario`
Contiene la información de los usuarios registrados y su saldo actual.

| Campo            | Tipo           | Descripción                          |
|------------------|----------------|--------------------------------------|
| `user_id`        | INT (PK, AI)   | Identificador único                   |
| `nombre`         | VARCHAR(100)   | Nombre completo                       |
| `correo`         | VARCHAR(150)   | Correo electrónico (único)            |
| `contrasena`     | VARCHAR(255)   | Contraseña hasheada (SHA-256)         |
| `saldo`          | DECIMAL(15,2)  | Saldo disponible                      |
| `currency_id`    | INT (FK)       | Moneda asociada al usuario            |
| `fecha_creacion` | DATETIME       | Fecha y hora de registro              |

### `transaccion`
Registra cada movimiento de dinero entre usuarios.

| Campo              | Tipo          | Descripción                          |
|--------------------|---------------|--------------------------------------|
| `transaction_id`   | INT (PK, AI)  | Identificador único                   |
| `sender_user_id`   | INT (FK)      | Usuario remitente                     |
| `receiver_user_id` | INT (FK)      | Usuario destinatario                  |
| `importe`          | DECIMAL(15,2) | Monto de la transacción               |
| `transaction_date` | DATETIME      | Fecha y hora de la transacción        |

---

## ⚙️ Requisitos

- MySQL 8.0 o superior
- Cliente MySQL (MySQL Workbench, DBeaver, CLI, etc.)

---

## 🚀 Instalación y Uso

1. Clona este repositorio:
   ```bash
   git clone https://github.com/tu-usuario/Proyecto-Modulo-5.git
   ```

2. Abre tu cliente MySQL y ejecuta el script completo:
   ```bash
   mysql -u root -p < AlkeWallet_DB.txt
   ```

3. Verifica que la base de datos fue creada correctamente:
   ```sql
   USE AlkeWallet;
   SHOW TABLES;
   ```

---

## 🔍 Consultas Incluidas

El script contempla las siguientes operaciones:

- **DDL:** Creación de tablas con claves primarias, foráneas e índices.
- **DML (INSERT):** Carga inicial de datos de prueba (5 monedas, 5 usuarios, 6 transacciones).
- **SELECT:** Consultas con `JOIN`, `CASE`, subconsultas y vistas.
- **UPDATE / DELETE:** Modificación de correos, eliminación de transacciones y actualización de saldos.
- **Transaccionalidad ACID:** Ejemplos con `START TRANSACTION`, `COMMIT` y `ROLLBACK`.
- **Agregaciones:** `COUNT`, `SUM`, `GROUP BY` para estadísticas por usuario.

### Vista destacada — Top 5 usuarios con mayor saldo
```sql
SELECT * FROM vw_top5_saldo;
```

---

## 🔐 Seguridad

Las contraseñas de los usuarios se almacenan hasheadas utilizando el algoritmo **SHA-256** mediante la función nativa de MySQL `SHA2()`, evitando el almacenamiento de texto plano.

---

## 📁 Archivos del Repositorio

```
Proyecto-Modulo-5/
├── AlkeWallet_DB.txt   # Script SQL completo (DDL + DML + consultas)
├── AlkeWallet_SQL.docx # Documentación del proyecto en formato Word
└── README.md           # Documentación del proyecto
```

---

## 👤 Autora

**Paula Albornoz Ramos**
Módulo 5: Fundamentos de Bases de Datos Relacionales.