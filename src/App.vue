<script setup>
import {ref,reactive,computed,watch,watchEffect,onErrorCaptured} from 'vue'
import Header  from './components/header.vue';
import Balance from './components/balance.vue';
import IncomeExpence from './components/incomeExpence.vue';
import Transaction from './components/Transaction.vue';
import History from './components/History.vue';

const balance = ref(0);
// const income = ref(0);
const income = computed(()=>
history
.filter(item=>item.isIncome)
.reduce((sum,item)=>sum+item.amount,0)
)
// const expence = ref(0);
const expence = computed(()=>
history
.filter(item=>item.isIncome)
.reduce((sum,item)=>sum+item.amount,0)
)
const saved = localStorage.getItem('history');
const history = reactive(saved ? JSON.parse(saved) : [])
watch(history, (value) => {
  localStorage.setItem('history', JSON.stringify(value))
}, { deep: true })

watchEffect(() => {
  document.title = `₹${balance.value} · Expence Tracker`
})

const errorMessage = ref('');

onErrorCaptured((error) => {
  errorMessage.value = error.message
  return false
})

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
  }
  else{
    history.push({
      text:transaction.text,
      amount:transaction.amount,
      isIncome:false
    })
  }
}
</script>


<template>

  <div class="page">
    <p v-if="errorMessage" role="alert">
      {{ errorMessage }}
      <button type="button" @click="errorMessage = ''">Dismiss</button>
    </p>

    <Header/>
    <Balance :balance="balance"/>
    <IncomeExpence :income="income" :expence="expence"/>
    <Transaction @send-transaction="addTransaction"/>
    <History :history="history"/>
  </div>

</template>
