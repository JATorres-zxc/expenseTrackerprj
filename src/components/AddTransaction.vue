<template>
    <h3>Add new transaction</h3>
    <form id="form" @submit.prevent="onSubmit">

        <div class="form-control">
            <label for="text">Text</label>
            <input type="text" v-model="text" id="text" placeholder="Enter text..." />
        </div>

        <div class="form-control">
            <label for="amount">Amount <br />
                (negative - expense, positive - income)
            </label>

            <input type="text" v-model="amount" id="amount" placeholder="Enter amount..." />
        </div>

        <button class="btn">Add transaction</button>

    </form>
</template>

<script setup>
    import { ref } from 'vue'
    import {useToast} from 'vue-toastification' // for toast message

    const text = ref('') // store text input 
    const amount = ref('') // store amount input
    const toast = useToast() // initialize toast function
    const emit = defineEmits(['transactionSubmitted']) // custom event

    // function handle form submission
    const onSubmit = () => {
        if(!text.value || !amount.value){ // to check if text and amount fields is filled
            toast.error('Both fields (Text and Amount) MUST be filled') // error toast if something is empty
            return
        }
        // console.log(text.value, amount.value)   
        const transactionData = { // create transaction data object which is the text and amount
            text: text.value,
            amount: parseFloat(amount.value)
        }

        emit('transactionSubmitted', transactionData) // emit custom event 
        
        // then clear again
        text.value = ''
        amount.value = ''
    };
</script>