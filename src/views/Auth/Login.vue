<template>
  <LoginComponent></LoginComponent>
</template>

<script>
import LoginComponent from "@/components/Auth/LoginComponent.vue";

  import { defineComponent } from 'vue'
  export default defineComponent ({

    name: "Login",
    components: {
    LoginComponent
  },
  })
</script>

<style lang="scss" scoped>
</style>