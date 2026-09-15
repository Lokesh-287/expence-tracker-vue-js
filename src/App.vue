<script setup>
import {ref,reactive} from 'vue'
import Header  from './components/header.vue';
import Balance from './components/balance.vue';
import IncomeExpence from './components/incomeExpence.vue';
import Transaction from './components/Transaction.vue';
import History from './components/History.vue';

let balance = ref(0);
let income = ref(0);
let expence = ref(0);
let history = reactive([])

function addTransaction(transaction){
  if(transaction.amount===0){
    return
  }
  if (transaction.amount > 0){
    history.push({
      text:transaction.text,
      amount:transaction.amount,
      isIncome:true
    })
    update_income(transaction.amount)
  }
  else{
    history.push({
      text:transaction.text,
      amount:transaction.amount,
      isIncome:false
    })
    update_expence(transaction.amount)
  }
  
}

function update_income(amount){
  income.value+=amount
  balance.value+=(amount)
}

function update_expence(amount){
  expence.value+=amount
  balance.value+=(amount)
}

</script>


<template>

  <div class="page">
    <Header/>
    <Balance :balance="balance"/>
    <IncomeExpence :income="income" :expence="expence"/>
    <Transaction @send-transaction="addTransaction"/>
    <History :history="history"/>
  </div>

</template>
