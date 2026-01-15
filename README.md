# Astro SSR on Render

This template deploys a server-side rendered [Astro](https://astro.build/) application on Render. It demonstrates SSR capabilities including dynamic content generation, request header access, and API routes.

## Features

- **Server-side rendering**: Pages render on every request with access to headers, cookies, and request data
- **API routes**: Built-in support for JSON API endpoints with GET and POST handlers
- **Standalone mode**: Uses the `@astrojs/node` adapter without Express or other frameworks
- **Tailwind CSS v4**: Modern styling with automatic content detection

## What is Astro SSR?

Unlike static site generation (SSG) where pages are built once at deploy time, SSR generates HTML on the server for every request. This enables:

- **Dynamic content**: Show real-time data like timestamps, user-specific content, or database results
- **Request context**: Access headers, cookies, and query parameters at render time
- **API endpoints**: Create backend routes alongside your pages

This template's homepage demonstrates SSR by displaying the server time and a random number that change on each page refresh.

## Local development

Install dependencies and start the development server:

```bash
npm install
npm run dev
```

The app runs at `http://localhost:4321` by default.

### Available scripts

| Script            | Description                                  |
| ----------------- | -------------------------------------------- |
| `npm run dev`     | Start the development server with hot reload |
| `npm run build`   | Build for production                         |
| `npm run preview` | Preview the production build locally         |
| `npm start`       | Run the production server                    |

## API routes

This template includes an example API endpoint at `src/pages/api/hello.ts`:

**GET** `/api/hello`

Returns a greeting with an optional `name` query parameter:

```bash
curl http://localhost:4321/api/hello?name=Astro
```

```json
{
  "message": "Hello, Astro!",
  "timestamp": "2025-01-15T12:00:00.000Z",
  "method": "GET"
}
```

**POST** `/api/hello`

Echoes back the JSON body you send:

```bash
curl -X POST http://localhost:4321/api/hello \
  -H "Content-Type: application/json" \
  -d '{"foo": "bar"}'
```

## Project structure

```
├── src/
│   ├── layouts/
│   │   └── Layout.astro       # Base HTML layout
│   ├── pages/
│   │   ├── index.astro        # Homepage with SSR demo
│   │   └── api/
│   │       └── hello.ts       # Example API endpoint
│   └── styles/
│       └── global.css         # Tailwind CSS entry point
├── public/                    # Static assets
├── astro.config.mjs           # Astro configuration
├── render.yaml                # Render deployment config
└── package.json
```

## Configuration

### Environment variables

| Variable | Description                      |
| -------- | -------------------------------- |
| `HOST`   | Server host (default: `0.0.0.0`) |
| `PORT`   | Server port (default: `4321`)    |

### Astro configuration

The `astro.config.mjs` file configures:

- **Output mode**: Set to `server` for SSR (use `hybrid` if you want some static pages)
- **Node adapter**: Runs in `standalone` mode without requiring Express
- **Tailwind**: Integrated via the Vite plugin

## Adding pages

Create new pages in `src/pages/`. Astro uses file-based routing:

- `src/pages/about.astro` → `/about`
- `src/pages/blog/[slug].astro` → `/blog/:slug` (dynamic route)
- `src/pages/api/users.ts` → `/api/users` (API route)

## Resources

- [Astro documentation](https://docs.astro.build/)
- [Astro Node adapter](https://docs.astro.build/en/guides/integrations-guide/node/)
- [Astro API routes](https://docs.astro.build/en/guides/endpoints/)
- [Render web services](https://render.com/docs/web-services)
