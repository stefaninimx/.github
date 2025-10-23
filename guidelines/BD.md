# Lineamientos Estándar para el Nombramiento de Objetos en Bases de Datos

**Autor:** Equipo de Arquitectura de Datos  
**Versión:** 1.0  
**Última actualización:** 2025-10-23  

---

## 📘 Propósito

Este documento define los **estándares de nombramiento** para objetos de base de datos (tablas, columnas, índices, procedimientos, etc.) con el fin de:

- Promover la **consistencia** en los entornos de datos.  
- Mejorar la **legibilidad y mantenibilidad** del código SQL.  
- Facilitar la **automatización** y estandarización en herramientas de CI/CD y monitoreo.  
- Evitar **conflictos o ambigüedades** entre entornos y equipos.  

---

## ⚙️ Principios Generales

1. **Consistencia sobre creatividad:** usa un patrón uniforme antes que uno ingenioso.  
2. **Evitar nombres reservados:** no usar palabras reservadas del motor de base de datos (ej. `user`, `index`, `order`).  
3. **Usar inglés técnico estándar:** facilita la interoperabilidad y entendimiento global.  
4. **Usar `snake_case`:** palabras en minúsculas separadas por guiones bajos (`_`).  
5. **Evitar caracteres especiales:** no usar acentos, espacios, ni símbolos.  
6. **Nombres descriptivos y concisos:** preferiblemente entre 3 y 30 caracteres.  
7. **Prefijos y sufijos con propósito:** solo cuando agregan claridad.  

---

## 🧱 1. Estructuras Principales

### 1.1. Esquemas (`schema`)
- **Formato:** `business_domain` o `area_funcional`
- **Ejemplo:**  
  - `sales`, `finance`, `hr`, `marketing`

**Buenas prácticas:**
- Usar un esquema por dominio o contexto lógico.  
- Evitar el uso excesivo de esquemas por usuario o entorno.  

---

### 1.2. Tablas (`table`)
- **Formato:** `tbl_<entidad>_<contexto>` *(solo usar prefijo `tbl_` si el estándar del equipo lo requiere)*  
- **Ejemplo:**  
  - `customer_orders`  
  - `invoice_header`  
  - `employee_salary`

**Reglas:**
- Siempre usar plural si la tabla contiene múltiples registros del mismo tipo (`customers`, `orders`).  
- Evitar abreviaturas ambiguas (`cust`, `emp`).  
- Tablas de relación (muchos a muchos) se nombran concatenando entidades en orden alfabético:  
  - `customer_product` (no `product_customer`)  

---

### 1.3. Columnas (`column`)
- **Formato:** `nombre_significativo`  
- **Ejemplo:**  
  - `customer_id`, `order_date`, `amount_total`  

**Reglas:**
- Usar sufijos estandarizados:
  - `_id` → Identificador o llave foránea.  
  - `_date` → Campos de tipo fecha.  
  - `_flag` o `_indicator` → Booleanos (0/1).  
  - `_name`, `_desc`, `_type` → Campos textuales descriptivos.  
- Evitar prefijos con nombre de tabla (`customer.customer_id` ya es claro dentro del contexto).  
- Para booleanos, usar prefijos `is_` o `has_`:  
  - `is_active`, `has_discount`

---

### 1.4. Llaves Primarias (`primary key`)
- **Formato:** `pk_<tabla>`  
- **Ejemplo:**  
  - `pk_customer`  
  - `pk_invoice_header`

**Reglas:**
- Siempre con prefijo `pk_`.  
- Nombrar en base a la tabla, no al esquema.  

---

### 1.5. Llaves Foráneas (`foreign key`)
- **Formato:** `fk_<tabla>_<tabla_referenciada>`  
- **Ejemplo:**  
  - `fk_order_customer`  
  - `fk_payment_invoice`

**Reglas:**
- Consistencia entre nombre de constraint y campo relacionado.  
- No duplicar el sufijo `_id` en el nombre de la constraint.  

---

### 1.6. Índices (`index`)
- **Formato:** `ix_<tabla>_<columna>`  
- **Ejemplo:**  
  - `ix_customer_email`  
  - `ix_order_date`

**Reglas:**
- Si es un índice compuesto: `ix_<tabla>_<col1>_<col2>`  
  - Ejemplo: `ix_order_customer_date`  
- Si es único: usar prefijo `ux_` en lugar de `ix_`  
  - Ejemplo: `ux_customer_email`

---

### 1.7. Vistas (`view`)
- **Formato:** `vw_<descripcion>`  
- **Ejemplo:**  
  - `vw_sales_summary`  
  - `vw_customer_balance`

**Reglas:**
- Evitar lógica compleja en vistas sin documentación.  
- Prefijo `vw_` obligatorio.  

---

### 1.8. Procedimientos almacenados (`stored procedure`)
- **Formato:** `sp_<accion>_<entidad>`  
- **Ejemplo:**  
  - `sp_insert_customer`  
  - `sp_update_order_status`

**Acciones comunes:**  
`insert`, `update`, `delete`, `get`, `validate`, `sync`

---

### 1.9. Funciones (`function`)
- **Formato:** `fn_<descripcion>`  
- **Ejemplo:**  
  - `fn_get_customer_age`  
  - `fn_calculate_discount`

**Reglas:**
- Prefijo `fn_` obligatorio.  
- Nombres descriptivos que indiquen propósito y tipo de retorno.  

---

### 1.10. Triggers
- **Formato:** `trg_<tabla>_<accion>`  
- **Ejemplo:**  
  - `trg_order_after_insert`  
  - `trg_customer_before_update`

**Acciones comunes:** `insert`, `update`, `delete`

---

### 1.11. Secuencias (`sequence`)
- **Formato:** `seq_<tabla>_<columna>`  
- **Ejemplo:**  
  - `seq_order_order_id`

---

## 📦 2. Ambientes y Prefijos de Entorno

Cuando se administran múltiples entornos (dev, qa, prod), se recomienda **no incluir el entorno en el nombre del objeto**, sino mantenerlo a nivel de instancia o base de datos.  
**Evitar:** `customer_dev`, `customer_prod`  
**Usar:** `customer` (en base de datos `DB_Dev`, `DB_Prod`, etc.)

---

## 🔒 3. Convenciones por Tipo de Dato

| Tipo de Dato | Sufijo sugerido | Ejemplo |
|---------------|----------------|----------|
| Integer (ID)  | `_id`          | `customer_id` |
| String (nombre) | `_name` | `product_name` |
| Boolean | `is_` / `_flag` | `is_active`, `active_flag` |
| Fecha | `_date` | `start_date`, `created_date` |
| Decimal | `_amount` / `_value` | `total_amount` |
| Texto largo | `_desc` | `product_desc` |

---

## 🧩 4. Ejemplo Completo

```sql
CREATE TABLE sales.customer (
    customer_id SERIAL PRIMARY KEY,
    first_name VARCHAR(100) NOT NULL,
    last_name VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE,
    is_active BOOLEAN DEFAULT TRUE,
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE sales.orders (
    order_id SERIAL PRIMARY KEY,
    customer_id INT NOT NULL,
    order_date DATE NOT NULL,
    total_amount DECIMAL(10,2),
    CONSTRAINT fk_orders_customer FOREIGN KEY (customer_id) REFERENCES sales.customer(customer_id)
);

CREATE INDEX ix_orders_order_date ON sales.orders(order_date);
CREATE VIEW sales.vw_customer_orders AS
SELECT c.customer_id, c.first_name, c.last_name, o.order_date, o.total_amount
FROM sales.customer c
JOIN sales.orders o ON o.customer_id = c.customer_id;


