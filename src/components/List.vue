<script setup lang="ts">

    import { ref, computed, watch } from 'vue'

    import type ToDo from '../types'

    const props = defineProps(['todos', 'action', 'remove'])

    const filteredTodos = computed(() => {
        props.todos.forEach((el) => console.log(el))
        console.log(props.todos)
        if(props.action === 'all') return props.todos
        if(props.action === 'active') return props.todos.filter((todo : ToDo) => todo.complete !== true)
        if(props.action === 'complete') return props.todos.filter((todo: ToDo) => todo.complete === true)
        if(props.action === 'today'){
            const curDate = new Date().toISOString().split('T')[0]
            return props.todos.filter((todo : ToDo) => todo.todoDate === curDate)
        }
        if(props.action === 'after'){
            const curDate = new Date().toISOString().split('T')[0]
            console.log('tut', curDate)
            return props.todos.filter((todo : ToDo) => todo.todoDate > curDate)
        }
        if(props.action=== 'before'){
            const curDate = new Date().toISOString().split('T')[0]
            return props.todos.filter((todo : ToDo) => todo.todoDate < curDate)
        }
    })


    watch(props.todos, () => {
        localStorage.setItem('tasks', JSON.stringify(props.todos));
        console.log(localStorage, props.todos, new Date().toISOString().split('T')[0])
    }, { deep: true })

</script>
<template>
         <div class="list-frame">
            <div class="list-el" :class="{done : todo.complete}" v-for="todo in filteredTodos" :key="todo.id">
                <div class="checkbox-frame">
                    <input type="checkbox" v-model="todo.complete" />
                </div>
                <div class="main-text-frame">
                    <div>
                        {{ todo.todoValue }}
                    </div>
                    <div>
                        {{  todo.todoDate }}
                    </div>
                </div>
                <div class="del-button-frame">
                    <button @click="remove(todo)">X</button>
                </div>
            </div>
        </div>
</template>
<style>
    .list-frame{
        width: 350px;
        height: 550px;
        display: flex;
        align-items: center;
        justify-content: flex-start;
        flex-direction: column;
        overflow: auto;
        border-radius: 10px;
    }
    .list-el{
        display: flex;
        margin: 5px 5px 5px 5px;
        width: 97%;
        height: 60px;
        background-color: brown;
        border-radius: 10px;
        font-size: 0.8em;
        background-color: #23395B;
        color: #FFFFFF;
        filter: drop-shadow(0px 0px 3px #23395B);
        animation-duration: 3s;
        animation-name: slidein;
        animation-duration: 3s;
        animation-name: fade;
    }
    .checkbox-frame{
        width: 60px;
        height: 60px;
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .main-text-frame{
        width: calc(100% - 120px);
        height: 60px;
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
    }
    .del-button-frame{
        width: 60px;
        height: 60px;
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .done{
        background-color: #06935e;;
        color: #FFFFFF;
        filter: drop-shadow(0px 0px 3px #06935e)
    }

    @keyframes slidein {
        from {
            margin-left: 100%;
        }

        to {
            margin-left: 5px;
        }
    }

</style>