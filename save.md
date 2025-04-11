npm install @mdx-js/react @mdx-js/rollup prism-react-renderer
npm install -D tailwindcss postcss autoprefixer
npm install class-variance-authority clsx tailwind-merge lucide-react


import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import mdx from '@mdx-js/rollup';

/////

export default defineConfig({
plugins: [
mdx(),
react()
],
});

////


/** @type {import('tailwindcss').Config} */
export default {
darkMode: ["class"],
content: [
"./index.html",
"./src/**/*.{js,ts,jsx,tsx,mdx}",
],
theme: {
container: {
center: true,
padding: "2rem",
screens: {
"2xl": "1400px",
},
},
extend: {
colors: {
border: "hsl(var(--border))",
input: "hsl(var(--input))",
ring: "hsl(var(--ring))",
background: "hsl(var(--background))",
foreground: "hsl(var(--foreground))",
primary: {
DEFAULT: "hsl(var(--primary))",
foreground: "hsl(var(--primary-foreground))",
},
secondary: {
DEFAULT: "hsl(var(--secondary))",
foreground: "hsl(var(--secondary-foreground))",
},
destructive: {
DEFAULT: "hsl(var(--destructive))",
foreground: "hsl(var(--destructive-foreground))",
},
muted: {
DEFAULT: "hsl(var(--muted))",
foreground: "hsl(var(--muted-foreground))",
},
accent: {
DEFAULT: "hsl(var(--accent))",
foreground: "hsl(var(--accent-foreground))",
},
popover: {
DEFAULT: "hsl(var(--popover))",
foreground: "hsl(var(--popover-foreground))",
},
card: {
DEFAULT: "hsl(var(--card))",
foreground: "hsl(var(--card-foreground))",
},
},
borderRadius: {
lg: "var(--radius)",
md: "calc(var(--radius) - 2px)",
sm: "calc(var(--radius) - 4px)",
},
keyframes: {
"accordion-down": {
from: { height: 0 },
to: { height: "var(--radix-accordion-content-height)" },
},
"accordion-up": {
from: { height: "var(--radix-accordion-content-height)" },
to: { height: 0 },
},
},
animation: {
"accordion-down": "accordion-down 0.2s ease-out",
"accordion-up": "accordion-up 0.2s ease-out",
},
},
},
plugins: [],
}

//////


@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {
:root {
--background: 0 0% 100%;
--foreground: 222.2 84% 4.9%;

    --card: 0 0% 100%;
    --card-foreground: 222.2 84% 4.9%;
 
    --popover: 0 0% 100%;
    --popover-foreground: 222.2 84% 4.9%;
 
    --primary: 222.2 47.4% 11.2%;
    --primary-foreground: 210 40% 98%;
 
    --secondary: 210 40% 96.1%;
    --secondary-foreground: 222.2 47.4% 11.2%;
 
    --muted: 210 40% 96.1%;
    --muted-foreground: 215.4 16.3% 46.9%;
 
    --accent: 210 40% 96.1%;
    --accent-foreground: 222.2 47.4% 11.2%;
 
    --destructive: 0 84.2% 60.2%;
    --destructive-foreground: 210 40% 98%;
 
    --border: 214.3 31.8% 91.4%;
    --input: 214.3 31.8% 91.4%;
    --ring: 222.2 84% 4.9%;
 
    --radius: 0.5rem;
}

.dark {
--background: 222.2 84% 4.9%;
--foreground: 210 40% 98%;

    --card: 222.2 84% 4.9%;
    --card-foreground: 210 40% 98%;
 
    --popover: 222.2 84% 4.9%;
    --popover-foreground: 210 40% 98%;
 
    --primary: 210 40% 98%;
    --primary-foreground: 222.2 47.4% 11.2%;
 
    --secondary: 217.2 32.6% 17.5%;
    --secondary-foreground: 210 40% 98%;
 
    --muted: 217.2 32.6% 17.5%;
    --muted-foreground: 215 20.2% 65.1%;
 
    --accent: 217.2 32.6% 17.5%;
    --accent-foreground: 210 40% 98%;
 
    --destructive: 0 62.8% 30.6%;
    --destructive-foreground: 210 40% 98%;
 
    --border: 217.2 32.6% 17.5%;
    --input: 217.2 32.6% 17.5%;
    --ring: 212.7 26.8% 83.9%;
}
}

