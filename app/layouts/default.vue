<template>
  <div class="min-h-screen flex flex-col">
    <header class="border-b border-neutral-200 dark:border-neutral-800">
      <UContainer class="py-4">
        <nav class="flex items-center justify-between">
          <NuxtLink to="/" class="font-bold text-xl text-primary-600 dark:text-primary-400 hover:text-primary-700 dark:hover:text-primary-300">
            My App
          </NuxtLink>
          <div class="flex items-center gap-4">
            <UColorModeButton />
          </div>
        </nav>
      </UContainer>
    </header>

    <main class="flex-1">
      <slot />
    </main>

    <footer class="border-t border-neutral-200 dark:border-neutral-800 mt-auto">
      <UContainer class="py-8 text-center text-neutral-600 dark:text-neutral-400">
        <p>&copy; {{ currentYear }} My App. All rights reserved.</p>
      </UContainer>
    </footer>
  </div>
</template>

<script setup lang="ts">
const currentYear = new Date().getFullYear()
</script>
