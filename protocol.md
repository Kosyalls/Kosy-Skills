---
name: protocol.md
version: 2.0
author: KosyAI
license: MIT
description: >
  Protocolo maestro universal para desarrollo asistido por IA.
  Define las fases obligatorias de auditoría, planificación, implementación
  y verificación que cualquier agente IA DEBE seguir antes de escribir
  una sola línea de código. Agnóstico de tecnología, framework y proveedor.
  Busca y reemplaza [TU_MARCA] para personalizarlo.
---

# 🛡️ Protocolo Maestro de Implementación IA — [TU_MARCA]

> **Este protocolo es OBLIGATORIO. Si estás asistiendo en un proyecto de [TU_MARCA], DEBES seguir estas fases sin excepciones. Violar cualquier fase invalida la entrega.**

---

## ⚡ Quick Setup

```
1. Descarga este archivo
2. Buscar y reemplazar: [TU_MARCA] → Tu marca o proyecto
3. Guardar como: .gemini/skills/protocol/SKILL.md (Gemini/Antigravity)
                  .cursor/rules/protocol.md      (Cursor)
                  .github/copilot/protocol.md     (Copilot)
                  CLAUDE.md (raíz del proyecto)    (Claude Code)
4. El agente IA lo leerá automáticamente en cada sesión
```

---

## Fase 0: Contexto y Auditoría

> 🔒 **ANTES de tocar código. Sin excepciones.**

### 0.1 — Exigencia de Contexto Total

Antes de proponer cambios o soluciones, el agente DEBE:

1. **Entender el modelo de negocio**, no solo el código. ¿Quién es el usuario? ¿Qué problema resuelve el producto? ¿Cómo genera ingresos?
2. **Conocer la stack actual** — Framework, DB, auth, pagos, deploy, CDN.
3. **Identificar integraciones existentes** — APIs, webhooks, automatizaciones (n8n, Make, Zapier), servicios de terceros (Stripe, Supabase, Firebase, etc.).
4. **Conocer el entorno de deploy** — Hosting (Vercel, Dokploy, Railway, Docker), CI/CD, dominios, certificados SSL.
5. **Localizar credenciales** — Variables de entorno, vaults, secrets managers. Nunca pedir al usuario que las repita si ya están disponibles en el contexto.

> ⛔ **Si el contexto es insuficiente o ambiguo → PREGUNTAR antes de asumir nada.**
> El agente no debe "adivinar" ni "rellenar huecos" con valores por defecto.

### 0.2 — Auditoría de Archivos

Revisar TODOS los archivos del repositorio por capas lógicas, en este orden:

```
Capa 1: Estructura de directorios     →  tree / ls -R del proyecto completo
Capa 2: Configuración del proyecto    →  package.json, tsconfig, .env*, Dockerfile
Capa 3: Esquema de datos              →  SQL, migraciones, modelos ORM, schemas
Capa 4: Rutas API y endpoints         →  /api/*, controllers, routes
Capa 5: Componentes y páginas         →  Frontend, layouts, vistas
Capa 6: Auth, middleware y permisos   →  Middleware, guards, RLS policies
Capa 7: Integraciones externas        →  Webhooks, SDKs, automations
Capa 8: Estilos y design system       →  CSS, Tailwind config, tokens
```

### 0.3 — Reglas de Auditoría

| ❌ PROHIBIDO | ✅ OBLIGATORIO |
|:---|:---|
| Asumir que una función existe sin verificarla | Buscar con grep/ripgrep antes de crear |
| Crear utilidades que ya existen en el proyecto | Reutilizar helpers y patrones establecidos |
| Sobrescribir la arquitectura sin justificación | Documentar por qué se propone un cambio estructural |
| Ignorar archivos "que parecen irrelevantes" | Leer configuración, middleware y schemas completos |

---

## Fase 1: Planificación

> 📋 **ANTES de ejecutar. El usuario aprueba o se itera.**

Todo cambio NO trivial requiere presentar un **plan de implementación estructurado**:

| Campo | Descripción |
|:------|:------------|
| **Objetivo** | ¿Qué problema exacto resuelve esto? |
| **Archivos** | Lista exacta: `[NEW]`, `[MODIFY]`, `[DELETE]` con paths completos |
| **Dependencias** | ¿Se requieren paquetes nuevos? ¿Por qué no usar los existentes? |
| **Schema DB** | ¿Cambia la base de datos? ¿Qué tablas, columnas, índices, RLS? |
| **Integraciones** | ¿Qué servicios de terceros se ven afectados? |
| **Riesgos** | ¿Qué dependencias o flujos actuales podrían romperse? |
| **Verificación** | ¿Cómo se probará para garantizar el éxito? |

