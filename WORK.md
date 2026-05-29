# GestorPinto App - Guía de Trabajo en Equipo

## Integrantes
- johan
- miguel
- andres
- justin
- juan

## Objetivo
Desarrollar una app móvil con React Native (Expo) que autentique usuarios vía Notion API y muestre recursos académicos.

---

## Configuración Inicial (Todos los integrantes)

### 1. Clonar el repositorio
```bash
git clone https://github.com/igrisdev/gestor-pinto-app.git
cd gestor-pinto-app
```

### 2. Crear tu rama de trabajo
```bash
git checkout -b dev_[tu_nombre]
```
Ejemplo: `git checkout -b dev_johan`

### 3. Crear tus archivos y hacer commit
**No es necesario correr la app.** Solo crea los archivos que te corresponden, haz commit y push a tu rama.

---

## Distribución de Archivos por Integrante

### johan — Configuración del Proyecto
**Rama:** `dev_johan`
**Archivos a crear:**
- `package.json`
- `tsconfig.json`
- `app.json`
- `babel.config.js`
- `.gitignore`
- `.env.example`
- `assets/icon.png`
- `assets/adaptive-icon.png`
- `assets/splash-icon.png`
- `assets/favicon.png`

**Commits:**
| # | Mensaje |
|---|---------|
| 1 | `feat: inicializar proyecto Expo SDK 54 con TypeScript` |
| 2 | `feat: configurar assets y variables de entorno` |

---

### miguel — Tipos y Capa API
**Rama:** `dev_miguel`
**Archivos a crear:**
- `src/types/index.ts`
- `src/lib/notion.ts`
- `src/lib/api.ts`
- `src/store/auth.ts`

**Commits:**
| # | Mensaje |
|---|---------|
| 3 | `feat: definir tipos TypeScript (User, Resource, LoginResponse)` |
| 4 | `feat: implementar cliente API de Notion y utilidades HTTP` |

---

### andres — Servicios
**Rama:** `dev_andres`
**Archivos a crear:**
- `src/services/auth.ts`
- `src/services/resources.ts`

**Commits:**
| # | Mensaje |
|---|---------|
| 5 | `feat: crear servicio de autenticación con validación numérica` |
| 6 | `feat: implementar servicio de recursos con filtros por clase y estado` |

---

### justin — Estado Global y Login
**Rama:** `dev_justin`
**Archivos a crear:**
- `src/context/AuthContext.tsx`
- `app/_layout.tsx`
- `app/index.tsx`

**Commits:**
| # | Mensaje |
|---|---------|
| 7 | `feat: crear AuthContext para gestión global de sesión` |
| 8 | `feat: implementar layout raíz y pantalla de login` |

---

### juan — Rutas Protegidas y Dashboard
**Rama:** `dev_juan`
**Archivos a crear:**
- `app/(app)/_layout.tsx`
- `app/(app)/index.tsx`

**Commits:**
| # | Mensaje |
|---|---------|
| 9 | `feat: crear layout protegido con verificación de sesión` |
| 10 | `feat: desarrollar dashboard con FlatList de recursos y logout` |

---

## Orden de Ejecución

```
johan (1-2) → miguel (3-4) → andres (5-6) → justin (7-8) → juan (9-10)
```

**Importante:** Cada integrante debe esperar a que el anterior termine sus commits antes de empezar los suyos.

Al finalizar, se hará un merge de todas las ramas a `master`.

---

## Comandos Útiles

```bash
# Crear rama
git checkout -b dev_[tu_nombre]

# Ver estado
git status

# Subir cambios
git push origin dev_[tu_nombre]
```

---

## Estructura del Proyecto

```
gestor-pinto-app/
├── app/
│   ├── _layout.tsx          # Root: SafeAreaView + AuthProvider
│   ├── index.tsx            # LoginScreen
│   └── (app)/
│       ├── _layout.tsx      # Protected: redirect si no hay user
│       └── index.tsx        # DashboardScreen: FlatList + recursos
├── src/
│   ├── types/index.ts       # Tipos User, Resource, LoginResponse
│   ├── lib/
│   │   ├── notion.ts        # Cliente API Notion
│   │   └── api.ts           # Utilidades HTTP
│   ├── services/
│   │   ├── auth.ts          # Login vía Notion DB
│   │   └── resources.ts     # Recursos por clase
│   ├── store/auth.ts        # Helpers de AsyncStorage
│   └── context/AuthContext.tsx  # Estado de sesión global
├── assets/
│   ├── icon.png
│   ├── adaptive-icon.png
│   ├── splash-icon.png
│   └── favicon.png
├── .env.example             # Ejemplo de variables de entorno
├── package.json
├── tsconfig.json
├── app.json
└── babel.config.js
```

---

## API

- **Login:** `POST /api/auth/login` → `{ success, user }`
- **Resources:** `GET /api/resources?clase=...` → `{ resources: [...] }`
- **Password numérico:** validar con `/^\d+$/` antes de enviar

---

## Diseño

- **Fondo:** #F9FAFB
- **Header/cards:** #0F172A
- **Errores:** #DC2626
- **Links:** #0070F3
- **Botón primario:** full-width, bg #0F172A, borderRadius 12
- **Inputs:** borderRadius 12, border #D1D5DB

---

## Convenciones

- Sin comentarios en código
- StyleSheet.create() preferido
- Estados: loading, error, data
- Errores de red con Alert.alert()
- Pull-to-refresh siempre hace fetch
