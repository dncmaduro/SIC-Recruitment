<template>
  <div class="flex flex-col gap-1 mt-9">
    <label class="font-medium"
      >{{ question
      }}<span class="text-red-500 ml-0.5">{{ required && '*' }}</span></label
    >
    <NuxtImg v-if="image" :src="image" class="mx-auto my-8 w-[480px]" />
    <UInput
      v-if="inputType === 'text' || inputType === 'date'"
      v-model="modelValue"
      :type="inputType"
      size="lg"
      class="w-full"
      :placeholder="placeholder"
      color="white"
      :ui="{
        rounded: 'rounded-lg',
        placeholder: 'italic',
        color: {
          white: {
            outline:
              'shadow-sm bg-white text-gray-900 ring-primary ring-2 ring-inset ring-gray-300 focus:ring-2 focus:ring-red-400'
          }
        }
      }"
    />
    <UTextarea
      v-else-if="inputType === 'textarea'"
      class="w-full"
      :placeholder="placeholder"
      color="white"
      :ui="{
        rounded: 'rounded-lg',
        placeholder: 'italic',
        color: {
          white: {
            outline:
              'shadow-sm bg-white text-gray-900 ring-primary ring-2 ring-inset ring-gray-300 focus:ring-2 focus:ring-red-400'
          }
        }
      }"
    />
    <div v-else class="flex gap-2">
      <UCheckbox
        v-for="option in genderOptions"
        :key="option.label"
        :label="option.label"
        color="red"
      />
    </div>
  </div>
</template>

<script setup lang="ts">
import type { ApplyBttQuestion } from '~/types/apply/question'

const props = defineProps<ApplyBttQuestion>()

const widthClass = computed(() => {
  if (props.basis === '1') {
    return 'w-full'
  }

  return `w-${props.basis}`
})

const genderOptions = ref([
  {
    value: 'Nam',
    label: 'Nam'
  },
  {
    value: 'Nữ',
    label: 'Nữ'
  }
])

const modelValue = ref<any>()
</script>