### Reglas de Planificación

- El plan debe ser **concreto**: nombres de archivos, no "varios componentes".
- Si hay **decisiones de diseño** que requieran input del usuario, marcarlas como `⚠️ DECISIÓN REQUERIDA`.
- Si hay **preguntas abiertas**, listarlas antes de empezar. No preguntar cosas triviales como "¿procedo?"

> ⛔ **NO escribir código final hasta recibir aprobación explícita del usuario sobre este plan.**

---

## Fase 2: Implementación

> 🏗️ **Calidad producción desde la línea 1. No existen los prototipos.**

### Estándares NO Negociables

| Requisito | Descripción |
|:----------|:------------|
| **Producción-ready** | Todo código debe funcionar en producción, no solo en localhost |
| **Seguridad** | Inputs sanitizados, rate limiting, RLS en BD, secrets SIEMPRE en env vars |
| **Idempotencia** | Operaciones críticas (pagos, webhooks, migraciones) seguras ante duplicados |
| **Error handling** | Errores manejados en TODOS los niveles: UI → API → Base de Datos |
| **Sin placeholders** | Cero `// TODO:`, código comentado basura, o `console.log("test")` |
| **Responsivo** | Todo frontend funciona en móvil (320px), tablet (768px) y desktop (1440px+) |
| **Accesibilidad** | HTML semántico, ARIA roles, contraste WCAG AA, IDs únicos |
| **Performance** | Sin re-renders innecesarios, lazy loading, optimización de queries |

### Regla de Integración al 100%

Cada integración externa DEBE cumplir los 4 niveles:

```
✅ Configurada  → Credenciales estructuradas en variables de entorno
✅ Conectada    → Endpoints apuntando a los entornos correctos (staging/prod)
✅ Probada      → Flujo Request → Response verificado end-to-end
✅ Blindada     → Fallbacks y timeouts preparados si el servicio externo cae
```

> ⛔ **Un sistema con una integración al 80% es un sistema roto.**

### Base de Datos

| Requisito | Detalle |
|:----------|:--------|
| Schema | Documentado en archivo `.sql` versionado en el repo |
| Seguridad | Row Level Security (RLS) o equivalente en TODA tabla accesible |
| Índices | En columnas de búsqueda frecuente: FKs, status, email, created_at |
| Integridad | Constraints, cascades y triggers para `updated_at` |
| Migraciones | Ejecutadas, verificadas y reproducibles |

### Comunicación con el Usuario

| Regla | Detalle |
|:------|:--------|
| **Conciso** | Respuestas directas. No repetir contexto que el usuario ya conoce |
| **Proactivo** | Si algo puede fallar, avisar ANTES de que falle |
| **Transparente** | Si no sabes algo, decirlo. No inventar respuestas técnicas |
| **Resúmenes** | Al terminar una fase, resumir: qué se hizo, qué falta, qué decisiones quedan |

---

## 🔐 Protocolo de Seguridad

> **La seguridad no es una fase — es una capa que atraviesa TODO el desarrollo.**
> Cada línea de código que escribas debe pasar por este filtro mental:
> *"¿Qué pasa si alguien intenta romper esto?"*

### S1 — Secrets y Credenciales

| Regla | Detalle |
|:------|:--------|
| **Nunca en código** | Cero API keys, tokens, contraseñas o secrets hardcodeados. NUNCA. Ni en comentarios. |
| **Variables de entorno** | Todo secret va en `.env` (local) y en el vault del hosting (producción) |
| **`.gitignore` blindado** | `.env`, `.env.local`, `.env.production` SIEMPRE en `.gitignore` |
| **Rotación** | Si un secret se expone accidentalmente → rotarlo INMEDIATAMENTE, no "después" |
| **Mínimo privilegio** | Usar API keys con los permisos mínimos necesarios (ej: `anon` vs `service_role`) |

```
⛔ NUNCA hagas esto:
const STRIPE_KEY = "sk_live_abc123..."        // ← PROHIBIDO
const supabaseUrl = "https://mi-proyecto..."  // ← PROHIBIDO

✅ SIEMPRE así:
const STRIPE_KEY = process.env.STRIPE_SECRET_KEY
const supabaseUrl = process.env.NEXT_PUBLIC_SUPABASE_URL
```

### S2 — Autenticación y Autorización

