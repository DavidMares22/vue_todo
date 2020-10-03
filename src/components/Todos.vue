<template>
    <div>
        <div v-bind:key="todo.id" v-for="todo in tasks">
            <h3>{{todo.title}}</h3>
        </div>
    </div>
</template>

<script>
export default {
    name: "Todos",
    props: ["tasks"]
}
</script>

<style scoped>

</style>