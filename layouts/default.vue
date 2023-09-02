<template>
    <div class="container pt-16 font-mono">
      <div class="app-content text-center">
        <TheNav />
        <Nuxt />
        <div class="footer"></div>
      </div>
  </div>
</template>

<script>
import TheNav from '@/components/TheNav'

export default {
  components: { TheNav }
}
</script>

<style>
.container {
  margin-left:auto;
  margin-right:auto;}
.app-content {
  background: #ededed;
  border-radius: 5px;
  box-shadow: 0 0 30px -5px #2c3e50;

  min-height: 300px;
}
.footer {
  height: 25px;
}
</style>
