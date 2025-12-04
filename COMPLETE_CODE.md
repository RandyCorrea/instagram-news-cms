# ⚡ Instalación Rápida del Proyecto

**OPCIÓN 1: Clonar y Ejecutar (RECOMENDADO)**

Si prefieres tener TODO el código listo, clona este repositorio en tu máquina local:

```bash
git clone https://github.com/RandyCorrea/instagram-news-cms.git
cd instagram-news-cms
npm install
npm run dev
```

Luego accede a: http://localhost:3000

Para el CMS (admin): http://localhost:3000/admin-secret-access
Contraseña: admin123 (cámbiala en .env.local)

---

**OPCIÓN 2: Copiar Todos los Archivos Manualmente**

Si necesitas ver o copiar el código completo de cada archivo, está incluido abajo.
Copia todo el código correspondiente a cada archivo.

---

## 📋 Índice de Archivos Completos

### Archivos de Configuración
1. **tailwind.config.js** - Temas y estilos
2. **tsconfig.json** - Configuración de TypeScript
3. **postcss.config.js** - Configuración de PostCSS
4. **.env.local** - Variables de entorno
5. **.github/workflows/deploy.yml** - GitHub Actions

### Archivos de Tipos y Utilidades
1. **lib/types.ts** - Interfaces TypeScript
2. **lib/posts.ts** - Lógica de lectura de posts
3. **lib/github.ts** - Integración con GitHub API

### Componentes React
1. **components/Header.tsx** - Encabezado
2. **components/FeedPost.tsx** - Tarjeta en el feed
3. **components/PostDetail.tsx** - Página de detalle
4. **components/ShareButtons.tsx** - Botones de compartir
5. **components/AdminPostForm.tsx** - Formulario del CMS
6. **components/LoginForm.tsx** - Autenticación

### Páginas Next.js
1. **app/layout.tsx** - Layout principal
2. **app/globals.css** - Estilos globales
3. **app/page.tsx** - Feed principal
4. **app/post/[slug]/page.tsx** - Detalle del post
5. **app/admin-secret-access/page.tsx** - Panel del CMS

---

## 📁 ARCHIVOS DE CONFIGURACIÓN

### tailwind.config.js
```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    './app/**/*.{js,ts,jsx,tsx}',
    './components/**/*.{js,ts,jsx,tsx}',
  ],
  theme: {
    extend: {
      colors: {
        'instagram-dark': '#000000',
        'instagram-gray': '#121212',
        'instagram-light-gray': '#262626',
        'instagram-border': '#363636',
      },
      fontFamily: {
        sans: ['-apple-system', 'BlinkMacSystemFont', '\"Segoe UI\"', 'Roboto', '\"Helvetica Neue\"', 'Arial', 'sans-serif'],
      },
    },
  },
  plugins: [],
};
```

### tsconfig.json
```json
{
  "compilerOptions": {
    "target": "ES2020",
    "useDefineForClassFields": true,
    "lib": ["ES2020", "DOM", "DOM.Iterable"],
    "module": "ESNext",
    "skipLibCheck": true,
    "esModuleInterop": true,
    "allowSyntheticDefaultImports": true,
    "strict": true,
    "forceConsistentCasingInFileNames": true,
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "declaration": true,
    "declarationMap": true,
    "sourceMap": true,
    "jsx": "react-jsx",
    "baseUrl": ".",
    "paths": {
      "@/*": ["./*"]
    }
  },
  "include": ["app/**/*", "components/**/*", "lib/**/*"],
  "exclude": ["node_modules", ".next", "out"]
}
```

### postcss.config.js
```javascript
module.exports = {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  },
};
```

### .env.local
```
NEXT_PUBLIC_ADMIN_PASSWORD=admin123
NEXT_PUBLIC_BASE_PATH=/instagram-news-cms
NEXT_PUBLIC_GITHUB_TOKEN=tu_token_aqui
NEXT_PUBLIC_GITHUB_REPO=instagram-news-cms
NEXT_PUBLIC_GITHUB_OWNER=tu_usuario
```

### .github/workflows/deploy.yml
```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      pages: write
      id-token: write

    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '18'
          cache: 'npm'

      - run: npm ci
      - run: npm run build

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v2
        with:
          path: './out'

  deploy:
    needs: build
    runs-on: ubuntu-latest
    permissions:
      pages: write
      id-token: write
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v2
```

---

## 📄 ARCHIVOS PRINCIPALES

### lib/types.ts
```typescript
export interface Post {
  slug: string;
  title: string;
  excerpt: string;
  content: string;
  date: string;
  publishAt: string;
  coverImage?: string;
  videoProvider?: 'youtube' | 'vimeo';
  videoId?: string;
  status: 'draft' | 'published' | 'scheduled';
}

export interface PostFrontmatter {
  title: string;
  excerpt: string;
  date: string;
  publishAt: string;
  coverImage?: string;
  videoProvider?: 'youtube' | 'vimeo';
  videoId?: string;
  status: 'draft' | 'published' | 'scheduled';
}
```

---

⚡ **NOTA**: Los archivos de componentes y páginas son bastante grandes.
Consulta **SETUP.md** en el repositorio para ver el código completo de cada componente.

O clona el repositorio directamente:
```bash
git clone https://github.com/RandyCorrea/instagram-news-cms.git
```
