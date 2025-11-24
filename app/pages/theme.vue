<template>
  <div class="min-h-screen transition-colors">
    <!-- Header with Dark Mode Toggle -->
    <UContainer class="py-8">
      <div class="flex justify-between items-center mb-8">
        <div>
          <h1 class="text-4xl font-bold text-neutral-900 mb-2">
            Theme Showcase
          </h1>
          <p class="text-neutral-600">
            Exploring all Nuxt UI components with our custom theme
          </p>
        </div>
        <UColorModeButton size="lg" />
      </div>

      <!-- Color Palette Section -->
      <section class="mb-12">
        <h2 class="text-2xl font-semibold text-neutral-900 mb-6">
          Color Palette
        </h2>
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
          <UCard>
            <template #header>
              <h3 class="font-semibold">Primary Colors</h3>
            </template>
            <div class="flex gap-2 flex-wrap">
              <UBadge color="primary" variant="solid">Primary</UBadge>
              <UBadge color="primary" variant="soft">Primary Soft</UBadge>
              <UBadge color="primary" variant="outline">Primary Outline</UBadge>
            </div>
          </UCard>

          <UCard>
            <template #header>
              <h3 class="font-semibold">Secondary Colors</h3>
            </template>
            <div class="flex gap-2 flex-wrap">
              <UBadge color="secondary" variant="solid">Secondary</UBadge>
              <UBadge color="secondary" variant="soft">Secondary Soft</UBadge>
              <UBadge color="secondary" variant="outline">Secondary Outline</UBadge>
            </div>
          </UCard>

          <UCard>
            <template #header>
              <h3 class="font-semibold">Status Colors</h3>
            </template>
            <div class="flex gap-2 flex-wrap">
              <UBadge color="success">Success</UBadge>
              <UBadge color="warning">Warning</UBadge>
              <UBadge color="error">Error</UBadge>
              <UBadge color="info">Info</UBadge>
            </div>
          </UCard>
        </div>
      </section>

      <!-- Buttons Section -->
      <section class="mb-12">
        <h2 class="text-2xl font-semibold text-neutral-900 mb-6">
          Buttons
        </h2>
        <UCard>
          <div class="space-y-6">
            <!-- Solid Buttons -->
            <div>
              <h3 class="text-sm font-medium text-neutral-700 mb-3">
                Solid Variant
              </h3>
              <div class="flex flex-wrap gap-3">
                <UButton color="primary" variant="solid">Primary</UButton>
                <UButton color="secondary" variant="solid">Secondary</UButton>
                <UButton color="success" variant="solid">Success</UButton>
                <UButton color="warning" variant="solid">Warning</UButton>
                <UButton color="error" variant="solid">Error</UButton>
                <UButton color="neutral" variant="solid">Neutral</UButton>
              </div>
            </div>

            <!-- Outline Buttons -->
            <div>
              <h3 class="text-sm font-medium text-neutral-700 mb-3">
                Outline Variant
              </h3>
              <div class="flex flex-wrap gap-3">
                <UButton color="primary" variant="outline">Primary</UButton>
                <UButton color="secondary" variant="outline">Secondary</UButton>
                <UButton color="success" variant="outline">Success</UButton>
                <UButton color="error" variant="outline">Error</UButton>
              </div>
            </div>

            <!-- Ghost Buttons -->
            <div>
              <h3 class="text-sm font-medium text-neutral-700 mb-3">
                Ghost Variant
              </h3>
              <div class="flex flex-wrap gap-3">
                <UButton color="primary" variant="ghost">Primary</UButton>
                <UButton color="secondary" variant="ghost">Secondary</UButton>
                <UButton color="neutral" variant="ghost">Neutral</UButton>
              </div>
            </div>

            <!-- Sizes -->
            <div>
              <h3 class="text-sm font-medium text-neutral-700 mb-3">
                Sizes
              </h3>
              <div class="flex flex-wrap items-center gap-3">
                <UButton size="xs">Extra Small</UButton>
                <UButton size="sm">Small</UButton>
                <UButton size="md">Medium</UButton>
                <UButton size="lg">Large</UButton>
                <UButton size="xl">Extra Large</UButton>
              </div>
            </div>

            <!-- Loading & Disabled -->
            <div>
              <h3 class="text-sm font-medium text-neutral-700 mb-3">
                States
              </h3>
              <div class="flex flex-wrap gap-3">
                <UButton loading>Loading</UButton>
                <UButton disabled>Disabled</UButton>
                <UButton icon="i-ph-magnifying-glass">With Icon</UButton>
              </div>
            </div>
          </div>
        </UCard>
      </section>

      <!-- Form Elements Section -->
      <section class="mb-12">
        <h2 class="text-2xl font-semibold text-neutral-900 mb-6">
          Form Elements
        </h2>
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
          <UCard>
            <template #header>
              <h3 class="font-semibold">Input Fields</h3>
            </template>
            <div class="space-y-4">
              <UInput placeholder="Standard input" />
              <UInput placeholder="With icon" icon="i-ph-user" />
              <UInput placeholder="Disabled input" disabled />
              <UInput
                placeholder="With validation"
                color="error"
                :error="true"
              />
              <UTextarea placeholder="Multi-line textarea" />
            </div>
          </UCard>

          <UCard>
            <template #header>
              <h3 class="font-semibold">Selection Controls</h3>
            </template>
            <div class="space-y-4">
              <div>
                <label class="text-sm font-medium text-neutral-700 mb-2 block">
                  Checkboxes
                </label>
                <div class="space-y-2">
                  <UCheckbox label="Option 1" :model-value="true" />
                  <UCheckbox label="Option 2" :model-value="false" />
                  <UCheckbox label="Disabled" disabled />
                </div>
              </div>

              <div>
                <label class="text-sm font-medium text-neutral-700 mb-2 block">
                  Radio Buttons
                </label>
                <URadioGroup v-model="selectedRadio" :options="radioOptions" />
              </div>

              <div>
                <label class="text-sm font-medium text-neutral-700 mb-2 block">
                  Switch
                </label>
                <USwitch v-model="switchValue" />
              </div>
            </div>
          </UCard>
        </div>
      </section>

      <!-- Alerts & Notifications Section -->
      <section class="mb-12">
        <h2 class="text-2xl font-semibold text-neutral-900 mb-6">
          Alerts & Feedback
        </h2>
        <div class="space-y-4">
          <UAlert
            color="primary"
            variant="soft"
            title="Primary Alert"
            description="This is a primary alert message with additional context."
            icon="i-ph-info"
          />
          <UAlert
            color="success"
            variant="soft"
            title="Success!"
            description="Your action was completed successfully."
            icon="i-ph-check-circle"
          />
          <UAlert
            color="warning"
            variant="soft"
            title="Warning"
            description="Please review this information carefully."
            icon="i-ph-warning"
          />
          <UAlert
            color="error"
            variant="soft"
            title="Error"
            description="Something went wrong. Please try again."
            icon="i-ph-x-circle"
          />
        </div>
      </section>

      <!-- Cards & Content Section -->
      <section class="mb-12">
        <h2 class="text-2xl font-semibold text-neutral-900 mb-6">
          Cards & Content Display
        </h2>
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
          <UCard>
            <template #header>
              <div class="flex items-center gap-3">
                <UAvatar
                  src="https://api.dicebear.com/7.x/avataaars/svg?seed=Felix"
                  alt="User"
                  size="md"
                />
                <div>
                  <h3 class="font-semibold">Card with Avatar</h3>
                  <p class="text-sm text-neutral-600">Subtitle</p>
                </div>
              </div>
            </template>
            <p class="text-neutral-700">
              This is a card component with a header containing an avatar and title.
            </p>
            <template #footer>
              <div class="flex justify-between items-center">
                <UBadge color="primary">Featured</UBadge>
                <UButton size="sm" variant="ghost">Learn More</UButton>
              </div>
            </template>
          </UCard>

          <UCard>
            <template #header>
              <h3 class="font-semibold">Statistics Card</h3>
            </template>
            <div class="space-y-4">
              <div>
                <div class="text-3xl font-bold text-primary-600">
                  1,234
                </div>
                <p class="text-sm text-neutral-600">Total Users</p>
              </div>
              <UProgress :value="75" color="primary" />
            </div>
          </UCard>

          <UCard>
            <template #header>
              <h3 class="font-semibold">Status Card</h3>
            </template>
            <div class="space-y-3">
              <div class="flex items-center justify-between">
                <span class="text-sm text-neutral-700">Active</span>
                <UBadge color="success" variant="soft">Online</UBadge>
              </div>
              <div class="flex items-center justify-between">
                <span class="text-sm text-neutral-700">Pending</span>
                <UBadge color="warning" variant="soft">3</UBadge>
              </div>
              <div class="flex items-center justify-between">
                <span class="text-sm text-neutral-700">Errors</span>
                <UBadge color="error" variant="soft">0</UBadge>
              </div>
            </div>
          </UCard>
        </div>
      </section>

      <!-- Accordion Section -->
      <section class="mb-12">
        <h2 class="text-2xl font-semibold text-neutral-900 mb-6">
          Accordion
        </h2>
        <UAccordion :items="accordionItems" />
      </section>

      <!-- Badges & Icons Section -->
      <section class="mb-12">
        <h2 class="text-2xl font-semibold text-neutral-900 mb-6">
          Badges & Icons
        </h2>
        <UCard>
          <div class="space-y-6">
            <div>
              <h3 class="text-sm font-medium text-neutral-700 mb-3">
                Badge Variants
              </h3>
              <div class="flex flex-wrap gap-3">
                <UBadge variant="solid">Solid</UBadge>
                <UBadge variant="soft">Soft</UBadge>
                <UBadge variant="outline">Outline</UBadge>
                <UBadge variant="subtle">Subtle</UBadge>
              </div>
            </div>

            <div>
              <h3 class="text-sm font-medium text-neutral-700 mb-3">
                Icons (Phosphor Icons)
              </h3>
              <div class="flex flex-wrap gap-4 text-2xl">
                <UIcon name="i-ph-house" class="text-primary-600" />
                <UIcon name="i-ph-user" class="text-secondary-600" />
                <UIcon name="i-ph-gear" class="text-neutral-600" />
                <UIcon name="i-ph-heart" class="text-error-600" />
                <UIcon name="i-ph-star" class="text-warning-600" />
                <UIcon name="i-ph-check-circle" class="text-success-600" />
                <UIcon name="i-ph-bell" class="text-info-600" />
              </div>
            </div>
          </div>
        </UCard>
      </section>

      <!-- Progress & Loading Section -->
      <section class="mb-12">
        <h2 class="text-2xl font-semibold text-neutral-900 mb-6">
          Progress & Loading States
        </h2>
        <UCard>
          <div class="space-y-6">
            <div>
              <h3 class="text-sm font-medium text-neutral-700 mb-3">
                Progress Bars
              </h3>
              <div class="space-y-3">
                <UProgress :value="25" color="primary" />
                <UProgress :value="50" color="secondary" />
                <UProgress :value="75" color="success" />
                <UProgress :value="100" color="warning" />
              </div>
            </div>

            <div>
              <h3 class="text-sm font-medium text-neutral-700 mb-3">
                Skeleton Loading
              </h3>
              <div class="space-y-3">
                <USkeleton class="h-4 w-full" />
                <USkeleton class="h-4 w-3/4" />
                <USkeleton class="h-4 w-1/2" />
              </div>
            </div>
          </div>
        </UCard>
      </section>

      <!-- Interactive Demo Section -->
      <section class="mb-12">
        <h2 class="text-2xl font-semibold text-neutral-900 mb-6">
          Interactive Demo
        </h2>
        <UCard>
          <template #header>
            <h3 class="font-semibold">Toast Notifications</h3>
          </template>
          <div class="flex flex-wrap gap-3">
            <UButton @click="showToast('success')">Show Success Toast</UButton>
            <UButton @click="showToast('error')" color="error">Show Error Toast</UButton>
            <UButton @click="showToast('warning')" color="warning">Show Warning Toast</UButton>
            <UButton @click="showToast('info')" color="neutral">Show Info Toast</UButton>
          </div>
        </UCard>
      </section>

    </UContainer>
  </div>
