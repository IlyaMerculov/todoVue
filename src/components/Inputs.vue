<script setup lang="ts">
    import { ref } from 'vue'
    
    const props = defineProps(['todos'])
    const newTodo : string = ref(''),
          newDate : string = ref('')

    const addTodo = () => {
        props.todos.push({id: Math.floor(Math.random() * 10000), todoValue: newTodo.value, todoDate: newDate.value, complete: false})
    }        

</script>
<template>
        <div class="inputs-frame">
            <input type="text" v-model="newTodo" placeholder="Введите задачу">
            <input type="date" v-model="newDate" >
            <button @click="addTodo">Добавить</button>
        </div>
</template>
<style>
    .inputs-frame{
        width: 400px;
        height: 50px;
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
</style>