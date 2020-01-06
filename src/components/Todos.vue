<template>
    <div>
        <div v-bind:key="todo.id" v-for="todo in todos">
            <p>
                {{todo.id}}
                {{todo.title}}

                    <input type="checkbox" @change="$emit('box-clicked',todo.id)">
            </p>
        
        </div>
    </div>
</template>

<script>
export default {
    name:'Todos',
    props:['todos'],

}
</script>

<style>

</style>