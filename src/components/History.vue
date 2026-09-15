<script setup>
const props=defineProps(
    {
        history:{
            type:Array
        }
    }
)
</script>

<template>
    <div class="history" v-if="props.history.length > 0">
        <h1 class="history__title">History</h1>

        <div class="history__list" >
            <div class="entry" v-for="his in props.history" :key="his.id">
                <p class="entry__text">{{ his.text }}</p>
                <p class="entry__amount entry__amount--income" v-if="his.isIncome">{{ his.amount }}</p>
                <p class="entry__amount entry__amount--expence" v-else>{{ his.amount}}</p>
            </div>
        </div>
    </div>
</template>

<style scoped>
.history__title {
    margin: 0 0 10px 2px;
    font-size: 13px;
    font-weight: 600;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    color: var(--muted);
}

.history__list {
    display: flex;
    flex-direction: column;
    gap: 8px;
}

.entry {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 12px;
    padding: 12px 14px;
    background-color: var(--card);
    border: 1px solid var(--line);
    border-left: 4px solid var(--line);
    border-radius: var(--radius-sm);
    box-shadow: var(--shadow);
}

/* :has() lets the row colour itself based on which child rendered */
.entry:has(.entry__amount--income) {
    border-left-color: var(--income);
}

.entry:has(.entry__amount--expence) {
    border-left-color: var(--expence);
}

.entry__text {
    margin: 0;
    font-size: 14.5px;
    font-weight: 500;
    overflow-wrap: anywhere;
}

.entry__amount {
    margin: 0;
    font-size: 15px;
    font-weight: 700;
    white-space: nowrap;
    font-variant-numeric: tabular-nums;
}

.entry__amount--income {
    color: var(--income);
}

.entry__amount--expence {
    color: var(--expence);
}
</style>
