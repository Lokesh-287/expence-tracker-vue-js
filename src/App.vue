<script setup>
import {ref,reactive,computed,watch,watchEffect,onErrorCaptured,nextTick} from 'vue'
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
const errorBanner = ref(null);

onErrorCaptured((error) => {
  errorMessage.value = error.message
  nextTick(() => {
    errorBanner.value?.focus()
  })
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
    <p v-if="errorMessage" ref="errorBanner" class="error-banner" role="alert" tabindex="-1">
      {{ errorMessage }}
      <button type="button" class="error-banner__dismiss" @click="errorMessage = ''">Dismiss</button>
    </p>

    <Header/>
    <Balance :balance="balance"/>
    <IncomeExpence :income="income" :expence="expence"/>
    <Transaction @send-transaction="addTransaction"/>
    <History :history="history"/>
  </div>

</template>

<style scoped>
.error-banner {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
  margin: 0 0 16px;
  padding: 12px 14px;
  background-color: var(--expence);
  color: #ffffff;
  border-radius: var(--radius-sm);
  font-size: 14px;
  font-weight: 500;
}

.error-banner:focus {
  outline: 2px solid #ffffff;
  outline-offset: 2px;
}

.error-banner__dismiss {
  flex-shrink: 0;
  padding: 4px 10px;
  font-family: inherit;
  font-size: 13px;
  font-weight: 600;
  color: var(--expence);
  background-color: #ffffff;
  border: none;
  border-radius: 6px;
  cursor: pointer;
}
</style>
