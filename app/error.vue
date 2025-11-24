<template>
  <div class="min-h-screen flex items-center justify-center p-6">
    <UCard class="max-w-2xl w-full">
      <template #header>
        <div class="flex items-center gap-3">
          <UIcon :name="errorIcon" :class="iconColor" class="w-8 h-8" />
          <div>
            <h1 class="text-2xl font-bold">
              {{ error?.statusCode || 'Error' }}
            </h1>
            <p class="text-sm opacity-70">
              {{ error?.statusMessage || 'An error occurred' }}
            </p>
          </div>
        </div>
      </template>

      <div class="space-y-4">
        <p>{{ displayMessage }}</p>

        <div class="flex gap-3 mt-6">
          <UButton @click="handleError" color="primary"> Go to Homepage </UButton>
          <UButton @click="reload" color="neutral" variant="soft"> Try Again </UButton>
        </div>
      </div>
    </UCard>
  </div>
</template>

<script setup lang="ts">
import type { NuxtError } from '#app'

const props = defineProps({
  error: Object as () => NuxtError,
})

const errorIcon = computed(() => {
  const code = props.error?.statusCode
  if (code === 404) return 'i-heroicons-magnifying-glass-circle-20-solid'
  if (code === 403) return 'i-heroicons-lock-closed-20-solid'
  if (code === 401) return 'i-heroicons-shield-exclamation-20-solid'
  return 'i-heroicons-exclamation-triangle-20-solid'
})

const iconColor = computed(() => {
  const code = props.error?.statusCode
  if (code === 404) return 'text-info-500'
  if (code === 403 || code === 401) return 'text-warning-500'
  return 'text-error-500'
})

// User-friendly error messages
const displayMessage = computed(() => {
  const code = props.error?.statusCode
  if (code === 404) return 'The page you are looking for could not be found.'
  if (code === 403) return 'You do not have permission to access this resource.'
  if (code === 401) return 'Please log in to access this resource.'
  if (code === 500) return 'An internal server error occurred. Our team has been notified.'
  return 'Something went wrong. Please try again later.'
})

const handleError = () => clearError({ redirect: '/' })

const reload = () => {
  clearError()
  window.location.reload()
}
</script>
