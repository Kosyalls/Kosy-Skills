# 🛡️ Kosy-Skills — protocol.md

### El archivo que tu IA necesita para dejar de darte prototipos y empezar a darte código de producción.

---

## ¿Qué es `protocol.md`?

Es un archivo de instrucciones que le das a tu agente IA (Cursor, Gemini, Copilot, Claude, etc.) para que **trabaje como un senior engineer** en vez de como un becario con prisa.

Sin `protocol.md`:
- ❌ Tu IA asume cosas que no existen en tu proyecto
- ❌ Te da código que "funciona en mi demo" pero rompe en producción
- ❌ Ignora seguridad, accesibilidad y rendimiento
- ❌ Te entrega prototipos que "luego arreglamos"

Con `protocol.md`:
- ✅ Audita tu proyecto ANTES de tocar una línea
- ✅ Te presenta un plan y espera tu aprobación
- ✅ Escribe código producción-ready desde el primer commit
- ✅ Maneja seguridad, errores y responsive sin que se lo pidas

---

## ⚡ Instalación (30 segundos)

1. **Descarga** [`protocol.md`](./protocol.md)
2. **Busca y reemplaza** `[TU_MARCA]` por el nombre de tu proyecto
3. **Colócalo** en la ubicación de tu agente:

| Agente IA | Dónde guardar el archivo |
|:----------|:-------------------------|
| **Cursor** | `.cursor/rules/protocol.md` |
| **Gemini / Antigravity** | `.gemini/skills/protocol/SKILL.md` |
| **Claude Code** | `CLAUDE.md` (raíz del proyecto) |
| **GitHub Copilot** | `.github/copilot/protocol.md` |
| **Windsurf** | `.windsurfrules` |
| **Cualquier otro** | Pégalo como System Prompt |

4. **Listo.** Tu agente IA lo leerá en cada sesión automáticamente.

---

## 📋 ¿Qué incluye?

| Fase | Qué hace |
|:-----|:---------|
| **Fase 0: Descubrimiento** | La IA escanea tu proyecto (o te pregunta si empiezas de cero) |
| **Fase 1: Planificación** | Presenta un plan estructurado y espera tu OK |
| **Fase 2: Implementación** | Código producción-ready con estándares no negociables |
| **🔐 Protocolo de Seguridad** | 7 dominios: secrets, auth, APIs, DB, frontend, infra, incidentes |
| **Fase 3: Verificación** | Checklist pre-entrega + documentación obligatoria |

---

## 🔐 Protocolo de Seguridad incluido

No es genérico. Es accionable:

- **S1** — Secrets y credenciales (env vars, .gitignore, rotación)
- **S2** — Autenticación (sesiones, bcrypt, OAuth, 2FA)
- **S3** — APIs (SQL injection, XSS, CSRF, rate limiting, CORS, CSP)
- **S4** — Base de datos (RLS, mínimo acceso, backups, PII)
- **S5** — Frontend ("el frontend miente", localStorage, source maps)
- **S6** — Infraestructura (HTTPS, Docker, CI/CD vaults)
- **S7** — Respuesta ante incidentes (protocolo de 6 pasos)

---

## 🌐 Compatible con cualquier stack

React · Next.js · Vue · Angular · Node.js · Python · Go · PostgreSQL · Supabase · Firebase · Stripe · n8n · Docker · y más.

---

## 📲 Créditos

Creado por **[KosyAI](https://github.com/Kosyalls)** · MIT License

Síguenos para más herramientas de productividad con IA:
- 📸 [Instagram](https://instagram.com/kosyai)
- 💼 [LinkedIn](https://linkedin.com/company/kosyai)
- 🎵 [TikTok](https://tiktok.com/@kosyai)

---

> ⭐ **Si te ha sido útil, deja una estrella en el repo. Ayuda a que más developers lo encuentren.**
