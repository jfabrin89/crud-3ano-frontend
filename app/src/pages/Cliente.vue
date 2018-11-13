<template>
  <div id="cliente">
    <Cabecalho />
    <v-content class="ma-3">
      <h1>Cliente</h1>
      <hr />
      <v-layout wrap>
        <v-flex xs12>
          <v-text-field v-model="filtro" label="Filtro" />
        </v-flex>
      </v-layout>
      <v-data-table :headers="tblCliente.cabecalho" 
        :items="tblCliente.item" hide-actions
        class="elevation-1"
        :search="filtro">
        <template slot="items" slot-scope="props">
          <td>{{ props.item.id }}</td>
          <td>{{ props.item.nome }}</td>
          <td>{{ props.item.telefone }}</td>
          <td>{{ props.item.email }}</td>
          <td>{{ props.item.situacao | situacao }}</td>
        </template>
      </v-data-table>
    </v-content>
  </div>
</template>

<script>
import Cabecalho from '@/components/Cabecalho'
export default {
  created () {
    this.buscarDados()
  },
  components: {
    Cabecalho
  },
  data () {
    return {
      filtro: '',
      tblCliente: {
        cabecalho: [
          {text: '#', value: 'id'},
          {text: 'Nome', value: 'nome'},
          {text: 'Telefone', value: 'telefone'},
          {text: 'E-mail', value: 'email'},
          {text: 'Situação', value: 'situacao'}
        ],
        item: []
      }
    }
  },
  filters: {
    situacao: function (val) {
      if (!val) return
      if (val === 'A') return 'Ativo'
      else return 'Inativo'
    }
  },
  methods: {
    buscarDados () {
      this
        .axios
        .get('clientes')
        .then((success) => {
          this.tblCliente.item = success.data
        })
    }
  }
}
</script>

<style>

</style>
