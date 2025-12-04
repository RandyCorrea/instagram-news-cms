# Instagram News CMS - Setup Completo

Guía para configurar y ejecutar el proyecto localmente, luego desplegarlo en GitHub Pages.

## 📋 Requisitos

- Node.js 18+
- npm o yarn
- Git
- GitHub account

## 🚀 Instalación Rápida

### 1. Clonar el repositorio

```bash
git clone https://github.com/RandyCorrea/instagram-news-cms.git
cd instagram-news-cms
```

### 2. Instalar dependencias

```bash
npm install
```

### 3. Crear estructura de carpetas

Crea estas carpetas manualmente o con el comando:

```bash
mkdir -p app/post/\[slug\] app/admin-secret-access components lib content/posts public
```

## 📁 Estructura Completa de Archivos

Todos los archivos necesarios están incluidos. Asegúrate de tener esta estructura:

```
instagram-news-cms/
├── .github/workflows/deploy.yml
├── app/
│   ├── globals.css
│   ├── layout.tsx
│   ├── page.tsx
│   ├── admin-secret-access/
│   │   └── page.tsx
│   └── post/
│       └── [slug]/
│           └── page.tsx
├── components/
│   ├── AdminPostForm.tsx
│   ├── FeedPost.tsx
│   ├── Header.tsx
│   ├── LoginForm.tsx
│   ├── PostDetail.tsx
│   └── ShareButtons.tsx
├── content/
│   └── posts/
│       └── (archivos .md)
├── lib/
│   ├── github.ts
│   ├── posts.ts
│   └── types.ts
├── public/
├── .gitignore
├── next.config.js
├── package.json
├── postcss.config.js
├── tailwind.config.js
├── tsconfig.json
└── README.md
```

## 🔧 Configuración de Variables de Entorno

Crea archivo `.env.local` en la raíz:

```
NEXT_PUBLIC_ADMIN_PASSWORD=tu_contraseña_segura_aqui
NEXT_PUBLIC_BASE_PATH=/instagram-news-cms
NEXT_PUBLIC_GITHUB_TOKEN=tu_token_github
NEXT_PUBLIC_GITHUB_REPO=instagram-news-cms
NEXT_PUBLIC_GITHUB_OWNER=tu_usuario
```

## 💻 Desarrollo Local

### Ejecutar servidor de desarrollo

```bash
npm run dev
```

Visita: http://localhost:3000

### Acceder al CMS

- URL: http://localhost:3000/admin-secret-access
- Contraseña: (la que configuraste en .env.local)

## 🌍 Desplegar en GitHub Pages

### 1. Configurar GitHub Pages

En tu repositorio:
1. Ve a Settings → Pages
2. En "Source", selecciona "GitHub Actions"
3. Confirma

### 2. Configurar GitHub Actions

El workflow `.github/workflows/deploy.yml` se ejecutará automáticamente.

Verifica que el workflow se ejecutó:
1. Ve a Actions
2. Busca el último workflow
3. Debe estar en verde ✓

### 3. URL de tu sitio

Tu sitio estará disponible en:
```
https://RandyCorrea.github.io/instagram-news-cms
```

## 📰 Crear tu Primer Post

### Vía CMS (Admin Panel)

1. Accede a `/admin-secret-access`
2. Introduce la contraseña
3. Completa el formulario con:
   - Título
   - Descripción corta (excerpt)
   - Contenido (Markdown soportado)
   - Imagen (1080x1350 ideal)
   - Fecha de publicación
4. Click en "Publicar"

### Vía Archivos Markdown (Manual)

Crea archivo `content/posts/mi-primer-post.md`:

```markdown
---
title: Mi Primer Post
excerpt: Una breve descripción del post
date: 2024-01-15T10:00:00Z
publishAt: 2024-01-15T10:00:00Z
coverImage: https://url-imagen.jpg
status: published
---

# Contenido del Post

Este es el contenido en Markdown. Soporta **negrita**, *cursiva*, listas, etc.
```

## 🎨 Diseño

El proyecto usa **Tailwind CSS** con tema oscuro tipo Instagram:
- Colores: Negros y grises oscuros
- Diseño mobile-first
- Responsive en desktop

## 🔐 Seguridad del CMS

### Autenticación

- Contraseña en `.env.local`
- Máximo 3 intentos fallidos
- Bloqueo de 30 días en IP tras 3 fallos
- LocalStorage + opcional Firebase para bloqueo real por IP

### Persistencia

- Los posts se guardan en `content/posts/`
- Al publicar desde CMS, se crea/actualiza el archivo `.md`
- Se dispara GitHub Actions para reconstruir el sitio

## 🚢 Pipeline CI/CD

Cada vez que hagas push a `main`:
1. GitHub Actions ejecuta el workflow
2. `npm install && npm run build`
3. Genera archivos estáticos en `/out`
4. Deploy automático a `gh-pages`
5. Sitio actualizado en ~2 minutos

## 📱 Features Implementados

✅ Feed estilo Instagram
✅ Detalles de noticia con URL única
✅ Open Graph & Twitter Cards (SEO)
✅ Botones de compartir (Web Share API, WhatsApp, Twitter, Facebook)
✅ Acortador de URLs (TinyURL API)
✅ CMS integrado con panel admin
✅ Autenticación por contraseña
✅ Bloqueo por intentos fallidos
✅ Soporte para imágenes y videos
✅ Markdown renderizado
✅ Hospedaje en GitHub Pages
✅ Build automático vía GitHub Actions

## 🛠️ Troubleshooting

### Error: "Module not found"
```bash
rm -rf node_modules package-lock.json
npm install
```

### El CMS no aparece
- Verifica que estés en `/admin-secret-access` exactamente
- Limpia caché del navegador

### GitHub Pages no actualiza
- Ve a Actions y verifica que el workflow termine sin errores
- Espera ~2 minutos para que se propague

### Imágenes no se ven
- Asegúrate de que las URLs sean públicas
- Usa URLs HTTPS siempre

## 📚 Recursos Útiles

- [Next.js Docs](https://nextjs.org/docs)
- [Tailwind CSS](https://tailwindcss.com)
- [GitHub Pages](https://pages.github.com)
- [Gray Matter (Frontmatter)](https://github.com/jonschlinkert/gray-matter)

## 📄 Licencia

MIT
