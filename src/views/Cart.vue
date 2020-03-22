<template>
  <div>
    <h1 v-if="cart.length === 0" class="message">No items in cart</h1>

    <h1 v-else class="message">Total: {{ total }}</h1>

    <div class="wrapper">
      <div class="books">
        <div class="book" v-for="book in cart" :key="book.id">
          <div class="info">
            <h1>{{book.name}}</h1>
            <p>{{book.country}}</p>
          </div>
          <div class="image">
            <img :src="'/images/books/'+book.image" />
          </div>
          <div class="price">
            <h2>{{book.price}}</h2>
            <button class="auto" @click="remove(book)">Remove From Cart</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Cart",
  components: {},
  computed: {
    cart() {
      return this.$root.$data.cart;
    },
    total() {
      let total = 0.0;
      this.cart.forEach(
        book => (total += parseFloat(book.price.substring(1)))
      );
      return "$" + total.toFixed(2);
    }
  },
  methods: {
    remove(book) {
      var index = this.$root.$data.cart.indexOf(book);
      if (index !== -1) {
        this.$root.$data.cart.splice(index, 1);
      }
    }
  }
};
</script>

<style scoped>
.wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
}

.books {
  margin-top: 20px;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}

.book {
  margin: 10px;
  margin-top: 50px;
  width: 200px;
}

.book img {
  border: 2px solid #333;
  height: 250px;
  width: 200px;
  object-fit: cover;
}

.book .image {
  display: flex;
  justify-content: center;
  margin-bottom: 5px;
}

.info {
  background: #1daff2;
  color: #000;
  padding: 10px 30px;
  height: 80px;
}

.info h1 {
  font-size: 16px;
}

.info h2 {
  font-size: 14px;
}

.info p {
  margin: 0px;
  font-size: 10px;
}

.price {
  display: flex;
}

button {
  height: 50px;
  background: #000;
  color: white;
  border: none;
}

.auto {
  margin-left: auto;
}

.message {
  background: #1daff2;
  color: #000;
  padding: 10px 30px;
  height: 80px;
  text-align: center;
}
</style>