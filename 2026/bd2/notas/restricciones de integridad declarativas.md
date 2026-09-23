RI:
- condiciones que restringen los posibles valores validos de datos en la BD
- importante: identificar e incorporar las RI que deben cumplirse
- el SGBD controla las operaciones sobre los datos para garantizar el cumplimiento de las RI
	- rechazando operaciones (altas, bajas, modificaciones)
	- realizando acciones reparadoras sobre los datos
ambas respuestas deben dejar la bd en un estado consistente

# clasificacion de RI
segun su naturaleza
- RI inherentes - implicitas
	- propias del modelo relacional, no necesitan declararse
- RI explicitas:
	- se especifican en el esquima de la BD mediante sentencias del DDL
		- ej: restricciones de dominio, clave, nulidad, integridad referencial
- RI semanticas (reglas del negocio):
	- restricciones adicionales segun la logica de la organizacion (planteadas en forma declarativa o procedural) -> **triggers**


segun estados involucrados
- RI de estado: restringen los valores de los datos en un momento dado
	- nulidad: el valor de un atributo puede o no ser nulo
	- dominio: valores permitidos para un atributo
	- cardinalidad: cantidad de participaciones de una entidad en una relacion
	- participacion: puede ser obligatoria u opcional
- RI de transicion: **controlan cambios entre estados sucesivos**
	- requieren conocer el estado "anterior" y "nuevo"
	- no pueden plantearse en forma declarativa sino procedural (triggers)
***los triggers son RI's semanticas o de transicion***

