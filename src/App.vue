<template>
  <h1>Ahorros -> ${{ ahorros }}</h1>
  <button v-on:click="depositar(100)">Depositar $100</button>
  <br />
  <br />
  <button v-on:click="retirar(100)" v-bind:disabled="deshabilitarBtn">
    Retirar $100
  </button>
  <div>
    <h3>Movimientos</h3>
    <ul>
      <li v-for="(movimiento, index) in arrayOrdenado" v-bind:key="index">
        <span v-if="movimiento.monto > 0">Deposito</span>
        <span v-else>Retiro</span>
        | {{ movimiento.monto }}$ ➡️ Saldo Actual: {{ movimiento.saldoActual }}$
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
import { computed, ref } from "vue";

interface IMovimiento {
  monto: number;
  saldoActual: number;
}

const ahorros = ref(0);
const movimientos = ref<IMovimiento[]>([]);

const depositar = (cantidad: number) => {
  ahorros.value += cantidad;
  movimientos.value.push({
    monto: cantidad,
    saldoActual: ahorros.value,
  });
};

const retirar = (cantidad: number) => {
  ahorros.value -= cantidad;
  movimientos.value.push({
    monto: -cantidad,
    saldoActual: ahorros.value,
  });
};

const deshabilitarBtn = computed(() => {
  return ahorros.value === 0;
});

const arrayOrdenado = computed(() => {
  return [...movimientos.value].reverse();
});
</script>

<style scoped></style>
