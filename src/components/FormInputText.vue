<script lang="ts">
import { defineProps } from "vue"
const props = defineProps({
  id: String, 
  label: {
    type: String, 
    required: false, 
    default: ""
  },
  required: {
    type: String, 
    required: false, 
    default: false, 
  },
  placeholder: {
    type: String, 
    required: false, 
    default: ""
  }
})
</script>
<template>
  <div class="d-flex flex-col gap-2">
    <label v-if="props.label" :for="props.label" class="block mb-2 text-sm font-medium text-green-700 dark:text-green-500">{{ props.label }}</label>
    <input type="text" id="success" class="bg-green-50 border border-green-500 text-green-900 dark:text-green-400 placeholder-green-700 dark:placeholder-green-500 text-sm rounded-lg focus:ring-green-500 focus:border-green-500 block w-full p-2.5 dark:bg-gray-700 dark:border-green-500" :required="props.required" :placeholder="props.placeholder"/>
  </div>
</template>
