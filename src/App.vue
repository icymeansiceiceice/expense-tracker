<template>
  <div>
    <Header></Header>
    <div class="container">
      <Balance :total="total"></Balance>
      <InComeExpense :income="income" :expense="expense"></InComeExpense>
      <TransactionList :transactions="transactions"></TransactionList>
      <AddTransaction></AddTransaction>
    </div>
  </div>
</template>

<script setup>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import InComeExpense from './components/InComeExpense.vue';
import TransactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';

import { computed, ref } from 'vue';

const transactions = ref([
    {id:1,text:'flower',amount:-19.99},
    {id:1,text:'salary',amount:299.99},
    {id:1,text:'book',amount:-19},
    {id:1,text:'camera',amount:300}
]);

const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0);
});

const income = computed(() => {
  return transactions.value.filter((transactions)=> transactions.amount>0).reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0).toFixed(2);
});

const expense = computed(() => {
  return transactions.value.filter((transactions)=> transactions.amount<0).reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0).toFixed(2);
});

</script>

<style lang="scss" scoped>

</style>