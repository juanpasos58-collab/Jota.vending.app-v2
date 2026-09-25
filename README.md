# Jota Family · Vending — Sistema de reservas

App real (no prototipo) con base de datos compartida: todos los que entren ven el mismo estado de los números, y tú administras desde un solo panel.

WhatsApp configurado por defecto: **3043750139** (573043750139). Puedes cambiarlo después desde el panel admin → Configuración.

## 1. Crear el proyecto en Supabase (base de datos)

1. Ve a https://supabase.com → crea una cuenta gratuita → "New project".
2. Cuando esté listo, ve a **SQL Editor** → "New query".
3. Abre el archivo `supabase/schema.sql` de esta carpeta, copia todo su contenido, pégalo ahí y dale **Run**. Esto crea las tablas, la configuración inicial y la función de reserva.
4. Ve a **Authentication → Users → Add user** y crea tu usuario administrador (correo + clave). Esta app no tiene página de registro público — solo tú puedes crear usuarios, desde aquí.
5. Ve a **Settings → API** y copia:
   - **Project URL**
   - **anon public key**

## 2. Configurar el proyecto localmente

1. Instala [Node.js](https://nodejs.org) si no lo tienes (versión 18 o superior).
2. Descomprime esta carpeta y abre una terminal dentro de ella.
3. Copia `.env.local.example` a `.env.local` y pega ahí tu Project URL y anon key:
   ```
   NEXT_PUBLIC_SUPABASE_URL=https://tu-proyecto.supabase.co
   NEXT_PUBLIC_SUPABASE_ANON_KEY=tu-anon-key
   ```
4. Instala las dependencias:
   ```
   npm install
   ```
5. Pruébalo en tu computador:
   ```
   npm run dev
   ```
   Abre http://localhost:3000 — ese ya es el flujo real conectado a tu base de datos. Para el panel admin ve a http://localhost:3000/admin.

## 3. Publicarlo en internet (Vercel, gratis)

1. Sube esta carpeta a un repositorio de GitHub (puedes hacerlo desde GitHub Desktop si no usas la terminal para git).
2. Ve a https://vercel.com → inicia sesión con GitHub → "Add New Project" → elige el repositorio.
3. En "Environment Variables" agrega las mismas dos variables del paso 2.3 (`NEXT_PUBLIC_SUPABASE_URL` y `NEXT_PUBLIC_SUPABASE_ANON_KEY`).
4. Dale **Deploy**. En un par de minutos te da un enlace público (algo como `tu-proyecto.vercel.app`) — ese es el que compartes con la gente real.

## 4. Antes de enviarlo a la gente

- Revisa en `/admin` → Configuración que el rango de números, el premio y el WhatsApp sean los correctos, y usa "Regenerar números" una sola vez antes de lanzar.
- Recuerda: si esta dinámica termina teniendo cobro y sorteo de un ganador, revisa primero los requisitos de Coljuegos (Ley 643 de 2001) antes de operarla como algo más que una reserva/preinscripción.

## Estructura del proyecto

- `app/page.js` — página pública (selector, formulario, confirmación).
- `app/admin/page.js` — login del administrador.
- `app/admin/dashboard/page.js` — panel: resumen, números, participantes, configuración.
- `supabase/schema.sql` — todo lo que se ejecuta en Supabase.
- `lib/supabaseClient.js` — conexión a Supabase.
