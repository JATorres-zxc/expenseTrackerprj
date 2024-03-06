<template>
    <h4>Your Balance</h4>
    <h1 id="balance">₱{{total}}</h1>
</template>

<script setup>
    // Props is properties passed from parent components to child components.
    // `defineProps` is a function used to define props in a Vue 3 composition API setup.

    // BTW
    // Composition API is a feature in Vue 3 that allows for organizing code logic
    // in a more flexible and reusable way by using functions and reactive variables.
    const props = defineProps({
        total: {
            type:Number, // type of prop
            required: true // prop required
        },
    });
</script>