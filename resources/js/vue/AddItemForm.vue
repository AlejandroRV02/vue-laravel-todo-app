<template>
    <div class="add-item">
        <input type="text" v-model="item.name" />
        <font-awesome-icon icon="plus-square" 
        @click.prevent="addItem()"
        :class="[item.name ? 'active' : 'inactive', 'plus']"/>
    </div>
</template>

<script>

export default {

    data()  {
        return {
            item: {
                name: ""
            }
        }
    },
    methods: {
        addItem(){
            if(this.item.name === ''){
                return;
            }

            axios.post('api/item/store', {item: this.item})
            .then(res => {
                if(res.status == 201){
                    this.item.name = "";
                    this.$emit('reloadlist')
                }
            })
            .catch(err => {
                console.error(err);
            });
        }
    }

}
</script>

<style scoped>
.add-item{
    display: flex;
    justify-content: center;
    align-items: center;
}

input{
    background: #f7f7f7;
    border: 0px;
    outline: none;
    padding: 5px;
    margin-right:10px;
    width: 100%;
}


.plus{
    font-size: 20px;
}

.active{
    color: #00ce25;
}

.inactive{
    color: #999999;
}
</style>