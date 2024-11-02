<template>
  <ScrollArea class="h-full">
    <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
      <div v-for="(grupo, index) in grupos" :key="index" class="bg-white p-6 rounded-lg shadow">
        <h2 class="text-lg font-semibold mb-4 text-center border-b border-gray-300 pb-2">{{ grupo.nome }}</h2>
        <ul class="space-y-2">
          <li v-for="(presente, indexPresente) in grupo.presentes" :key="indexPresente" class="flex items-center">
            <span class="mr-2">•</span>
            <span>{{ presente.nome }}</span>
          </li>
        </ul>
      </div>
    </div>
  </ScrollArea>
</template>

<script setup>
import { ScrollArea } from '@/components/ui/scroll-area'
import { defineProps } from 'vue'

defineProps({
  grupos: {
    type: Object,
    required: true,
    default: () => []
  }
})

</script>