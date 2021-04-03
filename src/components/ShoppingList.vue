<template>
    <div>
        <h1>Shoppping List</h1>
        <input type="text" placeholder="Item" v-model="item.name">
        <br>
        <input type="text" placeholder="Qty" v-model="item.qty">
        <br>
        <div v-for="error in errors" :key="error.index">
            <p>{{error}}</p>
        </div>
        <div class="add-item-btn">
            <b-button  pill variant="success" @click="addItem">Add</b-button>
        </div>
        
        <b-table striped hover :items="itemList"></b-table>
    </div>
</template>
<script>
export default {
    name: 'ShoppingList',
    data() {
        return {
            item: {
                name: null,
                qty: null
            },
            itemList: [],
            errors: []
        }
    },
    methods: {
        addItem() {
            if (!this.item.name) {
                this.errors.push("Enter Item name")
                return
            }
            if (isNaN(this.item.qty)) {
                this.errors.push("Qty should be a number")
                return
            }
            if (this.item.qty <= 0) {
                this.errors.push("Qty must be more than 0")
                return
            }

            this.itemList.push({name: this.item.name, qty: this.item.qty})
        }
    },
}
</script>
<style scoped>
.add-item-btn {
    margin-top: 5px;
}
input {
    margin-top: 7px;
}
</style>