<template>
  <div>
    <div class="pure-menu pure-menu-horizontal">
      <ul class="pure-menu-list">
        <li v-for="author in authors" :key="author" class="pure-menu-item">
          <a @click="select(author)" href="#" class="pure-menu-link">{{author}}</a>
        </li>
      </ul>
    </div>
    <BookList :books="books" />
  </div>
</template>

<script>
import BookList from "../components/BookList.vue";
export default {
  name: "Browse",
  components: {
    BookList
  },
  data() {
    return {
      author: ""
    };
  },
  computed: {
    books() {
      return this.$root.$data.books.filter(
        book => book.author === this.author
      );
    },
    authors() {
      let list = []
      this.$root.$data.books.forEach(function(element) {
        if (!list.includes(element.author)) {
          list.push(element.author)
        }
      });
      list.sort()
      return list
    }
  },
  methods: {
    select(author) {
      this.author = author;
    }
  }
};
</script>