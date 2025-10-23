# 🧭 Lineamientos Estándar para el Nombramiento de Objetos en Bases de Datos

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


# Lineamientos Estándar para el Nombramiento de Objetos en Bases de Datos 

## Introducción El nombramiento adecuado de objetos en bases de datos es crucial para mantener la claridad, la coherencia y la eficiencia en el desarrollo y mantenimiento de sistemas de gestión de bases de datos. 

Este documento ofrece lineamientos estandarizados para el nombramiento de objetos, basados en las mejores prácticas de la industria y la experiencia de expertos en administración de bases de datos (DBA). 

## Objetivos - Proporcionar claridad y legibilidad en el código. 

- Facilitar el mantenimiento y la escalabilidad de las bases de datos. 
- Establecer convenciones que sean fáciles de seguir y recordar. 

## Convenciones Generales 

### 1. Longitud de los Nombres 

- **Máximo 30 caracteres**: Aunque algunos sistemas permiten nombres más largos, es recomendable mantener los nombres dentro de esta longitud para garantizar compatibilidad y evitar truncamiento. 

### 2. Evitar Palabras Reservadas 

- No utilices palabras reservadas del sistema de gestión de bases de datos (DBMS) como nombres de objetos. Consulta la documentación del DBMS para conocer las palabras reservadas. 

### 3. Uso de Prefijos y Sufijos 

- **Prefijos**: Utiliza prefijos para indicar el tipo de objeto. Ejemplo: - `tbl_` para tablas. - `vw_` para vistas. - `sp_` para procedimientos almacenados. - **Sufijos**: Considera el uso de sufijos para indicar el estado o la versión. Ejemplo: - `_v1` para la primera versión. 

### 4. Uso de Notación 

- **Camel Case**: Utiliza la notación CamelCase para nombres compuestos. Ejemplo: `CustomerOrderDetails`. 
- **Snake Case**: Alternativamente, puedes usar snake_case para mayor legibilidad. Ejemplo: `customer_order_details`. 
- **Pascal Case**: Utiliza PascalCase para nombres de procedimientos y funciones. Ejemplo: `GetCustomerOrders`. 

### 5. Claridad y Descriptividad 

- Los nombres deben ser descriptivos y representar claramente el contenido o la función del objeto. Ejemplo: - `Customer` es mejor que `Cstmr`. - `GetCustomerOrders` es mejor que `GCO`. 

### 6. Uso de Abreviaciones 

- Evita el uso excesivo de abreviaturas. Si se utilizan, asegúrate de que sean comprensibles y de uso común en la industria. Ejemplo: `Qty` para cantidad es aceptable, pero `Ctmr` no es claro. 

## Nombres de Objetos Específicos 

### 1. Tablas - **Formato**: `tbl_<nombre_descriptivo>` - **Ejemplo**: - `tbl_Customer` - `tbl_Product` 

### 2. Vistas - **Formato**: `vw_<nombre_descriptivo>` - **Ejemplo**: - `vw_CustomerOrders` - `vw_ProductInventory` 

### 3. Procedimientos Almacenados - **Formato**: `sp_<nombre_descriptivo>` - **Ejemplo**: - `sp_GetCustomerOrders` - `sp_CalculateSalesTax` 

### 4. Funciones - **Formato**: `<nombreDescriptivo>Function` o `fn_<nombre_descriptivo>` - **Ejemplo**: - `CalculateDiscountFunction` - `fn_GetProductPrice` 

### 5. Índices - **Formato**: `idx_<nombre_tabla>_<columnas>` - **Ejemplo**: - `idx_Customer_LastName` - `idx_Product_Category_Price` 

### 6. Claves Primarias y Foráneas - **Primarias**: Usa el nombre de la tabla seguido de `_PK`. - Ejemplo: `Customer_PK`. - **Foráneas**: Usa el nombre de la tabla de referencia seguido de `_FK`. - Ejemplo: `Order_Customer_FK`. 

### 7. Triggers - **Formato**: `trg_<nombre_tabla>_<accion>` - **Ejemplo**: - `trg_Customer_AfterInsert` - `trg_Product_BeforeUpdate` 

### 8. Esquemas - **Formato**: `sch_<nombre_descriptivo>` - **Ejemplo**: - `sch_Sales` - `sch_Inventory` 

## Comentarios y Documentación 

- Siempre documenta el propósito de los objetos en comentarios. Esto ayuda a los futuros desarrolladores a entender mejor la estructura y el propósito de la base de datos. ```sql -- Esta tabla almacena información sobre los clientes CREATE TABLE tbl_Customer ( CustomerID INT PRIMARY KEY, FirstName VARCHAR(50), LastName VARCHAR(50) );
