<template>
  <div>
    <Header></Header>
    <div class="container">
      <Balance></Balance>
      <InComeExpense></InComeExpense>
      <TransactionList></TransactionList>
    </div>
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import InComeExpense from './components/InComeExpense.vue';
import TransactionList from './components/TransactionList.vue';


export default {
  components:{
    Header,
    Balance,
    InComeExpense,
    TransactionList
  },
  setup () {
    

    return {}
  }
}
</script>

<style lang="scss" scoped>

</style>