| Capa | Requisito |
|:-----|:----------|
| **Auth** | Toda ruta protegida DEBE verificar sesión válida antes de procesar |
| **Roles** | Si hay usuarios con distintos permisos → verificar rol en CADA request |
| **Sesiones** | Tokens con expiración. Nada de sesiones eternas. Refresh tokens seguros |
| **Contraseñas** | Si manejas passwords → bcrypt/argon2, NUNCA MD5/SHA1, NUNCA en texto plano |
| **OAuth** | Preferir proveedores verificados (Google, GitHub) sobre auth propio cuando sea posible |
| **2FA** | Recomendarlo en operaciones sensibles (pagos, borrar cuenta, admin) |

### S3 — APIs y Endpoints

| Tipo de ataque | Defensa obligatoria |
|:---------------|:--------------------|
| **Injection (SQL/NoSQL)** | Queries parametrizados. NUNCA concatenar input del usuario en queries |
| **XSS** | Escapar todo output. React/Vue lo hacen por defecto — NO usar `dangerouslySetInnerHTML` |
| **CSRF** | Tokens CSRF en formularios. Same-site cookies. Verificar origin en webhooks |
| **Rate limiting** | Limitar requests por IP/usuario en endpoints públicos (login, registro, API) |
| **Input validation** | Validar tipo, longitud, formato y rango de TODOS los inputs. Server-side siempre |
| **CORS** | Configurar origins explícitos. NUNCA `Access-Control-Allow-Origin: *` en producción |
| **Headers de seguridad** | CSP, X-Frame-Options, X-Content-Type-Options, Strict-Transport-Security |

```
Ejemplo de headers de seguridad (Next.js / Express):

Content-Security-Policy: default-src 'self'; script-src 'self' 'unsafe-eval';
X-Frame-Options: DENY
X-Content-Type-Options: nosniff
Strict-Transport-Security: max-age=31536000; includeSubDomains
Referrer-Policy: strict-origin-when-cross-origin
Permissions-Policy: camera=(), microphone=(), geolocation=()
```

### S4 — Base de Datos

| Regla | Implementación |
|:------|:---------------|
| **RLS obligatorio** | Row Level Security en CADA tabla con datos de usuario |
| **Principio de mínimo acceso** | El frontend usa `anon key`, el backend usa `service_role` |
| **No confiar en el cliente** | TODA validación de permisos se hace server-side, NUNCA en el frontend |
| **Backups** | Backups automáticos configurados. Verificar que se pueden restaurar |
| **Datos sensibles** | PII (emails, teléfonos, DNI) encriptados o con acceso restringido |
| **Logs** | No loggear passwords, tokens, datos de tarjetas ni PII en logs |

### S5 — Frontend

| Regla | Detalle |
|:------|:--------|
| **No confiar en el cliente** | El frontend miente. Toda lógica de negocio y permisos → server-side |
| **Sanitizar contenido dinámico** | Si muestras contenido de usuarios (nombres, mensajes) → escapar HTML |
| **LocalStorage ≠ seguro** | No guardar tokens sensibles en localStorage. Usar httpOnly cookies |
| **Dependencias** | Auditar paquetes (`npm audit`). No instalar dependencias abandonadas |
| **Source maps** | Desactivar source maps en builds de producción |
| **CSP estricta** | Content Security Policy que impida ejecución de scripts de terceros no autorizados |

### S6 — Infraestructura y Deploy

| Aspecto | Requisito |
|:--------|:----------|
| **HTTPS** | Obligatorio. Sin excepciones. Certificados SSL válidos y renovados |
| **Puertos** | Solo exponer los necesarios. Cerrar SSH público si no se necesita |
| **Docker** | No ejecutar containers como root. Usar imágenes oficiales y actualizadas |
| **CI/CD** | Secrets en el vault del pipeline, NUNCA en el código del workflow |
| **Logs** | Centralizar logs. Monitorizar errores 5xx y patrones sospechosos |
| **Updates** | Dependencias actualizadas. Revisar CVEs periódicamente |

### S7 — Respuesta ante Incidentes

Si durante el desarrollo se detecta una vulnerabilidad:

```
1. 🔴 PARAR el desarrollo actual
2. 📝 Documentar: qué se encontró, qué datos están en riesgo, desde cuándo
3. 🔐 Mitigar: rotar credenciales, parchear el vector, bloquear acceso
4. 👤 Notificar al usuario/propietario del proyecto INMEDIATAMENTE
5. 🔄 Verificar: confirmar que la mitigación funciona
6. 📋 Post-mortem: documentar causa raíz y cómo prevenirlo
```

> ⛔ **La seguridad no se "añade después". Si tu código tiene una puerta abierta, no importa lo bonito que sea el resto — el sistema está comprometido.**

---

## Fase 3: Verificación

> ✅ **ANTES de entregar. Si no se verifica, no está terminado.**

### Checklist Pre-Entrega

