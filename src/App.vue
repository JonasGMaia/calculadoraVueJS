<script setup>
import { reactive } from 'vue';


const estado = reactive({
  primeiroNumero: 0,
  segundoNumero: 0,
  operador: 'soma',
})

function recebePrimeiroNumero(evento){
  estado.primeiroNumero = evento.target.value;
}
function recebeSegundoNumero(evento){
  estado.segundoNumero = evento.target.value;
}

const somaNumeros = () =>{
  const {primeiroNumero, segundoNumero} = estado;
  return primeiroNumero + segundoNumero;
}

const subtracaoNumeros= () =>{
  const {primeiroNumero, segundoNumero} = estado;
  return primeiroNumero - segundoNumero;
}

const multiplicacaoNumeros= () =>{
  const {primeiroNumero, segundoNumero} = estado;
  return primeiroNumero * segundoNumero;
}

const divisaoNumeros= () =>{
  const {primeiroNumero, segundoNumero} = estado;
  return primeiroNumero / segundoNumero;
}

const operacaoNumeros = () => {
  const {primeiroNumero, segundoNumero, operador} = estado;

  if (isNaN(primeiroNumero) || isNaN(segundoNumero) || !isFinite(primeiroNumero) || !isFinite(segundoNumero)) {
    return 0; 
  }

  switch (operador) {
    case 'soma':
      return somaNumeros();
    case 'subtracao':
      return subtracaoNumeros();
    case 'multiplicacao':
      return multiplicacaoNumeros();
    case 'divisao':
      if (segundoNumero === 0) {
        return 'Divisão por 0';
      } else{return divisaoNumeros()};
    default: return 0;
  }
}
</script>

<template>
  <div class="container">
    <header class="text-bg-success rounded mt-3 p-3">
      <h1>Calculadora</h1>
      <p class="text-white-50">Use esta calculadora para fazer multiplicação, divisão, soma e subtração entre dois números.</p>
    </header>
    <main>
      <form action="">
        <div class="d-grid m-3">
          <label for="">Primeiro Número</label>
          <input @keyup="evento => estado.primeiroNumero = parseFloat(evento.target.value)" class="form-control" type="text" placeholder="Digite aqui um número">
        </div>
        <div class="d-grid m-3">
          <label for="">Segundo Número</label>
          <input @keyup="evento => estado.segundoNumero = parseFloat(evento.target.value)" class="form-control" type="text" placeholder="Digite aqui um número">
        </div>
        <div class="row">
          <div class="col-6 ms-3 d-grid">
            <label for="">Escolha uma operação</label>
            <select @change="evento => estado.operador = evento.target.value" class="form-control">
              <option value="soma">soma</option>
              <option value="subtracao">subtração</option>
              <option value="multiplicacao">multiplicação</option>
              <option value="divisao">divisão</option>
            </select>
          </div>
        </div>
      </form>
      
      <div class="d-grid m-3">
        <h2 class="text-success">RESULTADO:{{ operacaoNumeros() }}</h2>
      </div>
    </main>
  </div>
</template>

<style scoped>

</style>
