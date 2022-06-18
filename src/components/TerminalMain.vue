<template>
  <main class="main d-flex flex-column border rounded m-5 mh-100 bg-light">
    <div
      class="
        first_panel
        d-flex
        flex-row
        p-2
        justify-content-around
        align-items-center
        mt-2
      "
    >
      <div class="indicators d-flex flex-row">
        <div @click.prevent="switchSystem(true)" class="rounded-circle bg-success p-3 mr-4 ">ON</div>
        <div @click.prevent="switchSystem(false)"  class="rounded-circle bg-danger p-3">Off</div>
      </div>
      <div class="system_status">
        <div class="border rounded p-2">Система работает</div>
      </div>
      <div class="temperature border rounded p-2">{{temp.toFixed(2)}}</div>
      <div class="indicator d-flex flex-row">
        <div 
        :class="system_active ? 'bg-success' : 'bg-danger' "
        class="rounded-circle  p-3 m-1">Ind</div>
      </div>
    </div>
    <div class="info d-flex flex-column justify-content-around h-50 mt-4 ">
      <div v-show="!criticalTemp" class="note border h-25 w-75 rounded p-2 align-self-center">Система работает стабильно</div>
      <div v-show="criticalTemp" class="note border h-25 w-75 rounded p-2 align-self-center">Warning! Превышение критической температуры</div>      
      
      <div class="note border h-25 w-75 rounded p-2 align-self-center">Устройство Номер 1234</div>
    </div>
  
  </main>
</template>

<script>
// import Chart from "./Chart.vue"
export default {
  name: 'TerminalMain',
  mounted(){
    this.modulationTemp()
  },
  data () {
    return {
      temp : 60,
      temp_critical : 100,
      system_active : false
    }
  },
  methods :{
    modulationTemp(){
      setInterval(()=>{this.temp = this.temp + 2*(Math.random() - 0.2)}, 500)
    },
    switchSystem(bool){
        this.system_active = bool
    },
    autoResetTemperature(){
       if(this.system_active && this.temp >= this.temp_critical){
        while(this.temp > 60) {
          this.temp = this.temp - 0.01
        }
       }
    }
  },
  computed :{
    criticalTemp(){
      this.autoResetTemperature()
      return this.temp >= this.temp_critical
    }
  },

  components : {
    
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
main {
  height: 380px;
}
</style>
