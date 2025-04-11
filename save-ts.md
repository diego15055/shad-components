npm install @mdx-js/react @mdx-js/rollup prism-react-renderer
npm install -D tailwindcss postcss autoprefixer
npm install class-variance-authority clsx tailwind-merge lucide-react




import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import mdx from '@mdx-js/rollup';

export default defineConfig({
plugins: [
mdx(),
react()
],
});





import { type ClassValue, clsx } from "clsx";
import { twMerge } from "tailwind-merge";

export function cn(...inputs: ClassValue[]): string {
return twMerge(clsx(inputs));
}




declare module '*.mdx' {
import type { ComponentType } from 'react';

const MDXComponent: ComponentType;

export default MDXComponent;
}




import React, { ReactNode } from 'react';
import { Prism as SyntaxHighlighter } from 'react-syntax-highlighter';
import { vscDarkPlus } from 'react-syntax-highlighter/dist/esm/styles/prism';
import { cn } from '../lib/utils';

interface ComponentProps {
className?: string;
children?: ReactNode;
[key: string]: any;
}

interface CodeProps extends ComponentProps {
className?: string;
children: ReactNode;
}

const MDXComponents = {
h1: ({ className, ...props }: ComponentProps) => (
<h1
className={cn(
"scroll-m-20 text-4xl font-extrabold tracking-tight lg:text-5xl",
className
)}
{...props}
/>
),
h2: ({ className, ...props }: ComponentProps) => (
<h2
className={cn(
"scroll-m-20 border-b pb-2 text-3xl font-semibold tracking-tight first:mt-0",
className
)}
{...props}
/>
),
h3: ({ className, ...props }: ComponentProps) => (
<h3
className={cn(
"scroll-m-20 text-2xl font-semibold tracking-tight",
className
)}
{...props}
/>
),
h4: ({ className, ...props }: ComponentProps) => (
<h4
className={cn(
"scroll-m-20 text-xl font-semibold tracking-tight",
className
)}
{...props}
/>
),
p: ({ className, ...props }: ComponentProps) => (
<p
className={cn("leading-7 [&:not(:first-child)]:mt-6", className)}
{...props}
/>
),
a: ({ className, ...props }: ComponentProps) => (
<a
className={cn(
"font-medium text-primary underline underline-offset-4",
className
)}
{...props}
/>
),
ul: ({ className, ...props }: ComponentProps) => (
<ul
className={cn("my-6 ml-6 list-disc [&>li]:mt-2", className)}
{...props}
/>
),
ol: ({ className, ...props }: ComponentProps) => (
<ol
className={cn("my-6 ml-6 list-decimal [&>li]:mt-2", className)}
{...props}
/>
),
li: ({ className, ...props }: ComponentProps) => (
<li
className={cn("", className)}
{...props}
/>
),
blockquote: ({ className, ...props }: ComponentProps) => (
<blockquote
className={cn(
"mt-6 border-l-2 border-primary pl-6 italic text-muted-foreground",
className
)}
{...props}
/>
),
img: ({ className, ...props }: ComponentProps) => (
<img
className={cn("rounded-md border", className)}
{...props}
/>
),
hr: ({ ...props }: ComponentProps) => (
<hr className="my-4 md:my-8" {...props} />
),
table: ({ className, ...props }: ComponentProps) => (
<div className="my-6 w-full overflow-y-auto">
<table
className={cn("w-full", className)}
{...props}
/>
</div>
),
tr: ({ className, ...props }: ComponentProps) => (
<tr
className={cn(
"m-0 border-t p-0 even:bg-muted",
className
)}
{...props}
/>
),
th: ({ className, ...props }: ComponentProps) => (
<th
className={cn(
"border px-4 py-2 text-left font-bold [&[align=center]]:text-center [&[align=right]]:text-right",
className
)}
{...props}
/>
),
td: ({ className, ...props }: ComponentProps) => (
<td
className={cn(
"border px-4 py-2 text-left [&[align=center]]:text-center [&[align=right]]:text-right",
className
)}
{...props}
/>
),
code: ({ className, children, ...props }: CodeProps) => {
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
pre: ({ className, ...props }: ComponentProps) => (
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






import React, { ReactNode } from 'react';
import { MDXProvider } from '@mdx-js/react';
import MDXComponents from './MDXComponents';

interface CustomMDXProviderProps {
children: ReactNode;
}

const CustomMDXProvider: React.FC<CustomMDXProviderProps> = ({ children }) => {
return <MDXProvider components={MDXComponents}>{children}</MDXProvider>;
};

export default CustomMDXProvider;






import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App.tsx'
import './index.css'
import CustomMDXProvider from './components/MDXProvider.tsx'

ReactDOM.createRoot(document.getElementById('root')!).render(
<React.StrictMode>
<CustomMDXProvider>
<App />
</CustomMDXProvider>
</React.StrictMode>,
)






import React from 'react';
import { MDXProvider } from '@mdx-js/react';
import MDXComponents from './MDXComponents';
import { cn } from '../lib/utils';

interface MarkdownRendererProps {
content: string;
className?: string;
}

// Este componente é para renderizar markdown dinâmico
// Nota: Para renderização dinâmica, você precisará de uma biblioteca adicional
// como mdx-bundler ou next-mdx-remote
const MarkdownRenderer: React.FC<MarkdownRendererProps> = ({ content, className }) => {
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







import React from 'react';
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






import { bundleMDX } from 'mdx-bundler';
import { getMDXComponent } from 'mdx-bundler/client';
import React, { useMemo } from 'react';

export async function compileMDX(source: string) {
if (!source) return { code: '' };

// esbuild precisa ser disponível
try {
const result = await bundleMDX({
source,
// Você pode adicionar opções adicionais aqui
});

    return result;
} catch (error) {
console.error('Error bundling MDX:', error);
return { code: '' };
}
}

export function useMDXComponent(code: string) {
return useMemo(() => {
if (!code) return () => null;

    // Converte o código compilado em um componente React
    const Component = getMDXComponent(code);
    return Component;
}, [code]);
}




import React, { useEffect, useState } from 'react';
import { compileMDX, useMDXComponent } from '../services/mdxService';
import { MDXProvider } from '@mdx-js/react';
import MDXComponents from './MDXComponents';
import { cn } from '../lib/utils';

interface DynamicMarkdownProps {
content: string;
className?: string;
}

const DynamicMarkdown: React.FC<DynamicMarkdownProps> = ({ content, className }) => {
const [compiledCode, setCompiledCode] = useState('');
const Component = useMDXComponent(compiledCode);

useEffect(() => {
async function compile() {
const result = await compileMDX(content);
setCompiledCode(result.code);
}

    compile();
}, [content]);

return (
<div className={cn("markdown-body", className)}>
<MDXProvider components={MDXComponents}>
{Component ? <Component /> : <p>Carregando...</p>}
</MDXProvider>
</div>
);
};

export default DynamicMarkdown;






