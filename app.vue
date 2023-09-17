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
  height: 200px !important;
  border-radius: 10px !important;
  /* Например, 300px */
}

.ql-editor {
  border: 2px solid #000 !important;
  border-top: 0 !important;
  border-top-left-radius: 0 !important;
  border-top-right-radius: 0 !important;
}

.ql-container.ql-snow {
  border: 0 !important;
}

.ql-toolbar.ql-snow {
  border: 2px solid #000 !important;
  border-radius: 10px !important;
  border-bottom-right-radius: 0 !important;
  border-bottom-left-radius: 0 !important;
}
</style>