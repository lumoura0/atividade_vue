<template>
  <div id="app">
    <h1>Calculadora Aritmética</h1>

    <label for="num1">Número 1:</label>
    <input v-model="num1" type="number" @input="calcularResultado" />

    <label for="operacao">Operação:</label>
    <select v-model="operacao" @change="calcularResultado">
      <option v-for="op in ['+', '-', '*', '/']" :value="op">
        {{ operacaoRotulo(op) }}
      </option>
    </select>

    <label for="num2">Número 2:</label>
    <input v-model="num2" type="number" @input="calcularResultado" />

    <p v-if="typeof resultado === 'number'">Resultado: {{ resultado }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      num1: 0,
      operacao: "+",
      num2: 0,
      resultado: null,
    };
  },
  methods: {
    calcularResultado() {
      const { num1, operacao, num2 } = this;
      this.resultado =
        isNaN(num1) || isNaN(num2) ? null : eval(`${num1} ${operacao} ${num2}`);
    },
    operacaoRotulo(op) {
      const rotulos = {
        "+": "Soma (+)",
        "-": "Subtração (-)",
        "*": "Multiplicação (*)",
        "/": "Divisão (/)",
      };
      return rotulos[op] || op;
    },
  },
};
</script>

<style>
#app {
  text-align: center;
  margin-top: 60px;
}

label {
  margin: 10px;
}
</style>
