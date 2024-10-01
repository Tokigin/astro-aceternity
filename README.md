# Astro + Aceternity

I really like to use Aceternity Ui in Nextjs but sometime, I don't really need Nextjs to develop a project. About half of my new projects are done in Astro SSG. So, I thought, why not use Aceternity Ui in Astro.

## Reference

https://docs.astro.build/en/install-and-setup

https://www.framer.com/motion/introduction

https://ui.shadcn.com/docs/installation/astro

https://ui.aceternity.com/docs/add-utilities

## Installation

I use [Bun](https://bun.sh/) here. 
> There is some problem with using shardcn cli with npm ([#issue](https://github.com/Tokigin/astro-aceternity/issues/2)) but still no problem with bun. I will find the easy fix and update this instruction.

### 1. Creating Astro Project

```sh
bun create astro@latest
```

```text

dir   Where should we create your new project?
         ./project-name

tmpl   How would you like to start your new project?
         Empty

ts   Do you plan to write TypeScript?
         Yes

use   How strict should TypeScript be?
         Strict

deps   Install dependencies?
         Yes

git   Initialize a new git repository?
         No

```

```sh
cd project-name
```

### 2. Add React

```sh
bunx astro add react
```

Answer `Yes` to all the questions.

### 3. Add Tailwind

```sh
bunx astro add tailwind
```

Answer `Yes` to all the questions.

Add the following code to the tsconfig.json file to resolve paths:

```text
{
  "compilerOptions": {
    // ...
    "baseUrl": ".",
    "paths": {
      "@/*": [
        "./src/*"
      ]
    }
    // ...
  }
}
```

### 4. Install Shardcn Ui

```sh
bunx shadcn@latest init
```

```text
√ Would you like to use TypeScript (recommended)? ... yes
√ Which style would you like to use? » Default
√ Which color would you like to use as base color? » Slate
√ Where is your global CSS file? ... ./src/styles/globals.css
√ Would you like to use CSS variables for colors? ... no
√ Are you using a custom tailwind prefix eg. tw-? (Leave blank if not) ...
√ Where is your tailwind.config.js located? ... tailwind.config.mjs
√ Configure the import alias for components: ... @/components
√ Configure the import alias for utils: ... @/lib/utils
√ Are you using React Server Components? ... no
√ Write configuration to components.json. Proceed? ... yes
```

Import the `globals.css` file in the `@/pages/index.astro` file:

```text
---
import '@/styles/globals.css'
---
```

Update `astro.config.mjs` :

```text
export default defineConfig({
  integrations: [
    //your code,
    tailwind({
      applyBaseStyles: false,
    }),
  ],
})
```

Update `tailwind.config.mjs` :

```text
export default {
//your code,
  content: ["./src/**/*.{astro,html,js,jsx,md,mdx,svelte,ts,tsx,vue}"],
}

```

### 5. Install Framer Motion

```sh
bun i framer-motion clsx tailwind-merge
```

### 6. Add Aceternity Ui component

```sh
bunx aceternity-ui@latest add 3d-card
```

Remove `"use client";` as it is from `Nextjs`. We are using `Astro` so we don't need Nextjs Syntax.

Remove `import Image from "next/image";` and use normal `<img>` tag.

or

Replace it with `import { Image } from 'astro:assets';`.

### 7. Using Aceternity Ui component

Create `threedcarddemo.tsx` in `"@/components/"`.

Copy and Paste the code from https://ui.aceternity.com/components/3d-card-effect example.

Remove :

```text
"use client";
import Image from "next/image";
import React from "react";
```

Import component in the `@/pages/index.astro` file:

```text
---
import { ThreeDCardDemo } from "@/components/threedcarddemo";
---
```

You can use `client:idle` or `client:load` as you like.

```text
<ThreeDCardDemo client:idle />
```

## Project Structure

```text
/
├── public/
├── src/
│   └── components/
│       └── ui
│   └── lib/
│       └── utils.ts
│   └── pages/
│       └── index.astro
│   └── styles/
│       └── globals.css
│   └── env.d.ts
└── astro.config.mjs
└── components.json
└── package.json
└── tailwind.config.mjs
└── tsconfig.json
```
