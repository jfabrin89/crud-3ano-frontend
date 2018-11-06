<template>
  <div id="menu">
    <v-navigation-drawer fixed app v-model="gaveta" :clipped="$vuetify.breakpoint.mdAndUp" class="mt-4">
      <h1>Teste</h1>
    </v-navigation-drawer>
  </div>
</template>

<script>
export default {
  data () {
    return {
    }
  },
  props: [
    'gaveta'
  ]
}
</script>

<style scoped>
</style