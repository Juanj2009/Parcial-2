# Parcial Corte 2 - Sistema de Inteligencia de Negocios: Cafetería U. Sabana
## Universidad de La Sabana - EICEA | Programación y Decisiones 2026-1

### Nombre Completo: [TU NOMBRE AQUÍ]

---

## Descripción

Proyecto de limpieza de datos, normalización (1NF, 2NF, 3NF) y migración a base de datos relacional SQLite para el sistema de la cafetería universitaria.

---

## Archivos del repositorio

```
parcial_2_productos_sucios.csv       <- Dataset original sucio
parcial_2_clientes_sucios.csv        <- Dataset original sucio
parcial_2_proveedores_sucios.csv     <- Dataset original sucio

parcial_2_productos_limpios.csv      <- Dataset procesado limpio
parcial_2_clientes_limpios.csv       <- Dataset procesado limpio
parcial_2_proveedores_limpios.csv    <- Dataset procesado limpio

parcial_2_cafeteria.db               <- Base de datos SQLite (4 tablas)
parcial_corte_2_cafeteria.ipynb      <- Código fuente documentado
README.md                            <- Este archivo
```

---

## Paso a paso de la solución

### FASE 1 - Generación de CSV sucios
Se generaron los 3 archivos CSV con datos sucios directamente desde Python, usando strings multilinea y la función `open()` para escribir los archivos.

### FASE 2 - Limpieza y Normalización con Pandas

**Productos:**
- 1NF: Se separó `producto_categoria` en `Nombre_Producto` y `Categoria` usando `str.split(' - ', expand=True)`
- Se eliminó el símbolo `$` de los precios y se convirtió a entero
- Se rellenaron los stocks nulos con 0

**Clientes:**
- 1NF: Se separó `cliente_tipo` en `Nombre_Cliente` y `Tipo_Cliente`
- 3NF: Se eliminó la columna `edad` por ser un dato derivado de `fecha_nacimiento`
- Se rellenaron emails y teléfonos nulos con 'No Registra'
- Se estandarizaron nombres con `.str.title()`

**Proveedores:**
- 1NF: Se separó `empresa_ciudad` en `Nombre_Empresa` y `Ciudad`
- Se rellenaron contactos, teléfonos y emails nulos con 'No Registra'

### FASE 3 - Migración a SQLite
Se conectó a `parcial_2_cafeteria.db` usando `sqlite3` y se cargaron los 3 DataFrames limpios con `df.to_sql()`, creando las tablas `productos`, `clientes` y `proveedores`.

### FASE 4 - Arquitectura SQL y CRUD
- Se habilitaron las Foreign Keys con `PRAGMA foreign_keys = ON`
- Se creó la tabla `ventas` con PK autoincremental y FK hacia las 3 tablas
- **INSERT**: 5 ventas insertadas con `INSERT INTO`
- **SELECT**: Reporte con `INNER JOIN` entre ventas, clientes y productos
- **UPDATE**: Actualización de cantidad y total_venta donde `id_venta = 1`
- **DELETE**: Eliminación del registro donde `id_venta = 3`
