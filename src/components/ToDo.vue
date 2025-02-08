<script setup lang="ts">
    import { ref, computed, watch } from 'vue'

    import Buttons from './Buttons.vue'
    import Inputs from './Inputs.vue'
    import List from './List.vue'

    import type ToDo from '../types'
   
    const todos : ToDo[] = ref(JSON.parse(localStorage.getItem('tasks')) || []),
          action : string = ref('all')

    const removeToDo = (remove) => {
        todos.value = todos.value.filter((todo : ToDo) => todo.id !== remove.id)
    }

    const changeFilter = (curAction) => {
        console.log(curAction)
        action.value = curAction
    }

    const deleteAllComolete = () => {
        todos.value = todos.value.filter((todo : ToDo) => todo.complete !== true)
    }

</script>

<template>
    <div class="main-frame">
       <Inputs  :todos="todos" />
       <List :todos="todos" :action="action" :remove="removeToDo"/>
       <Buttons :changeFilter="changeFilter" :deleteAllComolete="deleteAllComolete"/>
    </div>
</template>

<style>
    .main-frame{
        width: 100%;
        height: 100%;
        display: flex;
        align-items: center;
        justify-content: flex-start;
        flex-direction: column;
    }
</style>