# Gestor de tareas en PHP

Aplicación web pequeña para practicar persistencia, operaciones CRUD, validación de datos y separación básica entre comandos y consultas.

## Requisitos

- Laravel Herd para Windows.
- PHP 8.1 o superior administrado por Herd.
- Extensión PDO SQLite habilitada.
- Navegador web.

El proyecto utiliza PHP puro y no requiere el framework Laravel. Herd proporciona PHP, nginx y el dominio local `.test`. No necesita XAMPP, Composer, Node.js ni un servidor de base de datos independiente.

## Preparación con Laravel Herd

1. Inicie la aplicación Laravel Herd y confirme que se encuentra activa.
2. Abra PowerShell en la carpeta del proyecto y compruebe PHP:

```bash
herd php -v
```

3. Entre en la carpeta pública y registre el sitio en Herd:

```bash
cd public
herd link gestor-tareas-s13
```

4. Después abra en el navegador:

```text
http://gestor-tareas-s13.test
```

La carpeta `public` se enlaza como raíz del sitio, mientras que `config`, `src` y `database` permanecen fuera del acceso web directo. La carpeta `database` y el archivo `tareas.sqlite` se crean automáticamente al abrir la aplicación.

Para retirar el enlace local al finalizar:

```bash
herd unlink gestor-tareas-s13
```

También puede agregar la carpeta `public` desde la interfaz de Herd como un sitio existente y asignarle el nombre `gestor-tareas-s13`.

## Funcionalidades

- Crear tareas.
- Listar y filtrar por estado o prioridad.
- Consultar el detalle.
- Actualizar tareas.
- Eliminar tareas.
- Validar título, descripción, prioridad y estado.
- Controlar identificadores inexistentes.
- Persistir los datos en SQLite.

## Estructura CQRS básica

```text
src/Commands   Operaciones que modifican datos
src/Queries    Operaciones que solamente consultan datos
```

La práctica no implementa una arquitectura CQRS distribuida. Se utiliza una sola base de datos y se separan responsabilidades para reconocer comandos y consultas.

## Prueba automática

Ejecute:

```bash
herd php tests/smoke.php
```

La prueba crea una base temporal, ejecuta el CRUD y la elimina al finalizar.

## Flujo Git recomendado

Cada equipo debe crear su propio repositorio a partir de esta plantilla.

```bash
git checkout -b feature/filtro-prioridad
git add .
git commit -m "Agrega filtro por prioridad"
git push -u origin feature/filtro-prioridad
```

Después debe abrir un pull request hacia `main`. No se recomienda utilizar una sola rama compartida por todos los grupos.

## Desafíos por equipo

Cada equipo debe elegir una ampliación:

1. Fecha límite.
2. Categorías.
3. Búsqueda por título.
4. Eliminación lógica.
5. Resumen de tareas por estado.

## Preparación para CI/CD

El archivo `.github/workflows/php-ci.yml` ejecuta validación de sintaxis y la prueba automática en cada `push` o pull request. Más adelante puede añadirse una etapa de despliegue sin cambiar el flujo de ramas.

