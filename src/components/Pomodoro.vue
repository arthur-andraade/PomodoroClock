<template>
  <div id = "Pomodoro" class="animated fadeInLeft">
    <div class="titulo">
      <h1>Pomodoro<span>Clock</span></h1>
    </div>

    <div class="cronometro" :class="{botaoSelecionado: start, cronometroFundo: start}">
      <h1>{{minutos}}.{{segundos}}</h1>
      <h3 v-if="start">{{tempoSelecionado}} min</h3>
    </div>

    <div class="ajusteTempo" v-if="!start">
      <button class="padraoBotao" @click="decrementar">-</button> <h3>{{tempoSelecionado}}</h3> <button class="padraoBotao" @click="tempoSelecionado++">+</button>
    </div>

    <div class="comandos">
      <div v-if="!start">
        <button class="padraoBotao botaoComando" @click="botaoStart">Start</button>
      </div>

      <div v-else>
        <button class="padraoBotao botaoComando" :class="{botaoSelecionado: pressionaPausar}" @click="pressionarPausarEContinuar"  >Pausar</button>
        <button class="padraoBotao botaoComando"  :class="{botaoSelecionado: pressionaContinuar}"   @click="pressionarPausarEContinuar">Continuar</button>
        <button class="padraoBotao botaoComando" @click="zerar">Zerar</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Pomodoro',
  data() {
    return {
      timer: null,
      start: false,
      tempoSelecionado: 0,
      minutos: 0,
      segundos: 0,
      pressionaPausar: false,
      pressionaContinuar: false
    }
  },

  methods: {
    
    decrementar: function (){
      if( this.tempoSelecionado > 0 && this.tempoSelecionado != 0){
        this.tempoSelecionado--;
      }
    },

    botaoStart: function(){
      if(this.tempoSelecionado != 0){
          this.start = true;
          this.minutos = this.tempoSelecionado - 1;
          this.segundos = 60;
          this.startTempo();
      }
    },

    zerar: function(){
      this.tempoSelecionado = 0;
      this.minutos = 0;
      this.segundos = 0;
      this.pararTempo()
      this.start = false;
      this.pressionaPausar = false;
      this.pressionaContinuar = false;
    },

    startTempo: function(){
      this.timer = setInterval(()=> this.decrementaTempo(), 1000);
    },

    decrementaTempo: function(){
      if(this.segundos == 0){
        this.minutos--;
        this.segundos = 60;
      }else{
        this.segundos--;
      }
    },
    
    pararTempo: function(){
      clearInterval(this.timer);
      this.timer = null
    },

    pressionarPausarEContinuar: function(){
      if(this.pressionaPausar){
        this.pressionaPausar = false;
        this.pressionaContinuar = true
        this.startTempo()
      }else{
        this.pressionaPausar = true;
        this.pressionaContinuar = false;
        this.pararTempo()
      }
    },
  }
}
</script>

<style scoped>
#Pomodoro{
  display: flex;
  flex-direction: column;
  align-items: center;
}

.titulo{
  font-family: 'Noto Sans TC', sans-serif;
  color: aliceblue;
  margin-bottom: 20px;
  font-size: 20px;
}
.titulo span {
  font-size: 50px;
  text-shadow: red 2px 2px 5px;
}
.cronometro{
  height: 250px;
  width: 250px;
  border-radius: 50%;
  background-color: aliceblue;
  box-shadow: red 0px 0px 20px;
  margin-bottom: 20px;
}

.cronometro h1{
  letter-spacing: 5px;
  margin-top: 90px;
  font-size: 40px;
  margin-left: 80px;
}

.cronometro h3{
  margin-top: 10px;
  font-size: 40px;
  margin-left: 85px;
  font-size: 20px;
}

.ajusteTempo{
  margin-top: 30px;
  display: flex;
  color: aliceblue;
}

.padraoBotao{
  font-family: 'Noto Sans TC', sans-serif;
  border-radius: 50%;
  height: 40px;
  width: 40px;
  background-color: red;
  border: aliceblue solid 2px;
  color: aliceblue;
  font-size: 20px;
}
.ajusteTempo h3{
  margin-right: 10px;
  margin-left: 10px;
  margin-top: 10px;
}

.comando{
  margin-top: 40px;
  display: flex;
  align-items: center;
}

.botaoComando{
  margin-top: 20px;
  width: 120px;
  border-radius: 10px;
  margin-left: 10px;
  margin-right: 10px;
}

.botaoComando:hover{
  background-color:#18d500;
}

.botaoSelecionado{
  background-color:#18d500;
  transition: 2s;
  box-shadow: 0px 0px 20px #38b42f,0px 0px 40px #38b42f,0px 0px 80px #38b42f;
}

.cronometroFundo{
  background-color: white;
}

</style>