@layer base {
* {
  @apply border-border;
  }
  body {
  @apply bg-background text-foreground;
  }
  }

/* Estilos específicos para markdown */
.markdown-body {
@apply text-foreground max-w-full;
}

.markdown-body h1,
.markdown-body h2,
.markdown-body h3,
.markdown-body h4,
.markdown-body h5,
.markdown-body h6 {
@apply font-bold leading-tight mt-6 mb-2;
}

.markdown-body h1 {
@apply text-4xl;
}

.markdown-body h2 {
@apply text-3xl;
}

.markdown-body h3 {
@apply text-2xl;
}

.markdown-body h4 {
@apply text-xl;
}

.markdown-body p {
@apply my-4;
}

.markdown-body a {
@apply text-primary hover:underline;
}

.markdown-body ul {
@apply list-disc pl-6 my-4;
}

.markdown-body ol {
@apply list-decimal pl-6 my-4;
}

.markdown-body li {
@apply my-1;
}

.markdown-body blockquote {
@apply border-l-4 border-muted pl-4 italic my-4 text-muted-foreground;
}

.markdown-body img {
@apply max-w-full;
}

.markdown-body pre {
@apply rounded-md bg-muted p-4 overflow-auto my-4;
}

.markdown-body code:not(pre code) {
@apply bg-muted px-1.5 py-0.5 rounded text-sm;
}

.markdown-body table {
@apply w-full border-collapse my-4;
}

.markdown-body th {
@apply bg-muted px-4 py-2 text-left font-bold;
}

.markdown-body td {
@apply border px-4 py-2;
}


/////



import { clsx } from "clsx";
import { twMerge } from "tailwind-merge";

export function cn(...inputs) {
return twMerge(clsx(inputs));
}

//////

MDXComponents.jsx
import React from 'react';
import { Prism as SyntaxHighlighter } from 'react-syntax-highlighter';
import { vscDarkPlus } from 'react-syntax-highlighter/dist/esm/styles/prism';
import { cn } from '../lib/utils';

