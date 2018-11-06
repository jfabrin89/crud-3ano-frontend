<template>
  <div class="teste">
    <Cabecalho />
    {{hello}}
  </div>
</template>

<script>
import Cabecalho from '@/components/Cabecalho'
export default {
  components: {
    Cabecalho
  },
  data () {
    return {
      hello: 'Teste'
    }
  },
  name: 'teste'
}
</script>

<style scoped>
</style>
