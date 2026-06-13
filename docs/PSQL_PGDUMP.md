# Backups con pg_dump desde la terminal

`pg_dump` viene incluido con el paquete `postgresql-client` ya instalado en el devcontainer. No requiere ninguna configuración adicional.

## Hacer un backup

```bash
pg_dump vete5 > data/vete5.sql
```

El archivo queda en `data/` junto a los backups generados desde pgAdmin. No hace falta montar nada — `data/` es una carpeta normal del workspace accesible directamente.

Para hacer el backup de otra base de datos, cambia el nombre:

```bash
pg_dump veterinariadb > data/veterinariadb.sql
```

## Restaurar un backup

```bash
psql veterinariadb < data/veterinariadb.sql
```

Si la base de datos aún no existe, créala primero:

```bash
psql -c "CREATE DATABASE veterinariadb;"
psql veterinariadb < data/veterinariadb.sql
```

## Diferencia con los backups de pgAdmin

| | pgAdmin | pg_dump (terminal) |
|---|---|---|
| Formato | `.db` (binario) | `.sql` (texto plano legible) |
| Dónde queda | `data/` via mount del contenedor pgadmin | `data/` directamente en el workspace |
| Cómo restaurar | Desde pgAdmin (Restore) | `psql nombre_db < archivo.sql` |

Ambos métodos guardan en `data/` y son válidos. El `.sql` tiene la ventaja de que puedes abrirlo con cualquier editor y leer exactamente qué contiene.
