<template>
  <div>
    <h1>Shoppping List</h1>
    <input
      type="text"
      placeholder="Item"
      v-model="item.name"
      @keyup.enter="addItem"
    />
    <br />
    <input
      type="text"
      placeholder="Qty"
      v-model="item.qty"
      @keyup.enter="addItem"
    />
    <br />
    <div v-for="error in errors" :key="error.index">
      <p>{{ error }}</p>
    </div>
    <div class="add-item-btn">
      <b-button @keydown.enter="addItem" pill variant="success" @click="addItem"
        >Add</b-button
      >
    </div>

    <b-table hover :items="itemList">
      <template #cell(actions)="row">
        <button @click="removeItem(row.item)"  type="button" class="close" aria-label="Close">
         {{row.item.actions}}
        </button>
      </template>
    </b-table>
  </div>
</template>
<script>
export default {
  name: "ShoppingList",
  data() {
    return {
      item: {
        name: null,
        qty: null
      },
      fields: [
        {
          key: "name",
          sortable: true,
          label: "Item Name",
        },
        {
          key: "qty",
          sortable: true,
          label: "Qty",
        },
        {
          key: "actions",
          sortable: false,
          label: "Remove?",
        },
      ],
      itemList: [{
        name: 'null',
        qty: 1,
        actions: 'x'
      }],
      errors: [],
    };
  },
  methods: {
    addItem() {
      this.errors = [];
      if (!this.item.name) {
        this.errors.push("Enter Item name");
        return;
      }
      if (isNaN(this.item.qty)) {
        this.errors.push("Qty should be a number");
        return;
      }
      if (this.item.qty <= 0) {
        this.errors.push("Qty must be more than 0");
        return;
      }

      this.itemList.push({ name: this.item.name, qty: this.item.qty, actions: 'x' });
      this.item.name = null;
      this.item.qty = null;
    },
    removeItem(item) {
        this.$delete(this.itemList, this.itemList.indexOf(item));
    }
  },
};
</script>
<style scoped>
.add-item-btn {
  margin-top: 5px;
}
input {
  margin-top: 7px;
}
</style>