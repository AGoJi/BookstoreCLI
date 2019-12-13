<template>
  <div class="flexBooks">
    <app-book v-for="(book, i) in books" v-bind:book="book" v-bind:key="`book-${i}`"></app-book>
  </div>
</template>

<script>
import Book from "./book.vue";
export default {
  components: {
    "app-book": Book
  },
  data() {
    return {
      books: []
    };
  },
  methods: {
    getData() {
      fetch("https://api.myjson.com/bins/zyv02", {
        method: "GET"
      })
        .then(response => {
          if (response.ok) {
            return response.json();
          }
          throw new Error(response.statusText);
        })
        .then(json => {
          this.books = json.books;
        })
        .catch(error => {
          console.log("Request failed: " + error.message);
        });
    }
  },
  created() {
    this.getData();
  }
};
</script>

<style scoped>
.flexBooks {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
}
</style>