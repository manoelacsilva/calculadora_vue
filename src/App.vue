<script setup>
import { computed, reactive } from 'vue';

const estado = reactive ({
  num1: '',
  num2: '',
  operacao: '+',
});


const resultado = computed(() => {
  const n1 = parseFloat(estado.num1);
  const n2 = parseFloat(estado.num2);
  if (isNaN(n1) || isNaN(n2)) {
    return '';
  };
  switch (estado.operacao) {
    case '-':
      return n1 - n2;
    case '+':
      return n1 + n2;
    case '/':
      return n1 / n2;
    case '*':
      return n1 * n2;
    default:
      return '';
  };
});

const naoUmNumero1 = () => {
  const n1 = parseFloat(estado.num1);
  if (isNaN(n1) && estado.num1.length > 0) {
    return true;
  };
};

const naoUmNumero2 = () => {
  const n2 = parseFloat(estado.num2);
  if (isNaN(n2) && estado.num2.length > 0) {
    return true;
  };
};

</script>

<template>
  <div class="container">
    <div>
      <h1>Calculadora VueJS</h1>
      <h3>By Manoela Coelho</h3>
    </div>
    <div>
      <div class="calculadora">
        <input type="number" class="campo" v-model="estado.num1" :class="{naoUmNumero: naoUmNumero1()}" placeholder="Digite o primeiro número">
        <select class="operacoes" @change="evento => estado.operacao = evento.target.value">
          <option value="+">+</option>
          <option value="-">-</option>
          <option value="*">*</option>
          <option value="/">/</option>
        </select>
        <input type="number" class="campo" v-model="estado.num2" :class="{naoUmNumero: naoUmNumero2()}" placeholder="Digite o segundo número">
      </div>
      <div class="resultado" v-if="estado.num1 !== '' && estado.num2 !== ''">
        <h2>Resultado</h2>
        <span>
          {{ estado.num1 }} {{ estado.operacao }} {{ estado.num2 }} é igual a <strong>{{ resultado }}</strong>
        </span>
      </div>
    </div>
  </div>
</template>

<style scoped>

* {
  margin: 0;
  padding: 0;
}

h1 {
  font-size: 40px;
  margin-bottom: 15px;
}

h2 {
  margin-top: 60px;
  margin-bottom: 25px;
  font-size: 30px;
}

h3 {
  margin-bottom: 60px;
  font-size: 17px;
}

.container {
  font-family: 'Roboco', sans-serif;
  background-color: #ccc;
  width: 500px;
  text-align: center;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  flex-direction: column;
  margin: 0 auto;
  border-radius: 10px;
  padding: 60px;
}

.calculadora {
  display: flex;
  flex-direction: column;
  gap: 50px;
  align-items: center;
  margin: 0px 8px;
}

.operacoes {
  width: 100px;
  border: 2px solid #000;
  border-radius: 4px;
  text-align: center;
  display: flex;
  justify-content: center;
  outline: none;
  height: 45px;
  font-size: 20px;
  align-items: center;
}

.campo {
  outline: none;
  border: 2px solid #000;
  border-radius: 4px;
  height: 35px;
  font-size: 20px;
  padding: 3px 6px;
  width: 100%;
}

span {
  font-size: 20px;
}

@media (max-width: 700px) {
  h1 {
    font-size: 28px;
    margin-bottom: 10px;
  }

  h2 {
    margin-top: 30px;
    margin-bottom: 15px;
    font-size: 20px;
  }

  .container {
    width: 200px;
    text-align: center;
    position: absolute;
    flex-direction: column;
    border-radius: 10px;
    padding: 20px 45px;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
  }

  .calculadora {
    gap: 30px;
  }

  .operacoes {
    height: 28px;
    font-size: 15px;
    border: 1px solid #000;
    width: 70px;
  }

  .campo {
    outline: none;
    border: 1px solid #000;
    border-radius: 4px;
    height: 20px;
    font-size: 15px;
    padding: 3px 6px;
    width: 100%;
  }

  span {
    font-size: 15px;
  }

  h3 {
    margin-bottom: 30px;
    font-size: 12px;
  }
} 

</style>
