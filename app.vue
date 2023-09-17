<template>
  <div class="fullpage">
    <TheHeader />

    <NuxtPage />

    <TheFooter />
  </div>
</template>
<style lang="scss">
.fullpage {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 100vh;
}
</style>
