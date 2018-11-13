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
        <template slot="no-data">
          <v-btn flat color="primary" @click="buscarDados">
            <v-icon class="mr-2">autorenew</v-icon>
            Recarregar
          </v-btn>
        </template>
      </v-data-table>
      <div style="position: relative">
        <v-btn 
          absolute
          small
          dark
          fab
          top
          right
          @click="modal.cliente = !modal.cliente">
          <v-icon>add</v-icon>
        </v-btn>
      </div>
    </v-content>

    <ModalClienteCadastro :modal="modal.cliente" v-on:cliente="closeCliente" />
  </div>
</template>

<script>
import Cabecalho from '@/components/Cabecalho'
import ModalClienteCadastro from '@/components/ModalClienteCadastro'
export default {
  created () {
    this.buscarDados()
  },
  components: {
    Cabecalho,
    ModalClienteCadastro
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
      },
      modal: {
        cliente: false
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
    },
    closeCliente (val) {
      this.modal.cliente = val
    }
  }
}
</script>

<style>

</style>
