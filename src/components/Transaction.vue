<script setup>
import {ref,computed} from 'vue'

const text=ref("");
const amount= ref(0);
const emit = defineEmits(["send-transaction",])

const isIncome = computed({
    get() {
        return amount.value >= 0
    },
    set(value) {
        amount.value = value ? Math.abs(amount.value) : -Math.abs(amount.value)
    }
})

function sendTransaction(){
    if (!text.value.trim() && !amount.value){
        throw new Error('Please enter description and amount for the transaction')
    }
    if (!text.value.trim()) {
        throw new Error('Please enter a description for the transaction.')
    }
    if (!amount.value) {
        throw new Error('Please enter an amount that is not zero.')
    }

    emit("send-transaction",{
        text:text.value,
        amount:amount.value}
    )
    text.value=""
    amount.value=0
}

</script>

<template>
    <div class="transaction">
        <h1 class="transaction__title">Add New Transaction</h1>

        <form class="form" @submit.prevent="sendTransaction">
            <div class="field">
                <h2 class="field__label">Text</h2>
                <input class="field__input" v-model="text" type="text" placeholder="Enter Text">
            </div>

            <div class="field">
                <h2 class="field__label">Amount</h2>
                <p class="field__hint">Negative for expence, positive for income</p>
                <input class="field__input" v-model.number = "amount" type="number" placeholder="Enter the amount here ">
            </div>

            <label class="toggle">
                <input type="checkbox" v-model="isIncome">
                {{ isIncome ? 'This is income' : 'This is an expense' }}
            </label>

            <button class="submit" type="submit">Add transaction</button>
        </form>
    </div>
</template>

<style scoped>
.transaction {
    padding: 18px 20px 20px;
    background-color: var(--card);
    border: 1px solid var(--line);
    border-radius: var(--radius);
    box-shadow: var(--shadow);
}

.transaction__title {
    margin: 0 0 14px;
    font-size: 16px;
    font-weight: 650;
    letter-spacing: -0.01em;
}

.form {
    display: flex;
    flex-direction: column;
    gap: 14px;
}

.field__label {
    margin: 0 0 5px;
    font-size: 11px;
    font-weight: 600;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    color: var(--muted);
}

.field__hint {
    margin: -2px 0 6px;
    font-size: 12px;
    color: var(--muted);
}

.field__input {
    width: 100%;
    padding: 11px 13px;
    font-family: inherit;
    font-size: 15px;
    color: var(--ink);
    background-color: #fbfcfd;
    border: 1px solid var(--line);
    border-radius: var(--radius-sm);
    outline: none;
    transition: border-color 0.15s ease, box-shadow 0.15s ease;
}

.field__input::placeholder {
    color: #a7b3c0;
}

.field__input:focus {
    background-color: #ffffff;
    border-color: var(--accent);
    box-shadow: 0 0 0 3px rgba(15, 118, 110, 0.14);
}

.toggle {
    display: flex;
    align-items: center;
    gap: 8px;
    font-size: 14px;
    color: var(--ink);
    cursor: pointer;
    user-select: none;
}

.toggle input {
    width: 16px;
    height: 16px;
    accent-color: var(--accent);
    cursor: pointer;
}

.submit {
    padding: 12px 16px;
    font-family: inherit;
    font-size: 15px;
    font-weight: 600;
    color: #ffffff;
    background-color: var(--dark);
    border: none;
    border-radius: var(--radius-sm);
    cursor: pointer;
    transition: background-color 0.15s ease, transform 0.15s ease;
}

.submit:hover {
    background-color: #223243;
}

.submit:active {
    transform: translateY(1px);
}
</style>
