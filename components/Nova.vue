<!-- Use preprocessors via the lang attribute! e.g. <template lang="pug"> -->
<template>
  <div id="app">
    <!--O Vue traz diretivas pra poder trabalhar com eventos como o @click (nome autoexplicativo)-->
    <h1>Valor do bitcoin</h1>
    <button @click="fetchBitcoin">Pegar valor</button>

    <h2>Resultado em Json</h2>
    <p>{{ bitcoinValue }}</p>

    <!--Como o objeto que a API retorna tem chaves com _ eu usei essa maneira do JS de acessar o objeto parecido com o que o PHP faz ate-->
    <h2>Resultado chamando uma chave o objeto</h2>
    <p>"asset_id_quote": {{ bitcoinValue["asset_id_quote"] }}</p>

    <h2>Loop dentro das chaves de um objeto</h2>
    <ul>
      <!--Aqui se pa voce ja deve ter brincado com loops no vue, mas e uma maneira de iterar pelos dados que o proprio framework entrega-->
      <li v-for="property in bitcoinValue" :key="property">
        {{ property }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // aqui eu defino os valores que posso usar dentro do meu template
      // por ser mais rapido to inicializando a variavel bitcoinValue como objeto vazio
      // pra depois substituir ela pelo valor na chamada da API
      message: "Welcome to Vue!",
      bitcoinValue: {}
    };
  },
  methods: {
    async fetchBitcoin() {
      // A funcao fetch veio pra substituir a chamada do XMLhttpRequest
      // fazendo chamadas assincronas no codigo por meio de requisicoes http
      // pra usar e so por o endpoint dentro da funcao e fazer o tratamento da promise
      // que ela retorna pra converter no tipo de dado que voce precisa
      // no caso converti o meu response pra um json por ser mais facil de usar
      const response = await fetch(
        "https://rest.coinapi.io/v1/exchangerate/BTC/USD?apikey=FD3DD3DE-FD89-4F89-B5CB-49F798890CEC"
      );
      const json = await response.json();

      // to fazendo o bind do meu resultado na variavel definida no data()
      this.bitcoinValue = json;
    }
  }
};
</script>

<!-- Use preprocessors via the lang attribute! e.g. <style lang="scss"> -->
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

a,
button {
  color: #4fc08d;
}

button {
  background: none;
  border: solid 1px;
  border-radius: 2em;
  font: inherit;
  padding: 0.75em 2em;
}

p {
  max-width: 480px;
  margin: 2rem auto;
}
</style>
