<template>
  <q-page class="q-pa-md row items-start q-col-gutter-md">
    <div class="col-xs-12 col-sm-6">
        <q-card>
          <q-card-section>
            <div class="text-h6">Scripts</div>
          </q-card-section>
          <q-card-section>
            <q-list bordered separator>
              <q-item @click="runScript('q31')" clickable v-ripple :disable="isRunning">
                <q-item-section>Carregar quadro 31</q-item-section>
              </q-item>
              <q-item @click="runScript('s31')" clickable v-ripple :disable="isRunning">
                <q-item-section>Sabotar quadro 31 (apaga o quadro)</q-item-section>
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
          <div>PID: {{result.pid}}</div>
          <div>Script: {{result.script}}</div>
          <div>Status: {{result.status}}</div>
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
    isRunning: false,
    result: 'Pronto'
  }),
  methods: {
    runScript (script) {
      this.isRunning = true
      this.$axios.post(this.apiURL + '/' + script).then((response) => {
        this.result = response.data
      }).catch(() => {
        this.result = { status: 'Erro' }
      }).finally(() => {
        this.isRunning = false
      })
    }
  }
}
</script>
