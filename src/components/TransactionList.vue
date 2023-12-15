<template>
    <div>
        <h3>History</h3>
        <ul id="list" class="list">
            <li v-for="transaction in transactions" :key="transactions.id" :class="transactions.amount<0 ? 'minus':'plus' ">    
                {{transaction.text }}  <span>${{ transaction.amount }}</span>
                <button class="delete-btn">x</button>
            </li>
        </ul>
    </div>
</template>

<script setup>

 const props = defineProps({
    transactions: {
        type: Array,
        required : true
    }
 });


</script>

<style lang="scss" scoped>

</style>