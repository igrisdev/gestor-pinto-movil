# GestorPinto Móvil - Guía de Trabajo

## Stack
- Expo SDK 54 (blank-typescript)
- expo-router (navegación file-based)
- AsyncStorage (persistencia)
- Notion API (backend directo)

## Comandos
```bash
npm start        # Expo dev server
npm run android  # Android emulator
npm run ios      # iOS simulator
npm run web      # Web preview
```

## Estructura
```
app/
  _layout.tsx        → Root: SafeAreaView + AuthProvider
  index.tsx          → LoginScreen
  (app)/
    _layout.tsx      → Protected: redirect si no hay user
    index.tsx        → DashboardScreen: FlatList + recursos
src/
  types/index.ts     → Tipos User, Resource, LoginResponse
  lib/notion.ts      → Cliente API Notion
  services/auth.ts   → Login vía Notion DB
  services/resources.ts → Recursos por clase
  context/AuthContext.tsx → Estado de sesión global
```

## API
- Base: `EXPO_PUBLIC_API_BASE_URL`
- Login: `POST /api/auth/login` → `{ success, user }`
- Resources: `GET /api/resources?clase=...` → `{ resources: [...] }`
- Password numérico: validar con `/^\d+$/` antes de enviar

## Diseño
- Fondo: #F9FAFB
- Header/cards: #0F172A
- Errores: #DC2626
- Links: #0070F3
- Botón primario: full-width, bg #0F172A, borderRadius 12
- Inputs: borderRadius 12, border #D1D5DB

## Convenciones
- Sin comentarios en código
- StyleSheet.create() preferido
- Estados: loading, error, data
- Errores de red con Alert.alert()
- Pull-to-refresh siempre hace fetch
