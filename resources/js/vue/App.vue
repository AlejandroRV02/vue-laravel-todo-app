<template>
    <div class="todo-list-container">
    
        <div class="heading">
            <h2 id="title">To Do List</h2>
            <AddItemForm v-on:reloadlist="getItems()" />
        </div>
        <ListView :items="items"
        v-on:reloadlist="getItems()"/>

    </div>
</template>

<script>
import AddItemForm from './AddItemForm';
import ListView from './ListView';

export default{
    data(){
        return{
            items: []
        }
    },
    components: {
        AddItemForm,
        ListView
    },
    methods: {
        getItems(){
            axios.get('api/items')
            .then(res => this.items = res.data)
            .catch(err => console.error(err));
        }
    },
    created(){
        this.getItems();
    }

}
</script>

<style scoped>

.todo-list-container{
    width: 350px;
    margin: auto;

}

.heading{
    background : #e6e6e6;
    padding: 10px;
}

#title{
    text-align: center;

}

</style>