const MDXComponents = {
h1: ({ className, ...props }) => (
<h1
className={cn(
"scroll-m-20 text-4xl font-extrabold tracking-tight lg:text-5xl",
className
)}
{...props}
/>
),
h2: ({ className, ...props }) => (
<h2
className={cn(
"scroll-m-20 border-b pb-2 text-3xl font-semibold tracking-tight first:mt-0",
className
)}
{...props}
/>
),
h3: ({ className, ...props }) => (
<h3
className={cn(
"scroll-m-20 text-2xl font-semibold tracking-tight",
className
)}
{...props}
/>
),
h4: ({ className, ...props }) => (
<h4
className={cn(
"scroll-m-20 text-xl font-semibold tracking-tight",
className
)}
{...props}
/>
),
p: ({ className, ...props }) => (
<p
className={cn("leading-7 [&:not(:first-child)]:mt-6", className)}
{...props}
/>
),
a: ({ className, ...props }) => (
<a
className={cn(
"font-medium text-primary underline underline-offset-4",
className
)}
{...props}
/>
),
ul: ({ className, ...props }) => (
<ul
className={cn("my-6 ml-6 list-disc [&>li]:mt-2", className)}
{...props}
/>
),
ol: ({ className, ...props }) => (
<ol
className={cn("my-6 ml-6 list-decimal [&>li]:mt-2", className)}
{...props}
/>
),
li: ({ className, ...props }) => (
<li
className={cn("", className)}
{...props}
/>
),
blockquote: ({ className, ...props }) => (
<blockquote
className={cn(
"mt-6 border-l-2 border-primary pl-6 italic text-muted-foreground",
className
)}
{...props}
/>
),
img: ({ className, ...props }) => (
<img
className={cn("rounded-md border", className)}
{...props}
/>
),
hr: ({ ...props }) => (
<hr className="my-4 md:my-8" {...props} />
),
table: ({ className, ...props }) => (
<div className="my-6 w-full overflow-y-auto">
<table
className={cn("w-full", className)}
{...props}
/>
</div>
),
tr: ({ className, ...props }) => (
<tr
className={cn(
"m-0 border-t p-0 even:bg-muted",
className
)}
{...props}
/>
),
th: ({ className, ...props }) => (
<th
className={cn(
"border px-4 py-2 text-left font-bold [&[align=center]]:text-center [&[align=right]]:text-right",
className
)}
{...props}
/>
),
td: ({ className, ...props }) => (
<td
className={cn(
"border px-4 py-2 text-left [&[align=center]]:text-center [&[align=right]]:text-right",
className
)}
{...props}
/>
),
code: ({ className, children, ...props }) => {
const match = /language-(\w+)/.exec(className || '');
return match ? (
<SyntaxHighlighter
style={vscDarkPlus}
language={match[1]}
PreTag="div"
className="rounded-md my-6"
{...props}
>
{String(children).replace(/\n$/, '')}
</SyntaxHighlighter>
) : (
<code
className={cn(
"relative rounded bg-muted px-[0.3rem] py-[0.2rem] font-mono text-sm",
className
)}
{...props}
>
{children}
</code>
);
},
pre: ({ className, ...props }) => (
<pre
className={cn(
"mb-4 mt-6 overflow-x-auto rounded-lg border bg-black p-4",
className
)}
{...props}
/>
),
};

export default MDXComponents;


////
MDXProvider.jsx
import React from 'react';
import { MDXProvider } from '@mdx-js/react';
import MDXComponents from './MDXComponents';

const CustomMDXProvider = ({ children }) => {
return <MDXProvider components={MDXComponents}>{children}</MDXProvider>;
};

export default CustomMDXProvider;

////
main.jsx
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App.jsx'
import './index.css'
import CustomMDXProvider from './components/MDXProvider.jsx'

ReactDOM.createRoot(document.getElementById('root')).render(
<React.StrictMode>
<CustomMDXProvider>
<App />
</CustomMDXProvider>
</React.StrictMode>,
)


//// 

import React from 'react';
import { MDXProvider } from '@mdx-js/react';
import MDXComponents from './MDXComponents';
import { cn } from '../lib/utils';

// Este componente é para renderizar markdown dinâmico
// Nota: Para renderização dinâmica, você precisará de uma biblioteca adicional
// como mdx-bundler ou next-mdx-remote
const MarkdownRenderer = ({ content, className }) => {
return (
<div className={cn("markdown-body", className)}>
<MDXProvider components={MDXComponents}>
{/* Aqui você precisaria de uma forma de renderizar o markdown dinamicamente */}
<div dangerouslySetInnerHTML={{ __html: content }} />
</MDXProvider>
</div>
);
};

export default MarkdownRenderer;



//////


import React from 'react';
import { useState } from 'react';
import './App.css';

// Importando um arquivo MDX
import ExampleMDX from './content/example.mdx';

function App() {
return (
<div className="container mx-auto py-10 px-4">
<div className="max-w-3xl mx-auto">
<div className="prose dark:prose-invert">
<ExampleMDX />
</div>
</div>
</div>
);
}

export default App;



//// 


# Markdown com React e shadcn/ui

## Introdução

Este é um exemplo de **Markdown** renderizado com _React_ e estilizado como **shadcn/ui**.

## Código de Exemplo

```javascript
// Exemplo de código
function exemplo() {
  return "Olá, mundo!";
}




