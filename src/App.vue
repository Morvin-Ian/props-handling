<template>
  <Header />
  <div class="container">
    <Balance :total="total" />
    <Expenses :expense="-expense" :income="+income" />
    <TransactionList :transactions="transactions" @del-task="handleDelete"/>
    <AddTransaction @new_transaction="handleSubmit"/>
  </div>
</template>


<script setup>
import { ref, computed } from 'vue'

import Header from "./components/Header.vue"
import Balance from "./components/Balance.vue"
import Expenses from "./components/Expenses.vue"
import TransactionList from "./components/TransactionList.vue"
import AddTransaction from "./components/AddTransaction.vue"


const transactions = ref([
  { id: 1, text: 'Movies', amount: -90 },
  { id: 2, text: 'Salary', amount: 900.07 },
  { id: 3, text: 'Shopping', amount: -300 },
  { id: 4, text: 'Twitter Monitization', amount: 500 }
])



const total = computed(() => {
  return transactions.value.reduce((intial, transaction) => {
    return (intial + transaction.amount)
  }, 0)
});

const income = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((intial, transaction) => {
      return (intial + transaction.amount)

    }, 0).toFixed(2)
});


const expense = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((intial, transaction) => {
      return (intial + transaction.amount)

    }, 0).toFixed(2)
});

const handleSubmit = (newTransaction) => {
  transactions.value.unshift({
    id: Math.floor(Math.random * 10000),
    text: newTransaction.text,
    amount: newTransaction.amount
  })
}

const handleDelete = (id) => {
  transactions.value = transactions.value.filter(
    (transaction) => id !== transaction.id
  );
}

</script>

<style scoped></style>
