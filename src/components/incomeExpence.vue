<template>
  <div class="tiles">
    <div class="tile tile--income">
      <p class="tile__label">Income</p>
      <p class="tile__value">₹{{ props.income }}</p>
    </div>
    <div class="tile tile--expence">
      <p class="tile__label">Expense</p>
      <p class="tile__value">₹{{ props.expence }}</p>
    </div>
  </div>
</template>


<script setup>
const props=defineProps({
    income:{
        type:Number
    },
    expence:{
        type:Number
    }
})
</script>

<style scoped>
.tiles {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 12px;
}

.tile {
  padding: 14px 16px;
  background-color: var(--card);
  border: 1px solid var(--line);
  border-radius: var(--radius-sm);
  box-shadow: var(--shadow);
}

.tile__label {
  margin: 0;
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: var(--muted);
}

.tile__value {
  margin: 4px 0 0;
  font-size: 20px;
  font-weight: 700;
  letter-spacing: -0.02em;
}

.tile--income .tile__value {
  color: var(--income);
}

.tile--expence .tile__value {
  color: var(--expence);
}
</style>
