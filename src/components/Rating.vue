<template>
  <div>
      <span @click="$emit('update:modelValue', 1)"> * </span>
      <span @click="$emit('update:modelValue', 2)"> * </span>
      <span @click="$emit('update:modelValue', 3)"> * </span>
      <span @click="$emit('update:modelValue', 4)"> * </span>
      <span @click="$emit('update:modelValue', 5)"> * </span>

      <p> Rating is:  {{ modelValue }} </p>
  </div>
</template>

<script>
export default {

    props: {
        modelValue: Number
    },
    emits: ['update:modelValue']

}
</script>

<style>

</style>