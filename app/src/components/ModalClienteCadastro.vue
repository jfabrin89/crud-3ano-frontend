<template>
  <div id="modalClienteCadastro">
    <v-dialog 
      v-model="modal"
      fullscreen
      hide-overlay
      transition="dialog-bottom-transition">
      <v-card>
        <v-toolbar dark>
          <v-btn icon dark @click.native="close(false)">
            <v-icon>close</v-icon>
          </v-btn>
          <v-toolbar-title>Cadastro de Cliente</v-toolbar-title>
        </v-toolbar>
        <v-layout row wrap justify-center>
          <v-flex xs8>
            <v-alert :type="mensagem.tipo" :value="true" v-if="mensagem.mostrar">
              {{mensagem.texto}}
            </v-alert>
            <v-form v-model="valid" ref="form" lazy-validation>
              <v-text-field v-model="cliente.id" label="ID" disabled />
              <v-text-field v-model="cliente.nome" label="Nome" />
              <v-text-field v-model="cliente.telefone" label="Telefone" />
              <v-text-field v-model="cliente.email" label="E-mail" />
              <v-select v-model="cliente.situacao" label="Situação" :items="cbb.situacao" />

              <v-btn flat color="primary" @click="salvar">
                <v-icon class="mr-2">save</v-icon>
                Salvar
              </v-btn>
            </v-form>
          </v-flex>
        </v-layout>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
export default {
  data () {
    return {
      cbb: {
        situacao: [
          {text: 'Ativo', value: 'A'},
          {text: 'Inativo', value: 'I'}
        ]
      },
      cliente: {
        id: '',
        nome: '',
        telefone: '',
        email: '',
        situacao: 'A'
      },
      mensagem: {
        tipo: '',
        mostrar: false,
        texto: ''
      },
      valid: true
    }
  },
  methods: {
    close (val) {
      this.$emit('cliente', val)
    },
    salvar () {
    this
      .axios
      .post('clientes', this.cliente)
      .then((success) => {
        this.mensagem = {
          mostrar: true,
          texto: 'Salvo com sucesso',
          tipo: 'success'
        }
      })
      .catch((error) => {
        this.mensagem = {
          mostrar: true,
          texto: 'Erro ao salvar ' + error,
          tipo: 'error'
        }
      })
    }
  },
  props: [
    'modal'
  ]
}
</script>

<style>

</style>
