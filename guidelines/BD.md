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
