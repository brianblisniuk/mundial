# Mundial 2026 · Argentina al Mundial · Trip Operations

App colaborativa de operaciones para el viaje Miami → Kansas City siguiendo a Argentina en el Mundial 2026. Sync real-time vía Supabase, sin build step.

**Stack**: HTML + Alpine.js 3.13.5 + Supabase JS 2.x + Leaflet 1.9.4 (todo via CDN)

## Setup inicial

1. **Crear tablas en Supabase** — abrir el SQL Editor del proyecto y correr `setup_supabase.sql`:

   https://supabase.com/dashboard/project/wtjggtmajmuahgtygjps/sql

2. **Deploy en Netlify** — dos opciones:

   - **Drag-and-drop**: arrastrar `index.html` a https://app.netlify.com/drop
   - **Git push**: con el repo conectado a Netlify, hacer `git push` y deploya automáticamente.

## Credenciales

- **Supabase Project**: `wtjggtmajmuahgtygjps`
- **Supabase URL**: `https://wtjggtmajmuahgtygjps.supabase.co`
- **Publishable Key**: `sb_publishable_PolwidwGLewBGR0czh_ZUA_0b5Wm3XT`

## Estructura

```
index.html              · app completa (single file, ~300KB)
setup_supabase.sql      · schema + RLS + realtime publication
netlify.toml            · headers de seguridad
README.md               · este archivo
```

## Datos del viaje

- **Cliente**: 4 pax · 1 driver autorizado
- **Período**: 10 jun → 2 jul 2026 · 22 noches
- **Vehículo**: El Monte RV Class C Medium (D) 24-26ft · Booking KFN852863-8
- **Pickup**: Mié 10 jun 13:00 · Princeton, FL
- **Devolución**: Jue 2 jul 11:00 · Princeton, FL
- **Match**: Argentina vs Argelia · 16 jun 20:00 CT · Arrowhead Stadium, KC

## Tablas en Supabase

| Tabla       | Propósito                                                        |
|-------------|------------------------------------------------------------------|
| `trips`     | JSON principal del trip (itinerario, presupuesto, providers...)  |
| `comments`  | Comentarios sobre slots, providers o acciones                    |
| `snapshots` | Backups manuales del estado del trip                             |
| `changes`   | Log de cambios (historial real-time)                             |

RLS habilitada con policies abiertas (la app usa publishable key sin auth). Para producción multi-cliente: agregar auth + restringir por `trip_id`.

## Identidades

App diseñada para colaboración entre 2 personas: `Brian` y `Federico`. Cambiar editando las opciones en el menú de identidad (líneas con `setIdentity('Brian')` y `setIdentity('Federico')` en el HTML).

## Build / Run local

No hay build step. Servir el `index.html` con cualquier static server:

```bash
python3 -m http.server 8080
# o
npx serve .
```
