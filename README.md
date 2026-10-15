# Arcea Estudio — Tienda de ropa online

> E-commerce full-stack para **Arcea Estudio**, una marca argentina de ropa de invierno (sweaters y casualwear en tejidos naturales). Catálogo, carrito, checkout con pagos, cuentas de usuario y panel de administración — todo en un solo proyecto Next.js.

![Next.js](https://img.shields.io/badge/Next.js_16-000000?logo=nextdotjs&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?logo=typescript&logoColor=white)
![Supabase](https://img.shields.io/badge/Supabase-3FCF8E?logo=supabase&logoColor=white)
![Tailwind](https://img.shields.io/badge/Tailwind_v4-06B6D4?logo=tailwindcss&logoColor=white)
![Mercado Pago](https://img.shields.io/badge/Mercado_Pago-00B1EA?logo=mercadopago&logoColor=white)

<!-- 📸 CAPTURAS: arrastrá imágenes del catálogo / detalle de producto / carrito acá en el editor web de GitHub, o guardá en docs/screenshots/ y descomentá: -->
<!-- ![Catálogo](docs/screenshots/catalogo.png) -->

> 💡 **Corre sin backend:** cloná, `npm install && npm run dev` y la tienda levanta con datos de ejemplo (seed), sin configurar nada. Al conectar Supabase, pasa a datos reales.

## Qué incluye

- **Catálogo** con detalle de producto y selección de variantes (talle / color).
- **Carrito** client-side persistente.
- **Checkout** con Mercado Pago (Checkout Pro); el estado del pedido lo decide el **webhook**, no las `back_urls`.
- **Cuentas de usuario**: registro, login, reset de contraseña y perfil editable.
- **Panel de administración** con route groups por área (storefront / auth / account / admin).
- **SEO**: sitemap, `robots` y Open Graph dinámica.

## Seguridad

- **Row Level Security** en Supabase y **anti-escalada de rol** por trigger (`prevent_role_change`).
- `admin.ts` marcado `import "server-only"` (nunca llega al cliente).
- El reset de contraseña **no revela** si el email existe.
- Precios en **enteros (centavos)**, nunca floats; se formatean en la UI.

## Stack

Next.js 16 (App Router) · React 19 · TypeScript strict · Tailwind CSS v4 · shadcn/ui (sobre Base UI) · Supabase (PostgreSQL + Auth + RLS + Storage) · Mercado Pago · `react-hook-form` + `zod` · `sonner` · `date-fns`.

## Correr en local

```bash
npm install
npm run dev     # http://localhost:3000  (arranca con datos seed, sin backend)
```

### Con backend real (Supabase)

1. Creá un proyecto en [supabase.com](https://supabase.com).
2. Ejecutá las migraciones de `supabase/migrations/` en orden (SQL Editor o Supabase CLI).
3. Copiá `.env.example` → `.env.local` y completá las credenciales de Supabase (y de Mercado Pago para pagos).
4. `npm run dev` — ahora persiste contra Postgres.

## Estructura

```
src/
  app/            # route groups: (storefront) (auth) (account) (admin)
    api/webhooks/mercadopago/route.ts   # webhook de pagos (público)
  actions/        # Server Actions ("use server")
  lib/            # supabase/ · mercadopago/ · auth/ · validations/ · db/
  components/     # ui · storefront · account · admin · layout
supabase/migrations/   # SQL versionado
mockup/index.html      # mockup de diseño de referencia (aprobado por el cliente)
```

## Estado

Catálogo, carrito, auth y panel están implementados y corren con datos seed. La conexión a Supabase / Mercado Pago en producción y el despliegue quedan como próximos pasos (ver [`ROADMAP.md`](./ROADMAP.md)).

---

**Convenciones:** UI y textos en español; identificadores, archivos y tablas/columnas en inglés. Mobile-first (buena parte del tráfico llega desde Instagram).
