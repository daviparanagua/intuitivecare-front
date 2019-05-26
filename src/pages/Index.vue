<template>
  <q-page class="q-pa-md row items-start q-col-gutter-md">
    <div class="col-xs-12 col-sm-6">
        <q-card class="q-pa-md">
          <q-card-section>
            <div class="text-h6">Our Changing Planet</div>
          </q-card-section>

          <q-card-section>
            <q-list bordered separator>
              <q-item clickable v-ripple>
                <q-item-section>Single line item</q-item-section>
              </q-item>

              <q-item clickable v-ripple>
                <q-item-section>
                  <q-item-label>Item with caption</q-item-label>
                  <q-item-label caption>Caption</q-item-label>
                </q-item-section>
              </q-item>

              <q-item clickable v-ripple>
                <q-item-section>
                  <q-item-label overline>OVERLINE</q-item-label>
                  <q-item-label>Item with caption</q-item-label>
                </q-item-section>
              </q-item>
            </q-list>
          </q-card-section>
        </q-card>
    </div>
    <div class="col-xs-12 col-sm-6">
      <q-card>
        <q-card-section>
          <div class="text-h6">Status do Servidor</div>
        </q-card-section>
        <q-card-section>
          <q-list bordered separator>
            <q-item clickable v-ripple>
              <q-item-section>Status do servidor: {{status.server}}</q-item-section>
            </q-item>
            <q-item clickable v-ripple>
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
    apiURL: 'http://localhost:3000',
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
