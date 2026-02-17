---
name: deno-hono
description: "Build and maintain web applications with Deno and Hono framework. Use when working with: (1) Creating new Deno/Hono projects or adding routes/components, (2) Debugging Hono apps (routing, middleware, context issues), (3) Explaining Hono concepts (JSX, middleware, routing patterns), (4) Working with TypeScript in Deno environment."
---

# Deno Hono

## Quick Start

```bash
deno task dev    # Start dev server with file watching
deno fmt        # Format code
deno lint        # Check for issues
```

## Project Structure

```
src/
├── index.tsx        # Main entry - all routes defined here
├── components/     # Reusable UI components (LayoutV2, Markdown, etc.)
├── app/            # Page components and content
│   ├── tools/      # Tool implementations (improve-text, is-site-down, etc.)
│   ├── wiki/      # Wiki-style content
│   └── [topics]/  # Content areas (web, react, python, etc.)
└── tools/          # Tool utilities
```

## Routing Pattern

Routes live in `src/index.tsx`:

```typescript
import { Hono } from "hono";
import { YourComponent } from "./app/your-component.tsx";

const app = new Hono();

app.get("/path", (c) => c.html(<YourComponent />));
```

### Route with Title

```typescript
const servePage = (component: Child, title?: string) => (c: Context) =>
  c.html(<LayoutV2 title={title}>{component}</LayoutV2>);

app.get("/about", servePage(<About />, "About"));
```

### GET/POST Pattern for Forms

```typescript
app.get("/tool", (c) => c.html(<ToolForm />));
app.post("/tool", async (c) => {
  const formData = await c.req.parseBody();
  // process data
  return c.html(<ToolResult data={result} />);
});
```

## Component Structure

Use `interface Props` for component props:

```typescript
import { PropsWithChildren } from "hono/jsx";

interface YourComponentProps {
  title?: string;
  items: string[];
}

export function YourComponent(
  { title, items }: YourComponentProps,
) {
  return (
    <div>
      {title && <h1>{title}</h1>}
      <ul>
        {items.map((item) => <li>{item}</li>)}
      </ul>
    </div>
  );
}
```

### Layout Component Pattern

```typescript
interface LayoutProps extends PropsWithChildren {
  title?: string;
  description?: string;
}

export function Layout({ children, title, description }: LayoutProps) {
  const pageTitle = title ? `${title} // SITE NAME` : "SITE NAME";

  return (
    <html lang="en">
      <head>
        <title>{pageTitle}</title>
        {description && <meta name="description" content={description} />}
        {/* other meta tags */}
      </head>
      <body>{children}</body>
    </html>
  );
}
```

## Middleware

### Logger Middleware

```typescript
app.use("*", async (c, next) => {
  const start = Date.now();
  await next();
  const end = Date.now();
  console.log(`${c.req.method} ${c.req.url} - ${c.res.status} ${end - start}ms`);
});
```

### Error Handling

```typescript
app.onError((err, c) => {
  console.error(`Error: ${err.message}`);
  return c.html(<ErrorPage message={err.message} />);
});
```

### 404 Handler

```typescript
app.notFound((c) => {
  c.status(404);
  return c.html(<NotFoundPage />);
});
```

## Key Conventions

- **No client-side React** - All rendering is server-side
- **CSS** - Define outside components using Hono's `css` helper or Tailwind
- **TypeScript** - Use interface for props, not inline types
- **Function declarations** - Prefer `function` over `const` for components
- **Dependencies** - Prefer built-in Deno/web APIs; add deps only for code > 20 lines

## Common Issues

- **Route not matching**: Check route order - more specific routes must come first
- **Context errors**: Ensure `c` is passed correctly in middleware chain
- **JSX not rendering**: Verify `hono/jsx` is imported and `.tsx` extension used

## References

- [Hono Documentation](https://hono.dev/) - Official Hono docs
- [Deno Docs](https://deno.land/) - Deno runtime documentation
- [Markdown Rendering](./references/markdown.md) - Using the Markdown component
- [Tool Development](./references/tools.md) - Creating interactive tools