RI referencial (RIR's)
- condiciones sobre los valores de las claves extranjeras - foreign keys (FK)
- el conjunto de valores de una FK en una relacion R debe existir como clave primaria (o alternativa) en una relacion R' a la que FK hace referencia, o ser nulos

ON UPDATE accionRef
ON DELETE accionRef
- es el comportamiento ante borrado o modificacion de datos referenciados

## acciones referenciales (delete)
al intentar borrar una tupla referenciada en R'
hay dos caminos
- rechaza la operacion
	- NO ACTION: impide borrar la tupla referenciada en R' si hay referencias en R(default en SQL estandar y postgreSQL)
	- RESTRICT: misma semantica pero se chequea antes de otras RI
- procede y realiza acciones reparadoras adicionales
	- CASCADE: borra la tupla referenciada en R' y propaga el borrado a las tuplas de R que la referenciaban mediante la FK
	- SET NULL: borra la tupla referenciada en R' y las tuplas que la referenciaban en R ponen a nulo la FK (si admite nulos)
	- SET DEFAULT: borra la tupla referenciada en R' y las tuplas que la referenciaban ponen en la FK el valor por defecto definido para la misma

## acciones referenciales (update)
al intentar actualizar una tupla referenciada en R'
hay dos caminos
- rechaza la operacion
	- NO ACTION: no permite modificar el valor de la clave en la tupla referenciada en R' **si hay referencias en R (opcion por default)**
	- RESTRICT: misma semantica pero se chequea antes de otras RI
- procede y realiza acciones reparadoras adicionales
	- CASCADE: modifica el valor de la tupla referenciada en R' y propaga en R la modificacion a las tuplas de R que la referenciaban
	- SET NULL: modifica la tupla referenciada en R' y las tuplas que la referenciaban en R ponen a nulo la FK (si admite nulos)
	- SET DEFAULT: modifica la tupla referenciada en R' y las tuplas que la referenciaban ponen en la FK el valor por defecto definido para la misma

### diferencia RESTRICT/NO ACTION
tienen la misma semantica básica (rechazar si hay referencias), **pero varia el momento de la verificacion**:
- **RESTRICT**: se chequea inmediatamente al inicio de la operacion. Si detecta la referencia, rechaza de inmediato y no permite que se ejecuten otras acciones en cascada ni modificaciones.
- **NO ACTION**: se chequea al final de la sentencia (o diferido al commit). Si otra regla referencial (ej: un `CASCADE` en otra tabla) o acción previa elimina las referencias antes de finalizar, la operación puede completarse sin violar la restricción.

# matching
aplica cuando la FK es **compuesta** y sus atributos **admiten nulos**.
sintaxis: `[ MATCH { SIMPLE | PARTIAL | FULL } ]`

condicion general: una RIR se satisface si ningun valor de la FK es null y coincide con la PK/clave referenciada, o si hay nulos segun la estrategia:

tipos de matching
- **MATCH SIMPLE** (default en SQL):
	- si **al menos una columna de la FK es NULL**, se da por satisfecha la restriccion (no valida el resto de columnas no nulas).
	- solo valida existencia en la tabla referenciada si **todas** las columnas son no nulas.
- **MATCH PARTIAL**:
	- los componentes **no nulos** de la FK deben coincidir con los correspondientes valores de clave de **al menos una tupla** en la tabla referenciada.
	- si todos son null, pasa.
- **MATCH FULL**:
	- **todo o nada**: o todas las columnas de la FK son nulas, o ninguna lo es (y debe existir en la tabla referenciada).
	- no admite mezclas de valores no nulos con nulos en la FK.

### ejemplo practico
tabla referenciada: `AREA(idArea, tipoA)` con tuplas: `(1, 'T1')`, `(1, 'T2')`, `(2, 'T1')`

| alta en `PROYECTO(idArea, tipoA)` | SIMPLE | PARTIAL | FULL | motivo |
|---|:---:|:---:|:---:|---|
| `(1, 'T1')` | OK | OK | OK | clave completa y existe |
| `(2, 'T2')` | X | X | X | clave completa pero no existe tupla con ese par |
| `(NULL, NULL)` | OK | OK | OK | todos nulos |
| `(NULL, 'T1')` | OK | OK | X | SIMPLE pasa por tener un null; PARTIAL pasa porque existe tupla con `tipoA = 'T1'`; FULL rechaza mezclas |
| `(3, NULL)` | OK | X | X | SIMPLE pasa por tener un null; PARTIAL rechaza porque no existe tupla con `idArea = 3`; FULL rechaza mezclas |

# restricciones de integridad declarativas segun SQL estandar
el estandar SQL permite la especificacion declarativa de RI de distinto tipo segun la jerarquia del modelo relacional:
- **atributo / dominio** (`DOMAIN` o `CHECK` de columna)
- **tupla** (`CHECK` de tupla)
- **tabla** (`CHECK` de tabla)
- **generales / BD** (`ASSERTION`)

### caracteristicas y comportamiento del SGBD
- **control continuo**: el SGBD valida su cumplimiento en todo momento ante operaciones DML (INSERT, UPDATE, DELETE).
- **atomicidad**: si alguna RI no se cumple, la operacion se rechaza completa (sin efectos parciales).
- **evaluacion trivalente**: una RI se cumple si la condicion evalua a `TRUE` o `UNKNOWN` (por presencia de nulos). Solo se rechaza si evalua a `FALSE`.
- **validacion inicial**: al declararse (`CREATE TABLE` o `ALTER TABLE`), el SGBD comprueba los datos existentes; si alguno viola la regla, rechaza la definicion de la RI.
- los nombres de las restricciones (`CONSTRAINT`) deben ser unicos dentro del esquema.

---

## 1. RI de atributo / dominio
define el conjunto de valores validos para un atributo individual.
- **en `CREATE TABLE`** (asociado a la columna):
```sql
CREATE TABLE empleado (
    idE INT PRIMARY KEY,
    sueldo DECIMAL(10,2) CONSTRAINT sueldo_pos CHECK (sueldo > 0)
);
```
- **mediante `CREATE DOMAIN`** (util para abstraer y reutilizar el tipo y sus reglas en varias tablas):
```sql
CREATE DOMAIN SueldoPos AS DECIMAL(10,2)
    CHECK (VALUE > 0);

CREATE TABLE empleado (
    idE INT PRIMARY KEY,
    sueldo SueldoPos
);
```

---

## 2. RI de tupla (CHECK de tupla)
restringe la combinacion de valores entre dos o mas atributos de una **misma fila**.
- **ambito**: tupla (se comprueba para cada fila insertada o modificada).
```sql
-- ej: salvo para empleados del proyecto 101, el premio no puede superar el 25% del sueldo
ALTER TABLE empleado
ADD CONSTRAINT chk_premio
CHECK (proy = 101 OR premio <= 0.25 * sueldo);
```

---

## 3. RI de tabla (CHECK de tabla)
involucra y restringe **multiples tuplas de la misma tabla**.
- **ambito**: tabla (se comprueba cada vez que se actualiza la tabla).
- en SQL "todo X cumple C" se expresa formalmente como: **"no existe ningun X que no cumpla C"** (`NOT EXISTS`).
```sql
-- ej: en cada proyecto pueden trabajar hasta 10 empleados
ALTER TABLE empleado
ADD CONSTRAINT chk_cant_empl
CHECK (NOT EXISTS (
    SELECT proy
    FROM empleado
    GROUP BY proy
    HAVING COUNT(*) > 10
));
```
> si la subconsulta devuelve filas (proyectos con >10 empleados), `NOT EXISTS` devuelve `FALSE` y la operacion se rechaza.

---

## 4. RI generales de la BD (ASSERTION)
restricciones sobre atributos de **dos o mas tablas** distintas.
- **ambito**: base de datos completa (no pertenece a una tabla en particular).
- **sintaxis estandar**:
```sql
-- ej: el sueldo de cada empleado no puede superar el presupuesto del proyecto donde trabaja
CREATE ASSERTION sueldo_menor_presup
CHECK (NOT EXISTS (
    SELECT 1
    FROM empleado e
    JOIN proyecto p ON e.proy = p.idProy
    WHERE e.sueldo > p.presupuesto
));
```
- **nota practica / de examen**: tendria un costo computacional altisimo al tener que verificarse ante cualquier cambio en cualquier tabla involucrada. Por eso **NO esta implementada en los SGBD relacionales reales (PostgreSQL, Oracle, MySQL, SQL Server)**.

---

## tiempo de verificacion (deferrable vs not deferrable)
determina en que momento de la transaccion se comprueba la restriccion:
- **`NOT DEFERRABLE`** (default): se verifica inmediatamente despues de ejecutar cada sentencia individual.
- **`DEFERRABLE`**: permite postergar la comprobacion hasta el final de la transaccion (`COMMIT`).
    - `INITIALLY IMMEDIATE`: por default chequea por sentencia, pero permite diferir con `SET CONSTRAINTS`.
    - `INITIALLY DEFERRED`: chequea automaticamente al final de la transaccion (`COMMIT`).
    - *caso de uso tipico*: referencias circulares entre tablas o cargas masivas donde los estados intermedios violan temporalmente la FK.

---

## alternativa: SQL procedural (triggers)
cuando las restricciones no pueden implementarse de forma declarativa:
- porque no se soportan `ASSERTION` ni subconsultas complejas en `CHECK`.
- porque son **RI de transicion** (requieren conocer y comparar el estado anterior `OLD` y nuevo `NEW`).
- porque se requiere ejecutar logica correctiva o validaciones dinamicas avanzadas.

**recursos PL/pgSQL / PL/SQL**:
- **Triggers**: bloques de codigo que se disparan automaticamente ante eventos DML (`BEFORE` / `AFTER` en `INSERT`, `UPDATE`, `DELETE`).
- **Stored Procedures / Functions**: logica encapsulada invocable explicitamente o desde triggers.

