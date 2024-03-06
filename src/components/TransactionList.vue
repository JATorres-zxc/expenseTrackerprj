<template>
    <h3>History</h3>
    <ul id="list" class="list">
        <!-- key value pair for loop  -->
        <!-- class with condition for css depending on the condition -->
        <li 
            v-for="transaction in transactions" :key="transaction.id"
            :class="transaction.amount < 0 ? 'minus' : 'plus'"
        > 

        {{ transaction.text }} <span>₱{{ transaction.amount }}</span>
        <button @click="deleteTransaction(transaction.id)" class="delete-btn">
        x
        </button>
        </li>
    </ul>
</template>

<script setup>
    const emit = defineEmits(['transactionDeleted']);
    // Props is properties passed from parent components to child components.
    // `defineProps` is a function used to define props in a Vue 3 composition API setup.

    // BTW
    // Composition API is a feature in Vue 3 that allows for organizing code logic
    // in a more flexible and reusable way by using functions and reactive variables.
    const props = defineProps({
        transactions: {
            type: Array,
            required: true,
        },
    });

    const deleteTransaction = (id) => {
        emit('transactionDeleted', id);
    };
</script>