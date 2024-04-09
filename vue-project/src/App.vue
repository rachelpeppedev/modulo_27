<script setup>
import { reactive } from 'vue';

const nome = "rachel peppe"
const meuObj = {
  nome: "rachel",
  filmeFavorito: "Derrepente 30"
}

function dizOla(nome) {
  return `${nome} diz Oi`;
}

const enderecoDaImagemDoBatman = "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ2ksk9mS35CTaWrrH9oT0cDUqBrkR-FbEmoQ&s"
const imagemSuperman = "https://t.ctcdn.com.br/sS0dqwq3BA9nGFigIH26q8YHOgI=/640x360/smart/i677638.jpeg"

const botaoEstaDesabilidado = false

const gostaDoBatman = false
const gostaDoSuperman = false

const estaAutorizado = false

// let contador = 0
const estado = reactive( {
  contador: 0,
  email: '',
  saldo: 5000,
  transferindo: 0,
})

function incrementar() {
  estado.contador++;
}

function decrementar() {
  estado.contador--;
}

function alteraEmail(evento) {
  estado.email = evento.target.value;
}

function mostraSaldoFuturo() {
  const { saldo, transferindo } = estado;
  return saldo - transferindo;
}

function validaValorTransferencia() {
  const { saldo, transferindo } = estado;
  return saldo >= transferindo;
}

</script>

<template>
    <h1>{{ dizOla("Paula") }}</h1>
    <img v-if="gostaDoBatman" :src="enderecoDaImagemDoBatman" alt="">
    <img v-else-if="gostaDoSuperman" :src="imagemSuperman" alt="">
    <h2 v-else>Não curte heróis da DC</h2>

    <h1 v-if="estaAutorizado">Bem-vindo</h1>
    <h1 v-else>Não possui acesso</h1>

    <button :disabled="!botaoEstaDesabilidado">Enviar mensagem</button>

    <br />
    <hr />

    {{ estado.contador }}

    <button @click="incrementar" type="button">+</button>
    <button @click="decrementar" type="button">-</button>

    <br />
    <hr />

    {{ estado.email }}
    <input type="email" @keyup="alteraEmail">

    <br />
    <hr />

    Saldo: {{ estado.saldo }} <br />
    Transferido: {{ estado.transferindo }} <br />
    Saldo depois da transferência: {{ mostraSaldoFuturo() }} <br />
    <input class="campo" :class="{invalido: !validaValorTransferencia()}" @keyup="evento => estado.transferindo = evento.target.value" type="number" placeholder="Quantia para transferir"/>
    <button v-if="validaValorTransferencia()">Transferir</button>
    <span v-else >Valor maior que o saldo</span>
</template>

<style scoped>

img {
  max-width: 200px;
}

.invalido {
  outline-color: red;
  border-color: red;
}

.campo {
  border: 2px solid #000;
}
</style>
