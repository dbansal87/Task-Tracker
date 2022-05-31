<template>
  <button class="btn" @click="addTask" :style="{background: color}">
      {{title}}
  </button>
</template>

<script>
export default {
    name: 'Button',
    props: ['title','color'],
    methods: {
        addTask() {
            console.log("Clicked");
        }
    }
}
</script>

<style>

</style>