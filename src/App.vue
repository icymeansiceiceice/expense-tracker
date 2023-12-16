<template>
  <div>
    <Header></Header>
    <div class="container">
      <Balance :total="+total"></Balance>
      <InComeExpense :income="+income" :expense="+expense"></InComeExpense>
      <TransactionList :transactions="transactions" @transactionDeleted="handleTransactionDeleted"></TransactionList>
      <AddTransaction @transactionSubmitted="handleTransactionSubmitted"></AddTransaction>
    </div>
  </div>
</template>

<script setup>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import InComeExpense from './components/InComeExpense.vue';
import TransactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';

import { computed, ref, onMounted } from 'vue';
import { useToast } from 'vue-toastification'

const toast = useToast();

const transactions = ref([]);

onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem('transactions'));

  if(savedTransactions){
    transactions.value = savedTransactions;
  }
});

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

const handleTransactionSubmitted = (transactionData)=>{
  transactions.value.push({
      id : generateUniqueId(),
      text : transactionData.text,
      amount : transactionData.amount
});
saveTransactionToLocalStroage();
  toast.success('transaction added');
}

const handleTransactionDeleted = (id)=>{
  transactions.value = transactions.value.filter((transaction) => transaction.id !== id);
  saveTransactionToLocalStroage();
  toast.success('transaction deleted');
}

const generateUniqueId = ()=>{
  return Math.floor(Math.random() * 100000);
}

const saveTransactionToLocalStroage = ()=>{
  localStorage.setItem('transactions',JSON.stringify(transactions.value));
}

</script>

<style lang="scss" scoped>

</style>