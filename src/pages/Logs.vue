<template>
  <q-page class="q-pa-md row items-start q-col-gutter-md">
    <div class="col-xs-12">
        <q-card>
          <q-card-section>
            <div class="text-h6">Últimas execuções</div>
          </q-card-section>
          <q-card-section>
            <q-table
              title="Execuções"
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
    apiURL: process.env.API,
    runs: [],
    columns: [
      { name: 'pid', label: 'PID', field: 'pid', sortable: true },
      { name: 'script', label: 'Script', field: 'script', sortable: true },
      { name: 'started', label: 'Início', field: row => new Date(row.started).toLocaleString() },
      { name: 'finished', label: 'Término', field: row => row.finished ? new Date(row.finished).toLocaleString() : '-' },
      { name: 'timeelapsed', label: 'Duração (s)', field: row => { return row.finished ? Math.abs(new Date(row.finished) - new Date(row.started)) / 1000 : '-' } }
    ]
  }),
  created () {
    this.$axios.get(this.apiURL + '/logs').then((response) => {
      this.runs = response.data
    }).catch(() => {
      console.error('Erro na conexão')
    })
  }
}
</script>