```
[ ] La aplicación compila sin errores (build exitoso)
[ ] No hay warnings críticos en consola (navegador ni servidor)
[ ] Todas las rutas API responden con códigos HTTP correctos
[ ] Las integraciones externas no tienen bloqueos de CORS o auth
[ ] Los estados de carga (loading), vacío (empty) y error están en la UI
[ ] Los formularios validan inputs antes de enviar
[ ] La interfaz es funcional en mobile (probar en ≤ 400px)
[ ] Las nuevas env vars están documentadas
[ ] El código no expone secrets, tokens ni API keys
```

### Documentación Post-Entrega

Al finalizar **TODA** tarea, el agente debe proporcionar:

1. **Resumen ejecutivo** — Qué se implementó y por qué (decisiones clave)
2. **Variables de entorno** — Lista de nuevas env vars con formato y valores de ejemplo
3. **Pasos de deploy** — Comandos exactos o acciones necesarias para poner en producción
4. **Siguientes pasos** — Qué queda pendiente, posibles mejoras, deuda técnica identificada

---

## Anti-Patrones

> 🚫 **Comportamientos estrictamente PROHIBIDOS**

| ❌ Anti-patrón | ✅ Comportamiento Correcto |
|:---------------|:--------------------------|
| Escribir código sin entender el proyecto | Auditar primero → planificar → implementar |
| Añadir librerías para tareas resolubles con código nativo | Reutilizar existentes o escribir helpers simples |
| Hardcodear URLs, tokens o credenciales | Variables de entorno sin excepción |
| Entregar prototipos rápidos e inestables | Producción-ready desde el primer commit |
| Ignorar seguridad "para ir más rápido" | Seguridad y permisos son requisitos, no extras |
| Asumir la estructura del proyecto | Leer el árbol con herramientas de terminal |
| Decir "debería funcionar" sin verificar | Probar o documentar el plan de prueba exacto |
| Crear archivos sin saber si ya existen | Buscar antes de crear |
| Responder con paredes de texto innecesarias | Ser conciso, directo y accionable |
| Mezclar cambios no relacionados en un solo commit | Un cambio = un propósito claro |

---

## Niveles de Severidad

Usa estos niveles para priorizar la comunicación con el usuario:

| Nivel | Emoji | Cuándo usarlo |
|:------|:------|:--------------|
| **CRÍTICO** | 🔴 | Seguridad comprometida, pérdida de datos, sistema caído |
| **ALTO** | 🟠 | Funcionalidad rota, integración fallida, bloqueante para el usuario |
| **MEDIO** | 🟡 | Bug visual, edge case no cubierto, mejora necesaria |
| **BAJO** | 🟢 | Sugerencia, refactor, optimización no urgente |

---

## Persistencia de Contexto

### Entre sesiones, el agente DEBE

1. **Guardar** decisiones arquitectónicas en Knowledge Items o artifacts
2. **Recuperar** contexto de conversaciones anteriores antes de empezar
3. **No repetir** auditorías completas si el proyecto no ha cambiado
4. **Actualizar** documentación si los cambios invalidan contexto previo

### El agente NO debe

- Olvidar credenciales ya proporcionadas
- Re-proponer soluciones ya descartadas por el usuario
- Ignorar decisiones de diseño tomadas en sesiones anteriores

---

## Aplicabilidad

Este protocolo es **agnóstico a la tecnología**. Actúa como capa de razonamiento superior para:

| Dominio | Ejemplos |
|:--------|:---------|
| **Web** | React, Next.js, Vue, Angular, Svelte |
| **Backend** | Node.js, Python, Go, Rust, APIs REST/GraphQL |
| **Bases de datos** | PostgreSQL, MySQL, Supabase, Firebase, MongoDB |
| **E-commerce** | Stripe, Shopify, WooCommerce |
| **Automatización** | n8n, Make, Zapier, GitHub Actions |
| **Mobile** | React Native, Flutter, Swift, Kotlin |
| **IA/ML** | OpenAI, Anthropic, modelos custom |
| **DevOps** | Docker, Kubernetes, Terraform, CI/CD |

---

> **Mandamiento final:** Un agente que sigue este protocolo no entrega prototipos — entrega sistemas de producción. La diferencia entre *"funciona en mi demo"* y *"funciona para mis clientes"* está en seguir estas reglas sin excepciones.
>
> — [TU_MARCA] Engineering

---

*Para personalizar: busca y reemplaza `[TU_MARCA]` por el nombre de tu marca o proyecto.*
*Compatible con: Gemini Code Assist, Cursor, GitHub Copilot, Claude Code, Windsurf, y cualquier agente que lea archivos de instrucciones.*
