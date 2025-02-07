<script setup lang="ts">
    import { ref, computed, watch } from 'vue'

    type ToDo = {
        id: number,
        todoValue: string,
        todoDate: string,
        complete: boolean
    }

    const newTodo : string = ref(''),
          newDate : string = ref(''),
          todos : ToDo[] = ref(JSON.parse(localStorage.getItem('tasks')) || []),
          action : string = ref('all')

    const addTodo = () => {
        todos.value.push({id: Math.floor(Math.random() * 10000), todoValue: newTodo.value, todoDate: newDate.value, complete: false})
        console.log(todos.value)
    }

    const removeToDo = (remove) => {
        todos.value = todos.value.filter((todo) => todo.id !== remove.id)
    }

    const filteredTodos = computed(() => {
        if(action.value === 'all') return todos.value
        if(action.value === 'active') return todos.value.filter((todo) => todo.complete !== true)
        if(action.value === 'complete') return todos.value.filter((todo) => todo.complete === true)
        if(action.value === 'today'){
            const curDate = new Date().toISOString().split('T')[0]
            return todos.value.filter((todo) => todo.todoDate === curDate)
        }
        if(action.value === 'after'){
            

            const curDate = new Date().toISOString().split('T')[0]
            console.log('tut', curDate)
            return todos.value.filter((todo) => todo.todoDate < curDate)
        }
        if(action.value === 'before'){
            const curDate = new Date().toISOString().split('T')[0]
            return todos.value.filter((todo) => todo.todoDate > curDate)
        }
    })

    const changeFilter = (curAction) => {
        console.log(curAction)
        action.value = curAction
    }

    const deleteAllComolete = () => {
        todos.value = todos.value.filter((todo) => todo.complete !== true)
    }

    watch(todos, () => {
        localStorage.setItem('tasks', JSON.stringify(todos.value));
        console.log(localStorage, todos.value, new Date().toISOString().split('T')[0])
    }, { deep: true })


</script>

<template>
    <div class="main-frame">
        <div class="inputs-frame">
            <input type="text" v-model="newTodo" placeholder="Введите задачу">
            <input type="date" v-model="newDate" placeholder="Введите задачу">
            <button @click="addTodo">Добавить</button>
        </div>
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
                    <button @click="removeToDo(todo)">X</button>
                </div>
            </div>
        </div>
        <div class="buttons-frame">
            <div class="buttons-filter">
                <button @click="changeFilter('all')" >Все</button>
                <button @click="changeFilter('active')" >Активные</button>
                <button @click="changeFilter('complete')" >Сделанные</button>
            </div>
            <div class="buttons-specific">
                <button @click="deleteAllComolete">Удалить все сделанные</button>
                <button @click="changeFilter('today')">Сегодня</button>
                <button @click="changeFilter('after')">Предстоящие</button>
                <button @click="changeFilter('before')">Просроченные</button>
            </div>
        </div>
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
    .inputs-frame{
        width: 400px;
        height: 50px;
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
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
        filter: drop-shadow(0px 0px 3px #23395B)
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
    .buttons-frame{
        width: 500px;
        height: 60px;
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
    }
    .buttons-filter{
        width: 100%;
        height: 30px;
        display: flex;
        align-items: center;
        justify-content: space-evenly;
    }
    .buttons-specific{
        width: 100%;
        height: 30px;
        display: flex;
        align-items: center;
        justify-content: space-evenly;
    }
</style>