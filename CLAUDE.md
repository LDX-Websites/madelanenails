# Madelane Nails (madelanenails.com) — Estado del proyecto
_Última actualización: 20/11/2026_

## Dónde está
- Repo GitHub `LDX-Websites/madelanenails` (organización LDX, rama `main`; antes estaba en `shucleleon-spec`). Se publica solo con cada push (worker `madelanenails`: la web en `public/` y el servidor en `src/index.js`, todo junto).
- No hay copia en la PC: GitHub es la única versión (web y servidor) y Cloudflare publica desde ahí.
- Base de datos D1 + Resend para correos + Turnstile. Recordatorios y resumen diario por cron (7 p. m. hora de Caracas).

## Lo que hay hoy
- **Portada: diseño 1 "Tu tono"** (lila claro, letra Epilogue): tocas un color de esmalte y lo ves en manos reales. Con preguntas frecuentes (8) y datos para Google (NailSalon). Fotos en `public/imagenes/trabajos/`.
- `/disenos` (propuestas) redirige y no se indexa.
- **Panel** (`/admin`) y **Reservar** con el mismo estilo. El panel entra **solo con contraseña** + Turnstile (20/11/2026); sesión de 12 h; bloqueo a los 8 fallos en 15 min.
- La web es solo en español (no tiene versión en inglés).
- **Seguridad revisada (20/11/2026):** trampas anti-bots (campo oculto, tiempo mínimo), límites por IP y por persona, todo se escapa en panel y correos.

## Secrets (los pone el dueño, nunca en código)
`ADMIN_USER` (ya no se pide al entrar, pero se usa para firmar la sesión), `ADMIN_PASS`, `SESSION_SECRET`, `RESEND_API_KEY`, `TURNSTILE_SECRET`.

## Ojo
- En LDX no se muestra la ubicación de Madelane (Pampatar/Margarita) porque revela de dónde es el dueño.

## Reglas del dueño (aplican a todas las webs de LDX)
- Hablarle en español sencillo. Siempre "sin romper nada": probar en local y revisar en vivo antes y después de publicar.
- Las claves (secrets) las pone el dueño con `npx wrangler secret put …` en su CMD. Nunca pedirlas ni escribirlas en el chat o en archivos.
- Cuentas de negocio: leondigitalexperience@gmail.com. Pagos: solo Stripe.
- No pulsar "Comenzar gratis" (Google Cloud) ni "Upgrade" (Workers). Todo debe quedar dentro del plan gratis.
- Firma "Diseñado por LDX" solo con permiso del dueño del negocio, y con el logo de LDX.
- GitHub (rama `main`) es la única versión de cada web, también de su servidor si tiene uno, y se publica desde ahí. No hay copias en la PC.
- Nada de bloquear clic derecho, F12 o arrastrar imágenes: no protege nada y molesta (se quitó de todas el 20/11/2026).

## Seguridad común (revisada el 20/11/2026 con una prueba de ataque)
- Dominio en Cloudflare: HTTPS siempre, TLS mínimo 1.2, HSTS, bloqueo de bots (Bot Fight Mode), DMARC.
- Paneles: solo contraseña (sin usuario), verificación anti-robots Turnstile, sesión firmada que vence sola, bloqueo por intentos fallidos.
- Las direcciones técnicas `*.workers.dev` de las webs están apagadas (solo responden en su dominio).
- Resultado del ataque: no se pudo entrar a paneles, ver datos, falsificar pagos ni inyectar código. Riesgo aceptado: alguien muy insistente que resuelva Turnstile a mano podría ocupar horarios con citas falsas (hay límites por IP y por persona).
