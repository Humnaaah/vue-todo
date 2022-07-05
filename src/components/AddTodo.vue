<template>
    <div> 
        <form @submit="addTodo">
            <input type="text" class="inputElement" v-model="title" name="title" placeholder="Add  Todo" />
            <input type="submit" value="submit" class="btn" />
        </form>
    </div>
</template>

<script>
export default {
    name:"AddTodo",
    data(){
        return{
            title: ''
        }
    },
    methods:{
        addTodo(e){
            e.preventDefault();
            const newTodo= {
                title:this.title,
                completed:false, 
            }
            this.$emit('add-todo', newTodo);
            this.title = '';
        }
    }
}
</script>

<style scoped>
    form{
        display: flex;
    }
    input [type="text"]{
        flex: 10;
        padding: 5px;
       
    }
    input [type="submit"]{
        flex:2;
    }
    .inputElement{
         width: 90%;
        height: 30px;
        border-radius: 4px;
        border: 1px solid #bdb6b6;
        margin-top: 10px;
    }
    .btn{
    height: 33px;
    margin-top: 20;
    margin-top: 10px;
    margin-left: 10px;
    width: 130px;
    margin-right: 10px;
    border-radius: 4px;
    border: 1px solid green;
    background: green;
    color: white;
    }
</style>