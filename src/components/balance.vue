<script setup>
const props=defineProps(
    {
        balance:{
            type:Number
        }
    }
)
</script>

<template>
    <div class="balance">
        <p class="balance__label">Your balance</p>
        <h1 class="balance__value"><span class="balance__unit">₹</span>{{ balance }}</h1>
    </div>
</template>

<style scoped>
.balance {
    padding: 20px 22px 22px;
    background-color: var(--dark);
    border-radius: var(--radius);
    box-shadow: var(--shadow-lift);
    color: #ffffff;
}

.balance__label {
    margin: 0;
    font-size: 11px;
    font-weight: 600;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    opacity: 0.55;
}

.balance__value {
    margin: 6px 0 0;
    font-size: 36px;
    font-weight: 700;
    letter-spacing: -0.03em;
    line-height: 1;
}

.balance__unit {
    margin-right: 2px;
    font-size: 22px;
    font-weight: 600;
    opacity: 0.6;
    vertical-align: 4px;
}
</style>
