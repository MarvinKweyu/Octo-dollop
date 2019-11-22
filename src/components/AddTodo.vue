<template>
<div>
    <form @submit="addTodo">
        <input type="text" v-model="title" name="title" placeholder="Add Todo...">
        <input type="submit" value="Submit" class="btn">
    </form>
</div>
    
</template>


<script>
// import uuid from 'uuid'; // since jsonplaceholder gives unique id by default

export default {
    name: "AddToDo",
    data(){
        return{
            title:""
        }
    },
    methods:{
        addTodo(e){
            e.preventDefault(); // since we don't want it submitting to a file
            const newTodo = {
                // id: uuid.v4(), // create a unique id
                title: this.title,
                completed: false
            }
            // send up to parent
            this.$emit('add-todo', newTodo);
            // clear form after hit submit
            this.title = '';
        }
    }

}
</script>

<style scoped>
    form{
        display: flex;
    }

    input[type="text"]{
        flex: 10;
        padding:5px;
    }

    input[type="submit"]{
        flex: 2;
    }


</style>