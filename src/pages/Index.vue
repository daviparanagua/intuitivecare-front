<template>
  <q-page class="q-pa-md row items-start q-col-gutter-md">
    <div class="col-xs-12 col-sm-6">
        <q-card>
          <q-card-section>
            <div class="text-h6">Ações frequentes</div>
          </q-card-section>
          <q-card-section>
            <q-list bordered separator>
              <q-item to="/scripts" clickable v-ripple>
                <q-item-section>Executar scripts</q-item-section>
              </q-item>

              <q-item to="/logs" clickable v-ripple>
                <q-item-section>Visualizar logs</q-item-section>
              </q-item>
            </q-list>
          </q-card-section>
        </q-card>
    </div>
    <div class="col-xs-12 col-sm-6">
      <q-card>
        <q-card-section>
          <div class="text-h6">Status do servidor</div>
        </q-card-section>
        <q-card-section>
          <q-list bordered separator>
            <q-item v-ripple>
              <q-item-section>Status do servidor: {{status.server}}</q-item-section>
            </q-item>
            <q-item v-ripple>
              <q-item-section>Status do banco de dados: {{status.database}}</q-item-section>
            </q-item>
          </q-list>
        </q-card-section>
      </q-card>
    </div>
  </q-page>
</template>

<style>
</style>

<script>
export default {
  name: 'PageIndex',
  data: () => ({
    apiURL: process.env.API,
    status: {
      server: 'Desconhecido',
      database: 'Desconhecido'
    }
  }),
  created () {
    this.$axios.get(this.apiURL + '/status').then((response) => {
      this.status = response.data
    }).catch(() => {
      this.status = { server: 'Offline', database: 'Desconhecido' }
    })
  }
}
</script>
