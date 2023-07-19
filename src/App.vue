<script setup>

import Section from "@/components/Section.vue";

</script>

<template>
  
  <header class="header">
    <div class="container">
      <h1 class="title">
        Hi optimalcity!
      </h1>
    </div>
  </header>
  
  <main class="main">
    <Section/>
  </main>
  
  <footer></footer>
</template>

<style scoped lang="scss">
.header {
  padding-block: 16px;
}

.title {
  text-align: center;
  font-size: 32px;
  font-weight: 600;
}

.main {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100%;
}

</style>
