<script setup lang="ts" >
import { defineProps, HTMLAttributes } from "vue"
import { cn } from "../../utils";
import { useVModel } from "@vueuse/core";

interface FormInputText {
  id:string, 
  name?: string,
  disabled?: boolean,
  label?: string,
  required?: boolean, 
  placeholder?: string, 
  type?: "text" | "email" | "password" 
  class?: HTMLAttributes['class']
  value?: string | number
  modelValue?: string | number
}

const props = withDefaults(defineProps<FormInputText>(), {
  name: "", 
  disabled: false, 
  type: "text", 
  label: "", 
  required: false, 
  placeholder: "",
  class: "", 
  value: ""
})

const emits = defineEmits<{
  (e: 'update:modelValue', payload: string | number): void
}>()

const modelValue = useVModel(props, 'modelValue', emits, {
  passive: true,
  defaultValue: props.value,
})
</script>
<template>
  <div class="flex flex-col gap-3">
    <label v-if="label && label.length > 0" :for="id" class="text-sm font-medium leading-none peer-disabled:cursor-not-allowed peer-disabled:opacity-70">
      {{ label }}
    </label>
    <div :class="cn('grid grid-cols-6 gap-2 ')">
      <div :class="cn(props.type === 'password' ? 'col-span-5' : '')">
        <input
        v-model="modelValue"
          type="props.type"
          :id="id"
          autocomplete="off"
          :disabled="props.disabled"
          :required="props.required"
          :placeholder="props.placeholder"
          :class="cn('flex h-10 w-full rounded-md border border-input bg-background px-3 py-2 text-sm ring-offset-background file:border-0 file:bg-transparent file:text-sm file:font-medium placeholder:text-muted-foreground focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:cursor-not-allowed disabled:opacity-50', props.class)"
        />
      </div>
      <div v-if="props.type === 'password'">

      </div>
    </div>
  </div>
</template>