# Nuxt Base Layer

A production-ready Nuxt 4 base layer with custom theming, Nuxt UI components, and automatic form generation capabilities.

## Features

This base layer provides:

- **Custom Theme System** - 7 semantic color families with 11 shades each, full dark mode support
- **Nuxt UI Integration** - Pre-configured with 50+ auto-imported components
- **Nuxt Auto Forms** - Automatic form generation from Zod schemas
- **Error Handling** - Beautiful, user-friendly error pages
- **Theme Showcase** - Live demo page at `/theme` displaying all components
- **TypeScript First** - Full type safety throughout
- **Tailwind CSS v4** - Modern utility-first CSS with custom properties

## Quick Start

### Installation

```bash
# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build
```

Visit `http://localhost:3000/theme` to see the complete theme showcase.

## What's Included

### Project Structure

```
nuxt-baselayer/
├── app/
│   ├── assets/css/
│   │   ├── main.css          # Tailwind imports & custom styles
│   │   └── basetheme.css     # Theme color definitions
│   ├── components/           # Your custom components go here
│   ├── composables/          # Your composables go here
│   ├── layouts/              # Your layouts go here
│   ├── middleware/           # Your middleware go here
│   ├── pages/
│   │   └── theme.vue        # Theme showcase page
│   ├── app.config.ts        # App configuration
│   ├── app.vue              # Root component
│   └── error.vue            # Custom error page
├── public/                  # Static assets
├── nuxt.config.ts          # Nuxt configuration
└── package.json
```

### Pre-configured Components

