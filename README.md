# Rebold — Client Delivery Platform

Plataforma interna para gestión del flujo de entrega y activación de clientes: revisión financiera, activación operativa, integración con Slack y Google Drive.

---

## 🚀 Deploy en 15 minutos

### Requisitos previos
- Cuenta en [GitHub](https://github.com)
- Cuenta en [Vercel](https://vercel.com) (gratis)
- API Key de Anthropic → [console.anthropic.com](https://console.anthropic.com)

---

### Paso 1 — Subir a GitHub

1. Crea un repositorio nuevo en GitHub (puede ser privado)
2. Sube todos los archivos de esta carpeta:

```bash
git init
git add .
git commit -m "Initial deploy — Rebold Client Delivery"
git remote add origin https://github.com/TU_USUARIO/TU_REPO.git
git push -u origin main
```

---

### Paso 2 — Conectar con Vercel

1. Ve a [vercel.com](https://vercel.com) → **Add New Project**
2. Importa el repositorio de GitHub que creaste
3. Vercel detectará automáticamente la configuración (`vercel.json`)
4. Haz clic en **Deploy** (sin configurar nada más aún)

---

### Paso 3 — Configurar la API Key (variables de entorno)

En Vercel, ve a tu proyecto → **Settings → Environment Variables** y agrega:

| Variable | Valor |
|---|---|
| `ANTHROPIC_API_KEY` | `sk-ant-...` (tu key de Anthropic) |
| `ALLOWED_ORIGIN` | `https://TU-PROYECTO.vercel.app` (la URL que te dio Vercel) |

Luego ve a **Deployments → Redeploy** para que tome las variables.

---

### Paso 4 — Conectar Slack y Google Drive en Claude.ai

Las integraciones MCP usan las credenciales de tu cuenta de Claude.ai.

Para que funcionen en producción, el servidor llama a Anthropic con tu API key. Las conexiones a Slack y Drive se autentican con los tokens MCP que Claude.ai gestiona internamente — **no necesitas configurar OAuth adicional**.

> ⚠️ Asegúrate de que en tu cuenta de Claude.ai (claude.ai/settings/integrations) estés conectado a:
> - **Slack** — workspace de Rebold
> - **Google Drive** — cuenta de Google donde quieres las carpetas

---

### Paso 5 — Verificar

1. Abre tu URL de Vercel: `https://TU-PROYECTO.vercel.app`
2. Crea un cliente de prueba y actívalo
3. Verifica en Slack que se creó el canal
4. Verifica en tu Google Drive que aparece la carpeta con el nombre del cliente

---

## 📁 Estructura del proyecto

```
rebold-client-delivery/
├── public/
│   └── index.html          # Frontend completo (SPA)
├── api/
│   └── activate.js         # Serverless function (Vercel)
├── vercel.json             # Configuración de rutas Vercel
├── package.json
├── .gitignore
└── README.md
```

---

## 🔑 Variables de entorno requeridas

| Variable | Descripción | Obligatoria |
|---|---|---|
| `ANTHROPIC_API_KEY` | API key de Anthropic (`sk-ant-...`) | ✅ Sí |
| `ALLOWED_ORIGIN` | URL de producción para CORS | Recomendada |

---

## 🛠 Desarrollo local

```bash
npm install -g vercel
vercel dev
```

Crea un archivo `.env` local (no se sube a Git):
```
ANTHROPIC_API_KEY=sk-ant-tu-key-aqui
ALLOWED_ORIGIN=http://localhost:3000
```

---

## 🔄 Flujo de trabajo

```
Comercial → Nuevo Cliente (docs) → Revisión Financiera → Aprobado
                                                             ↓
                                              Activación Operativa
                                           (Slack + Drive automático)
                                                             ↓
                                                     Cliente Activo
```

---

## 📞 Soporte

Plataforma desarrollada para uso interno de Rebold.
