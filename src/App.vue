<script setup>
import { reactive } from 'vue';

  const estado = reactive({
    primeiroNumero: 0,
    segundoNumero: 0,
    resultado: 0,
    calculo: 'somar',
  })

  function atualizaPrimeiroNumero(e) {
    if (e.target.value != '') {
      estado.primeiroNumero = parseInt(e.target.value)
    } else {
      estado.primeiroNumero = 0
    }
  }

  function atualizaSegundoNumero(e) {
    if (e.target.value != '') {
      estado.segundoNumero = parseInt(e.target.value)
    } else {
      estado.segundoNumero = 0
    }
  }

  function atualizaCalculo(e) {
    estado.calculo = e.target.value;
    atualizaResultado();
  }

  function atualizaResultado() {
    let resposta = 0;
    const {calculo, primeiroNumero, segundoNumero} = estado;
    
    if (calculo == 'somar') {
      resposta = primeiroNumero + segundoNumero
    } else if (calculo == 'subtrair') {
      resposta = primeiroNumero - segundoNumero
    } else if (calculo == 'multiplicar') {
      resposta = primeiroNumero * segundoNumero
    } else {
      resposta = primeiroNumero / segundoNumero
    };

    if ((resposta % 1) > 0) {
      estado.resultado = parseFloat(resposta).toFixed(1);
    } else {
      estado.resultado = parseFloat(resposta)
    }
  }

</script>
<template>
  <div class="corpo">
    <div class="container">
      <h1>CALCULADORA ARITMÉTICA</h1>
      <div class="campos">
        <input @keyup="evento => atualizaPrimeiroNumero(evento)" @change="() => atualizaResultado()" id="n-1" type="number" placeholder="First num">
        <input @keyup="evento => atualizaSegundoNumero(evento)" @change="() => atualizaResultado()" id="n-2" type="number" placeholder="Second num">
      </div>
      <select @change=" evento => atualizaCalculo(evento)">
          <option value="somar">somar</option>
          <option value="subtrair">subtrair</option>
          <option value="multiplicar">multiplicar</option>
          <option value="dividir">dividir</option>
      </select>
      <div class="caixa-da-resposta">
        <span id="resultado">{{ estado.resultado }}</span>
      </div>
    </div>
  </div>
</template>
<style scoped>
  .corpo {
    background-image: linear-gradient(45deg, rgb(255, 0, 0), rgb(255, 0, 255));
    height: 100vh;
    width: 100vw;
    position: absolute;
    top: 0;
    left: 0;
    padding: 10px;
  }

  .container {
    padding: 10px;
    margin: 72px auto;
    max-width: 500px;
    width: 100%;
    max-height: 400px;
    height: auto;
    background-color: rgb(223, 223, 223);
    border-radius: 6px;
    text-align: center;
    font-family: sans-serif;
  }

  .campos {
    display: flex;
    justify-content: space-around;
    align-items: center;
    max-width: 450px;
    width: 100%;
    margin: 0 auto;
    flex-wrap: wrap;
  }



  h1 {
    text-align: center;
    margin-top: 24px ;
  }
  input {
    text-align: center;
    height: 40px;
    font-size: 24px;
    max-width: 150px;
    width: 100%;
  }
  select {
    display: flex;
    margin: 16px auto 0;
    height: 30px;
    font-size: 24px;
    text-align: center;
    max-width: 158px;
    width: 100%;
  }
  span {
    text-align: center;
    font-size: 32px;
    height: 40px;
    padding: 90p;
  }
  
  .caixa-da-resposta {
    width: 50%;
    padding: 16px;
    background-color: rgb(255, 255, 255);
    margin: 24px auto;
    border-radius: 6px;
    
  }

  @media screen and (max-width: 720px) {
    .container {
      max-width: 300px;
    }
    .campos {
      flex-direction: column;
    }
    input {
      margin-bottom: 8px;
    }
  }
</style>
