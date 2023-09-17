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

.ql-editor {
  height: 300px;
  /* Например, 300px */
}
</style>
<style>
.ql-editor {
  height: 200px;
  border-radius: 10px;
  /* Например, 300px */
}

.ql-editor {
  border: 2px solid #000;
  border-top: 0;
  border-top-left-radius: 0;
  border-top-right-radius: 0;
}

.ql-container.ql-snow {
  border: 0;
}

.ql-toolbar.ql-snow {
  border: 2px solid #000;
  border-radius: 10px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
</style>