<template>
     <h3>History</h3>
      <ul id="list" class="list">
        <li v-for="transaction in transactions" 
          :key="transaction.id"  
          :class="transaction.amount > 0 ? 'plus': 'minus'"
          >
            {{transaction.text}} <span>${{transaction.amount}}</span>
            <button @click="handleDelete(transaction.id)" class="delete-btn">x</button>
        </li>
      </ul>
</template>

<script setup>
  import { defineProps, defineEmits } from 'vue';

  const emits = defineEmits(['del-task'])
  const props = defineProps({
    transactions:{
      type:Array,
      required:true,
    }
  })

  const handleDelete = (id) => {
    emits('del-task', id)
  }


</script>