All [Nuxt UI components](https://ui.nuxt.com) are auto-imported and ready to use:

- **Layout**: UApp, UContainer, UCard
- **Forms**: UInput, UTextarea, UCheckbox, URadioGroup, USwitch
- **Feedback**: UAlert, UProgress, USkeleton, Toast notifications
- **Navigation**: UAccordion, UButton
- **Data Display**: UBadge, UAvatar, UIcon
- **Actions**: UColorModeButton

Icons use the Phosphor icon pack with the `i-ph-*` prefix.

## Creating Your Own Theme

### Color System Overview

The theme uses 7 semantic color families, each with 11 shades (50-950):

- **primary** - Brand color (default: ocean blue `#338CB4`)
- **secondary** - Complementary color (default: deeper blue `#256d8d`)
- **neutral** - Grays for text and backgrounds
- **info** - Informational states (default: cyan-blue `#3bafda`)
- **success** - Success states (default: emerald `#3ba776`)
- **warning** - Warning states (default: amber `#e9b949`)
- **error** - Error states (default: red `#d64550`)

### Customizing Colors

#### Step 1: Update Color Variables

Edit [app/assets/css/basetheme.css](app/assets/css/basetheme.css) to change your theme colors:

```css
@theme static {
  /* PRIMARY - Change the base color (500) first */
  --color-primary-500: #338cb4; /* Your brand color */

  /* Then adjust the other shades */
  --color-primary-50: #f1f9fc;   /* Lightest */
  --color-primary-100: #d9eef7;
  /* ... */
  --color-primary-900: #143948;
  --color-primary-950: #0f2a36;  /* Darkest */
}
```

**Tips for creating color scales:**
- Start with your brand color as the `500` shade
- Shade `50` is the lightest (nearly white with a hint of color)
- Shade `950` is the darkest (nearly black with a hint of color)
- Use tools like [UI Colors](https://uicolors.app) or [Tailwind Color Generator](https://tailwind.simeongriggs.dev/) to generate complete scales

#### Step 2: Update Dark Mode Colors

In the same file, update the `.dark` section for dark mode variants:

```css
.dark {
  /* Dark mode typically inverts the scale logic */
  --color-primary-50: #0f2a36;   /* Darkest in dark mode */
  --color-primary-500: #338cb4;  /* Keep base similar */
  --color-primary-950: #f1f9fc;  /* Lightest in dark mode */
}
```

#### Step 3: Test Your Theme

Visit `/theme` to see all components styled with your custom colors. The showcase displays:

- All color variants
- Button states (solid, outline, ghost)
- Form elements
- Alerts and notifications
- Cards and layouts
- Dark mode variants

### Advanced Theme Customization

#### Changing Base Color Names

If you want to use different semantic names (e.g., "accent" instead of "secondary"):

1. Update color definitions in [basetheme.css](app/assets/css/basetheme.css):
```css
--color-accent-50: #...;
/* ... all shades ... */
```

2. Update [nuxt.config.ts](nuxt.config.ts):
```typescript
ui: {
  theme: {
    colors: ['primary', 'accent', 'neutral', 'info', 'success', 'warning', 'error'],
  },
}
```

3. Update [app.config.ts](app/app.config.ts):
```typescript
export default defineAppConfig({
  ui: {
    colors: {
      primary: 'primary',
      accent: 'accent',
      // ... other mappings
    }
  }
})
```

## Using Nuxt UI

### Auto-Import

All Nuxt UI components are automatically imported. No import statements needed:

```vue
<template>
  <UCard>
    <template #header>
      <h3>Card Title</h3>
    </template>

    <p>Card content goes here</p>

    <template #footer>
      <UButton color="primary">Action</UButton>
    </template>
  </UCard>
</template>

<script setup>
// No imports needed!
</script>
```

### Color Props

Use your theme colors directly in component props:

```vue
<UButton color="primary">Primary Button</UButton>
<UButton color="secondary">Secondary Button</UButton>
<UAlert color="success">Success message</UAlert>
<UBadge color="warning">Warning</UBadge>
```

### Dark Mode

Toggle dark mode using the `UColorModeButton` component:

```vue
<UColorModeButton />
```

Or programmatically with the `useColorMode` composable:

```vue
<script setup>
const colorMode = useColorMode()

const toggleDark = () => {
  colorMode.preference = colorMode.value === 'dark' ? 'light' : 'dark'
}
</script>
```

### Toast Notifications

Display toast notifications:

```vue
<script setup>
const toast = useToast()

const showSuccess = () => {
  toast.add({
    title: 'Success!',
    description: 'Your action completed successfully',
    color: 'success',
    icon: 'i-ph-check-circle'
  })
}
</script>
```

## Using Nuxt Auto Forms

Nuxt Auto Forms generates forms automatically from Zod schemas.

### Basic Example

```vue
<template>
  <UAutoForm :schema="userSchema" @submit="onSubmit" />
</template>

<script setup lang="ts">
import { z } from 'zod'

const userSchema = z.object({
  name: z.string().min(2, 'Name must be at least 2 characters'),
  email: z.string().email('Invalid email address'),
  age: z.number().min(18, 'Must be at least 18 years old'),
  role: z.enum(['admin', 'user', 'guest']),
  newsletter: z.boolean().default(false)
})

const onSubmit = (data: z.infer<typeof userSchema>) => {
  console.log('Form data:', data)
}
</script>
```

### With Validation

```vue
<template>
  <UAutoForm
    :schema="loginSchema"
    @submit="handleLogin"
    :submit-button="{ label: 'Sign In', color: 'primary' }"
  />
</template>

<script setup lang="ts">
import { z } from 'zod'

const loginSchema = z.object({
  email: z.string().email('Please enter a valid email'),
  password: z.string().min(8, 'Password must be at least 8 characters')
})

const handleLogin = async (data: z.infer<typeof loginSchema>) => {
  const toast = useToast()

  try {
    // Your login logic here
    await $fetch('/api/auth/login', {
      method: 'POST',
      body: data
    })

    toast.add({
      title: 'Login successful',
      color: 'success'
    })
  } catch (error) {
    toast.add({
      title: 'Login failed',
      description: 'Please check your credentials',
      color: 'error'
    })
  }
}
</script>
```

For more details, see the [Nuxt Auto Forms documentation](https://github.com/norbiros/nuxt-auto-form).

## Using as a Layer

You can use this as a Nuxt layer in other projects to inherit all theme colors, components, and configurations.

### Option 1: Extend from GitHub Repository

The easiest way is to extend directly from a GitHub repository:

```typescript
// nuxt.config.ts
export default defineNuxtConfig({
  extends: [
    'github:yourusername/nuxt-baselayer'
  ]
})
```

**Using a specific branch or tag:**

```typescript
export default defineNuxtConfig({
  extends: [
    'github:yourusername/nuxt-baselayer#main',        // specific branch
    'github:yourusername/nuxt-baselayer#v1.0.0',      // specific tag
    'github:yourusername/nuxt-baselayer#a1b2c3d',     // specific commit
  ]
})
```

**Using other Git providers:**

```typescript
export default defineNuxtConfig({
  extends: [
    'gitlab:yourusername/nuxt-baselayer',             // GitLab
    'bitbucket:yourusername/nuxt-baselayer',          // Bitbucket
    'https://github.com/yourusername/nuxt-baselayer', // Full URL
  ]
})
```

### Option 2: Extend from Local Path

If you have the layer locally (git submodule, monorepo, etc.):

```typescript
export default defineNuxtConfig({
  extends: [
    './layers/nuxt-baselayer',    // relative path
    '../nuxt-baselayer',          // parent directory
  ]
})
```

### Required Dependencies

When using this layer, you must install the following peer dependencies in your consuming project:

```json
{
  "dependencies": {
    "nuxt": "^4.2.0",
    "@nuxt/ui": "^4.1.0",
    "@norbiros/nuxt-auto-form": "^0.5.0",
    "vue": "^3.5.22",
    "vue-router": "^4.6.3",
    "zod": "^4.1.12"
  }
}
```

Install them with:

```bash
npm install nuxt@^4.2.0 @nuxt/ui@^4.1.0 @norbiros/nuxt-auto-form@^0.5.0 vue@^3.5.22 vue-router@^4.6.3 zod@^4.1.12
```

**Note:** These dependencies are not automatically installed when you extend from this layer. Your project must have them installed for the layer to function correctly.

### What You Inherit

Your project automatically inherits:
- All theme colors and styles
- Nuxt UI configuration
- Auto Forms setup
- Error page template
- TypeScript configuration
- Custom CSS and Tailwind setup

### Overriding Layer Defaults

You can override anything from the layer in your project:

**Override colors:**
Create your own `app/assets/css/basetheme.css` with different color values

**Override app config:**
```typescript
// app/app.config.ts
export default defineAppConfig({
  ui: {
    colors: {
      primary: 'blue',  // Override to use Tailwind's blue instead
    }
  }
})
```

**Add your own components:**
Place components in `app/components/` - they'll be auto-imported alongside layer components

**Extend Nuxt config:**
```typescript
// nuxt.config.ts
export default defineNuxtConfig({
  extends: ['github:yourusername/nuxt-baselayer'],

  // Add your own modules
  modules: ['@nuxtjs/supabase'],

  // Override UI theme colors
  ui: {
    theme: {
      colors: ['primary', 'blue', 'red']  // Use different colors
    }
  }
})
```

## Customization Examples

### Adding Custom Components

Create components in `app/components/`:

```vue
<!-- app/components/Hero.vue -->
<template>
  <UContainer>
    <div class="text-center py-20">
      <h1 class="text-4xl font-bold text-primary-600 dark:text-primary-400">
        {{ title }}
      </h1>
      <p class="mt-4 text-neutral-600 dark:text-neutral-400">
        {{ description }}
      </p>
      <UButton color="primary" size="lg" class="mt-8">
        Get Started
      </UButton>
    </div>
  </UContainer>
</template>

<script setup lang="ts">
defineProps<{
  title: string
  description: string
}>()
</script>
```

Use it anywhere (auto-imported):

```vue
<template>
  <Hero
    title="Welcome to My App"
    description="Build amazing things with Nuxt"
  />
</template>
```

### Adding Layouts

Create layouts in `app/layouts/`:

```vue
<!-- app/layouts/default.vue -->
<template>
  <UApp>
    <header class="border-b border-neutral-200 dark:border-neutral-800">
      <UContainer class="py-4">
        <nav class="flex items-center justify-between">
          <div class="font-bold text-xl">My App</div>
          <UColorModeButton />
        </nav>
      </UContainer>
    </header>

    <main>
      <slot />
    </main>

    <footer class="border-t border-neutral-200 dark:border-neutral-800 mt-20">
      <UContainer class="py-8 text-center text-neutral-600 dark:text-neutral-400">
        &copy; 2025 My App
      </footer>
    </footer>
  </UApp>
</template>
```

Use in pages:

```vue
<template>
  <div>
    <h1>Page Content</h1>
  </div>
</template>

<script setup>
definePageMeta({
  layout: 'default'
})
</script>
```

## Tech Stack

- **[Nuxt 4](https://nuxt.com/)** - Vue.js framework
- **[Nuxt UI](https://ui.nuxt.com/)** - Beautiful, accessible components
- **[Nuxt Auto Forms](https://github.com/norbiros/nuxt-auto-form)** - Schema-driven forms
- **[Tailwind CSS v4](https://tailwindcss.com/)** - Utility-first CSS
- **[Zod](https://zod.dev/)** - TypeScript-first schema validation
- **[Phosphor Icons](https://phosphoricons.com/)** - Flexible icon family

## Additional Resources

- [Nuxt Documentation](https://nuxt.com/docs)
- [Nuxt UI Components](https://ui.nuxt.com/components)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)
- [Zod Documentation](https://zod.dev)

## License

MIT
