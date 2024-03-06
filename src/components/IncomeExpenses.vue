<template>
    <div class="inc-exp-container">
        <div>
            <h4>Income</h4>
            <p id="money-plus" class="money plus">+₱{{income}}</p>
        </div>
        <div>
            <h4>Expenses</h4>
            <p id="money-minus" class="money minus">₱{{expenses}}</p>
        </div>
    </div>
</template>



<script setup>
    // Props is properties passed from parent components to child components.
    // `defineProps` is a function used to define props in a Vue 3 composition API setup.

    // BTW
    // Composition API is a feature in Vue 3 that allows for organizing code logic
    // in a more flexible and reusable way by using functions and reactive variables.
    const props = defineProps({
        income: {
            type:Number,
            required: true
        },
        expenses: {
            type:Number,
            required: true
        },
    });

</script>