<template>
  <q-page class="q-pa-md row items-start q-col-gutter-md">
    <div class="col-xs-12">
        <q-card>
          <q-card-section>
            <div class="text-h6">Conteúdo da tabela</div>
          </q-card-section>
          <q-card-section>
            <q-table
              title="Tabela"
              :data="runs"
              :columns="columns"
              row-key="name"
            />
          </q-card-section>
        </q-card>
    </div>
  </q-page>
</template>

<style>
</style>

<script>
export default {
  name: 'Logs',
  data: () => ({
    apiURL: 'http://localhost:3000',
    runs: [],
    columns: [
      { name: 'fieldID', label: 'Cód. componente', field: 'fieldID', sortable: true },
      { name: 'fieldName', align: 'left', label: 'Título Componente', field: 'fieldName', sortable: true }
    ]
  }),
  created () {
    this.$axios.get(this.apiURL + '/q31').then((response) => {
      this.runs = response.data
    }).catch(() => {
      console.error('Erro na conexão')
    })
  }
}
</script>
