# 📦 Automatiza Platform - Plataforma SaaS de Gestión Modular

Automatiza Platform es una plataforma **autoalojada**, **modular** y **escalable**, diseñada para empresas que requieren gestionar personas, procesos de RRHH, auditoría, carga de documentos, automatizaciones e integraciones inteligentes con N8N y servicios externos.

---

## 🚀 Características principales

- ✅ Autenticación robusta con **Keycloak** (JWT, OAuth, roles)
- ✅ Multiempresa con gestión de usuarios, roles y privilegios
- ✅ Módulos de:
  - Carga de CV y análisis IA (`/api/cargar_cv`)
  - Bot asistente para automatizaciones (`/api/bot`)
  - Liquidaciones de sueldo (`/api/liquidacion`)
  - Rendiciones de gastos con historial (`/api/rendiciones`)
  - Auditoría automática de eventos (`/api/auditoria`)
- ✅ Gestión desde el frontend:
  - `/admin/usuarios` (roles, empresas)
  - `/admin/auditoria` (logs)
  - `/perfil`, `/dashboard`, etc.
- ✅ Infraestructura desplegable en **Docker Compose** ARM64
- ✅ Monitoreo con **Prometheus + Alertmanager**
- ✅ Alertas por **correo electrónico** (Telegram opcional)

---

## 🧱 Estructura de carpetas

```
automatiza-platform/
│
├── backend/                 # Backend FastAPI
│   ├── main.py              # Entrypoint con middleware
│   ├── routes/              # Rutas/módulos desacoplados
│   ├── middleware/          # Auditoría
│   ├── utils/               # Auth y utilitarios
│   └── scripts/             # Init roles Keycloak
│
├── frontend/                # Frontend Next.js
│   ├── pages/               # Páginas de navegación (login, dashboard, admin/...)
│   ├── components/          # Layout, selector empresa, etc.
│
├── db/
│   └── init.sql             # Script de creación de tablas
│
├── infra/                   # Infraestructura Docker + monitoreo
│   ├── docker-compose.yml
│   ├── docker-compose.override.yml
│   ├── prometheus/
│   │   ├── prometheus.yml
│   │   ├── alertmanager.yml
│   │   └── alerts.yml
│
└── README.md
```

---

## ⚙️ Instalación rápida en VPS ARM64

```bash
git clone https://github.com/lbadilla1970/automatiza-platform.git
cd automatiza-platform
cp .env.example .env
nano .env     # Configura claves y dominio

# Construye todo
cd infra
docker-compose up -d --build
```

Accede a:
- Frontend: `https://app.automatizaml.cl`
- Keycloak Admin: `https://auth.automatizaml.cl`
- N8N: `https://n8n.automatizaml.cl`
- Prometheus: `http://<IP>:9090`
- Alertmanager: `http://<IP>:9093`

---

## 🛡️ Seguridad

- Acceso por token JWT
- Validación por rol por cada endpoint
- Auditoría de IP, timestamp, usuario y método
- CORS habilitado con `*` (restringir en prod)
- Contraseñas y claves fuera del repositorio en `.env`

---

## 📬 Alertas (ejemplo)

- Si backend cae → correo `luciano.badilla@outlook.com`
- Si errores 500 aumentan → alerta `warning`

---

## 🔧 Mantenimiento y expansión

Para crear un nuevo proceso:
1. Crear archivo en `backend/routes/mi_modulo.py`
2. Crear página en `frontend/pages/mi_modulo.tsx`
3. Agregar endpoint y fetch
4. Validar rol con `Depends(get_current_user)`

---

## 📌 Roles predefinidos
- `admin`: acceso completo y configuración
- `empresa`: gestiona sus trabajadores y procesos
- `trabajador`: acceso limitado a sus datos y acciones

---

## ✉️ Contacto
Creado por Luciano Badilla - [automatiza.cl](https://automatiza.cl)  
Correo: luciano.badilla@outlook.com  
GitHub: [lbadilla1970](https://github.com/lbadilla1970)

---

**Licencia:** MIT.  
**Instalación local 100% libre y privada.**
