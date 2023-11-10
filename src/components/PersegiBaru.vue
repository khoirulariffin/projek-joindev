<template>
  <div :class="`h-10 w-10 border border-black ${props.latarBelakang}`" @click="handleClick" />
</template>

<script setup>
const props = defineProps({
  latarBelakang: {
    type: String,
    default: 'bg-red-500'
  }
})

const emit = defineEmits(['onClick'])

const handleClick = () => {
  emit('onClick')
}
</script>
