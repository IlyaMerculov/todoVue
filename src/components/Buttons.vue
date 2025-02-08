<script setup lang="ts">

    const props = defineProps(['changeFilter', 'deleteAllComolete'])

</script>
<template>
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
</template>
<style>
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