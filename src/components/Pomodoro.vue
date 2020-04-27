<template>
  <div id = "Pomodoro">
    <div class="titulo">
      <h1>PomodoroClock</h1>
    </div>

    <div class="cronometro">
      <h1>Minutos.segundos</h1>
    </div>

    <div class="ajusteTempo" v-if="!start">
      <button class="padraoBotao">-</button> <h3>tempo</h3> <button class="padraoBotao">+</button>
    </div>

    <div class="comandos">
      <div v-if="!start">
        <button class="padraoBotao botaoComando">Start</button>
      </div>

      <div v-else>
        <button class="padraoBotao botaoComando">Pausar</button>
        <button class="padraoBotao botaoComando">Continuar</button>
        <button class="padraoBotao botaoComando">Zerar</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Pomodoro',
  data() {
    return {
      start: false
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#Pomodoro{
  padding-top: 80px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.titulo{
  color: aliceblue;
  margin-bottom: 30px;
}

.cronometro{
  display: flex;
  align-items: center;
  height: 250px;
  width: 250px;
  border-radius: 50%;
  background-color: aliceblue;
  box-shadow: red 0px 0px 20px;
}

.cronometro h1{
  font-size: 20px;
  margin-left: 22px;
}

.ajusteTempo{
  margin-top: 30px;
  display: flex;
  color: aliceblue;
}

.padraoBotao{
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
</style>
