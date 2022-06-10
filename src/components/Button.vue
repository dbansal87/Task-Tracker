<template>
  <button class="btn" @click="$emit('toggle-add-task')" :style="{background: color}">
      {{title}}
  </button>
</template>

<script>
export default {
    name: 'Button',
    props: ['title','color'],
    methods: {
    }
}
</script>

<style>

</style>