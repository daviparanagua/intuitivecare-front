<template>
  <q-page class="q-pa-md row items-start q-col-gutter-md">
    <div class="col-xs-12 col-sm-6">
        <q-card>
          <q-card-section>
            <div class="text-h6">Ações frequentes</div>
          </q-card-section>
          <q-card-section>
            <q-list bordered separator>
              <q-item @click="runScript('q31')" clickable v-ripple :disable="isRunning">
                <q-item-section>Carregar quadro 31</q-item-section>
              </q-item>
            </q-list>
          </q-card-section>
        </q-card>
    </div>
    <div class="col-xs-12 col-sm-6">
      <q-card>
        <q-card-section>
          <div class="text-h6">Status</div>
        </q-card-section>
        <q-card-section v-if="isRunning">
          O script selecionado está em execução...
        </q-card-section>
        <q-card-section v-else>
          Status: {{status}}
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
    isRunning: false,
    status: 'Aguardando'
  }),
  methods: {
    runScript (script) {
      this.isRunning = true
      this.$axios.get(this.apiURL + '/' + script).then((response) => {
        this.status = response.data.status
      }).catch(() => {
        this.status = { server: 'Offline', database: 'Desconhecido' }
      }).finally(() => {
        this.isRunning = false
      })
    }
  }
}
</script>
