<template>
    <div class="item">
        <input type="checkbox" @change="updateItem()"
        v-model="item.completed"/>
        <span :class="[item.completed ? 'completed' : '', 'item-text']">{{item.name}}</span>
        <button 
        @click.prevent="deleteItem()" class="trashcan">
            <font-awesome-icon icon="trash" />
        </button>
    </div>
</template>


<script>
export default {
    props: ['item'],
    methods: {
        deleteItem(){
            axios.delete(`api/item/${this.item.id}`)
            .then(res => {
                if(res.status == 200){
                    this.$emit('itemchanged');
                }
            })
            .catch(err => console.error(err))
            
        },
        updateItem(){
            axios.put(`api/item/${this.item.id}`, {item: this.item})
            .then(res => {
                if(res.status == 200){
                    this.$emit('itemchanged');
                }
            })
            .catch(err => console.error(err))
        }
    }
}
</script>

<style scoped>

.completed{
    text-decoration: line-through;
    color: #999999;
}

.item-text{
    width:100%;
    margin-left: 20px;
}

.item{
    display: flex;
    justify-content: center;
    align-items: center;
}

.trashcan{
    background: #e6e6e6;
    border: none;
    color: #FF0000;
    outline: none;
}

</style>