</template>

<script setup lang="ts">
const toast = useToast()

const selectedRadio = ref('option1')
const radioOptions = [
  { value: 'option1', label: 'Option 1' },
  { value: 'option2', label: 'Option 2' },
  { value: 'option3', label: 'Option 3' }
]

const switchValue = ref(true)

const accordionItems = [
  {
    label: 'What is Nuxt UI?',
    content: 'Nuxt UI is an open-source UI library with 110+ customizable components built with Tailwind CSS and Reka UI.',
    defaultOpen: true
  },
  {
    label: 'How do I customize colors?',
    content: 'You can customize colors using CSS custom properties with the @theme directive in your CSS files.'
  },
  {
    label: 'Is it accessible?',
    content: 'Yes! All components are built with accessibility in mind, following WAI-ARIA guidelines.'
  }
]

const showToast = (type: string) => {
  const toastConfig: Record<string, any> = {
    success: {
      title: 'Success!',
      description: 'Your action completed successfully.',
      color: 'success',
      icon: 'i-ph-check-circle'
    },
    error: {
      title: 'Error',
      description: 'Something went wrong. Please try again.',
      color: 'error',
      icon: 'i-ph-x-circle'
    },
    warning: {
      title: 'Warning',
      description: 'Please review this information.',
      color: 'warning',
      icon: 'i-ph-warning'
    },
    info: {
      title: 'Information',
      description: 'Here is some useful information.',
      color: 'neutral',
      icon: 'i-ph-info'
    }
  }

  toast.add(toastConfig[type])
}
</script>
