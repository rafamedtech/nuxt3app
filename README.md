# Nuxt 3 + Tailwind CSS + Pinia + Supabase Starter

> Look at the [nuxt 3 documentation](https://v3.nuxtjs.org) to learn more.

## Setup

Make sure to install the dependencies:

```bash
# yarn (Recommended)
yarn install

# npm
npm install

```

## Setup Tailwind CSS

> Look at the [Tailwind documentation](https://tailwindcss.com/docs/guides/nuxtjs) to learn more.

Make sure to install Tailwind and all the dependencies with the `--dev` flag:

```bash
yarn add --dev tailwindcss postcss@latest autoprefixer@latest @nuxt/postcss8 prettier prettier-plugin-tailwindcss
```

Generate `tailwind.config.js` file

```bash
npx tailwindcss init
```

Include all the directories where **Tailwind** is going to purge all the unused utility classes inside the content array:

```javascript
// nuxt.config.ts

/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    './components/**/*.{js,vue,ts}',
    './layouts/**/*.vue',
    './pages/**/*.vue',
    './plugins/**/*.{js,ts}',
  ],

  theme: {
    extend: {},
  },
  plugins: {},
};
```

For some reason when I include the `"./nuxt.config.{js,ts}"` directory I got an error, maybe is something related with the RC so that's why I'm ignoring it this time.

Now let's add some customizations to the current **"container"** utility class in the `theme` object in order to get better distributed the content on bigger screens:

```javascript
// nuxt.config.ts

/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    // ...some code
  ],

  theme: {
    extend: {
      container: {
        center: true,
        screens: {
          lg: '1124px',
          xl: '1124px',
          '2xl': '1124px',
        },
      },
    },
  },

  plugins: {},
};
```

Create the `corePlugins` object in order to remove the opacity in some type of utility classes and get the **Hex** color instead of the **Tailwind** variable on **DevTools**:

```javascript
// nuxt.config.ts

/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    // ...some code
  ],
  theme: {
    extend: {
      // ...some code
    },
  },

  corePlugins: {
    textOpacity: false,
    backgroundOpacity: false,
    borderOpacity: false,
    divideOpacity: false,
    placeholderOpacity: false,
    ringOpacity: false,
  },

  plugins: {},
};
```

Include the `postcss` configurations for **tailwindcss** and **autoprefixer** within the `nuxt.config.ts` file:

```javascript
// nuxt.config.ts
import { defineNuxtConfig } from 'nuxt';

export default defineNuxtConfig({
  build: {
    postcss: {
      postcssOptions: {
        plugins: {
          tailwindcss: {},
          autoprefixer: {},
        },
      },
    },
  },
});
```

Create the directory **assets/css** and create a new file named `main.css`

<!-- screenshot -->

Include the new directory in your `nuxt.config.ts` file:

```javascript
// nuxt.config.ts

import { defineNuxtConfig } from 'nuxt';

export default defineNuxtConfig({
  css: ['@/assets/css/main.css'],

  build: {
    // ...some code
  },
});
```

Delete the `app.vue` file and create a **pages** folder and an `index.vue` file inside:

<!-- screenshot -->

Let's add some content to our `index.vue` file with **Tailwind CSS** classes to try this out:

```html
<!-- pages/index.vue -->
<template>
  <div
    class="grid h-screen place-items-center bg-gradient-to-tr from-green-900 via-gray-900 to-green-900"
  >
    <section class="rounded-3xl border border-gray-700 bg-gray-900 text-gray-400 shadow-2xl">
      <div class="container mx-auto flex flex-col items-center px-12 py-24 md:flex-row">
        <div
          class="mb-16 flex flex-col items-center text-center md:mb-0 md:w-1/2 md:items-start md:pr-16 md:text-left lg:flex-grow lg:pr-24"
        >
          <h1 class="title-font mb-4 text-3xl font-medium text-white sm:text-4xl">
            Welcome to your new Nuxt 3 app
          </h1>
          <p class="mb-8 leading-relaxed">This project is a Vue.js application using Nuxt 3.</p>
        </div>
      </div>
    </section>
  </div>
</template>
```

## Setup Pinia

> Look at the [Pinia documentation](https://pinia.vuejs.org/ssr/nuxt.html) to learn more.

To setup **pinia** we need to install the dependencies first:

```bash
# yarn
yarn add pinia @nuxt/pinia

# npm
npm install pinia @pinia/nuxt

```

Include `@pinia/nuxt` in the `buildModules` array in your `nuxt.config.ts` file:

```javascript
// nuxt.config.ts

import { defineNuxtConfig } from 'nuxt';

export default defineNuxtConfig({
  css: [
    // ...some code
  ],

  buildModules: ['@pinia/nuxt'],

  build: {
    // ...some code
  },
});
```

Create a **stores** directory and a `.ts` file called however you like for your store in this time I'm calling it `main.ts`:

<!-- screenshot -->

In `main.ts` create a new store by importing `{ defineStore }` from `pinia`:

```javascript
// stores/main.ts

import { defineStore } from 'pinia';
```

Create a store by declaring a variable that will be exported using **_"use"_** before the name of the store for convention purposes and this will be equal to the imported `defineStore` who receives two parameters: a string with the name of the store (I don't understand why) and an object:

```javascript
// stores/main.ts

import { defineStore } from 'pinia';

export const useMainStore = defineStore('main', {});
```

Inside the object we can setup our `state`, `actions`, and `getters`:

```javascript
// stores/main.ts

import { defineStore } from 'pinia';

export const useStore = defineStore('main', {
  state: () => ({}),
  actions: {},
  getters: {},
});
```

## Setup Supabase

> Look at the [Supabase documentation](https://supabase.com/docs) to learn more.

> Look at the [@nuxtjs/supabase module documentation](https://supabase.nuxtjs.org/get-started) to learn more.

Install the dependencies:

```bash
# yarn
yarn add --dev @nuxtjs/supabase

# npm
npm install @nuxtjs/supabase --save-dev
```

Include `@nuxtjs/supabase` to the `buildModules` array in `nuxt.config.ts` file:

```javascript
// nuxt.config.ts

import { defineNuxtConfig } from 'nuxt';

export default defineNuxtConfig({
  css: [
    // ...some code
  ],

  buildModules: ['@pinia/nuxt', '@nuxtjs/supabase'],

  build: {
    // ...some code
  },
});
```

create an `.env` file with your **_SUPABASE_URL_** and your **_SUPABASE_KEY_**:

```plaintext
SUPABASE_URL = 'https://example.supabase.com';
SUPABASE_KEY = '<your_key>';
```

## Development Server

Start the development server on http://localhost:3000

```bash
# yarn (Recommended)
yarn dev

# npm
npm run dev
```

## Production

Build the application for production:

```bash
npm run build
```

Locally preview production build:

```bash
npm run preview
```

Checkout the [deployment documentation](https://v3.nuxtjs.org/guide/deploy/presets) for more information.
