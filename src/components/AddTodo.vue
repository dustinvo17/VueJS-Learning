<template>
  <div>
      <form @submit="addtodo">
          <input type="text" v-model="item">
          <input type="submit" value="Add To do">
      </form>
  </div>
</template>

<script>
export default {
    name:"AddTodo",
    data(){
        return {
            item:''
        }
    },
      props:['currentID'],
    methods:{
        addtodo() {
          
            let newID = this.$props.currentID + 1
            const todo = {
                id:newID,
                title:this.item,
                completed:false
            }
            this.$emit('addToDo',todo)
        }
    },
  

}
</script>

<style>

</style>