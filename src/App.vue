<template>
  <Header />
  <div class="container">
    <Balance :total="+total"/>
    <IncomeExpenses :income="+income" :expenses="+expenses"/>
    <TransactionList :transactions="transactions" @transactionDeleted="handleTransactionDeleted"/>
    <AddTransaction @transactionSubmitted="handleTransactionSubmitted"/>
  </div>  
</template>









<script setup>
  import Header from './components/Header.vue';
  import Balance from './components/Balance.vue';
  import IncomeExpenses from './components/IncomeExpenses.vue';
  import TransactionList from './components/TransactionList.vue';
  import AddTransaction from './components/AddTransaction.vue';
  
  
  import {ref, computed, onMounted} from 'vue'
  import {useToast} from 'vue-toastification'

  const toast = useToast() // intialize toast

  const transactions = ref([]); // reactive? variable for transaction, basta yung nagbabago

  // load transactions from local storage on component mount
  onMounted(() =>{
    // retrieve the 'transactions' data from local storage and parse it into a js object
    const savedTransactions = JSON.parse(localStorage.getItem('transactions'))
    
    if(savedTransactions){
      transactions.value = savedTransactions
    }
  })


  // get total
  const total = computed(() => {
    return transactions.value.reduce((acc, transaction) => {
      return acc + transaction.amount; // pwede din for -value since positive + negative will just subtract
    }, 0);
  });

  // get income
  const income = computed(() => {
    return transactions.value.filter(transaction => transaction.amount > 0)
      .reduce((acc, transaction) => {
        return acc + transaction.amount;
      }, 0).toFixed(2);
  });

  //get expenses
  const expenses = computed(() => {
    return transactions.value.filter(transaction => transaction.amount < 0)
      .reduce((acc, transaction) => {
        return acc + transaction.amount;
      }, 0).toFixed(2);
  });

  // unique id generator
  const generateUniqueId = () => {
    return Math.floor(Math.random() * 1000)
  }

  // add transaction
  const handleTransactionSubmitted = (transactionData) => {
    // console.log(transactionData)
    transactions.value.push({
      id: generateUniqueId(),
      text: transactionData.text,
      amount: transactionData.amount
    })
    savedTransactionsToLocalStorage()
    toast.success('Transaction Added')
    // console.log(generateUniqueId())
  }

  // delete transaction
  const handleTransactionDeleted = (id) => {
    // console.log(id)
    transactions.value = transactions.value.filter((transaction => transaction.id !== id))
    savedTransactionsToLocalStorage()
    toast.success('Transaction deleted')
  }

  // save to localstorage
  const savedTransactionsToLocalStorage = () => {
    localStorage.setItem('transactions',JSON.stringify(transactions.value))
  }
</script>