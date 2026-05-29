# GestorPinto Móvil

Expo SDK **54** (blank-typescript), migración desde web Next.js.

## Stack (verificar instalación)

| Paquete | Propósito |
|---------|-----------|
| expo-router | Navegación file-based (`app/`) |
| @react-native-async-storage/async-storage | Persistencia sesión |
| @expo/vector-icons | Iconos |

## Comandos

```bash
npm start              # Expo dev server
npm run android        # Android emulator
npm run ios            # iOS simulator (macOS)
npm run web            # Web preview
```

## API

- Base: `EXPO_PUBLIC_API_BASE_URL` (`.env` local), prefijo `EXPO_PUBLIC_` requerido por Expo.
- **No CORS** en React Native.
- **No JWT / cookies** — sesión por user persistido en AsyncStorage.
- Login: `POST /api/auth/login` { email, password } → `{ success, user }` | `{ success, error }`.
- Resources: `GET /api/resources?clase=...` → `{ resources: [...] }`.

## ⚠️ Quirk crítico: password numérico

El backend hace `Number.parseInt(password, 10)`. Si el password contiene letras, responde "Credenciales incorrectas" **sin consultar Notion**. Validar con `/^\d+$/` antes de enviar.

## Navegación

```
app/
  _layout.tsx    # Root: SafeAreaView + StatusBar
  index.tsx      # LoginScreen → redirect a (app)/ si hay sesión
  (app)/
    _layout.tsx  # Protegido: redirect a / si no hay user en AsyncStorage
    index.tsx    # DashboardScreen: FlatList + RefreshControl + Linking
```

- Al abrir app: leer `user` de AsyncStorage → Dashboard si existe, Login si no.
- Logout: `AsyncStorage.clear()` + `router.replace("/")`.

## Diseño

- Fondo: `#F9FAFB`. Header/cards: `#0F172A`. Errores: `#DC2626`. Links: `#0070F3`.
- Botón primario: full-width, `bg #0F172A`, texto blanco, `borderRadius: 12`.
- Inputs: `borderRadius: 12`, border `#D1D5DB`, padding vertical 12px horizontal 16px.
- Tarjetas recurso: `borderRadius: 12`, border `#EAEAEA`, padding 24px, sombra ligera.
- Botón logout: texto `#DC2626`, sin bg.

## Convenciones

- Sin comentarios en código.
- Preferir `StyleSheet.create()` sobre inline styles.
- Estados: `loading`, `error`, `data` — manejar los tres.
- Errores de red con `Alert.alert()` nativo.
- Pull-to-refresh: siempre hace fetch (sin TTL).

## Lectura obligatoria

Antes de escribir cualquier código: leer docs de Expo v54 en
https://docs.expo.dev/versions/v54.0.0/
