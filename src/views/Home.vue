<template>
  <div class="home">
    <shoppinglist></shoppinglist>
  </div>
</template>

<script>
// @ is an alias to /src
import ShoppingList from '../components/ShoppingList.vue'

export default {
  name: 'Home',
  components: {
    shoppinglist: ShoppingList
  }
}
</script>
