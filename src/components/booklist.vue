<template>
  <div>
    <div class="flexSearch">
      <input type="text" placeholder="Search books" class="searchBar" v-model="search" />
    </div>
    <div class="flexBooks">
      <app-book v-for="(book, i) in filteredBooks" v-bind:book="book" v-bind:key="`book-${i}`"></app-book>
    </div>
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
      books: [],
      search: ""
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
  computed: {
    filteredBooks: function() {
      return this.books.filter(book => {
        return (
          book.title.includes(this.search) ||
          book.description.includes(this.search)
        );
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

.flexSearch {
  /*display: flex;
  flex-direction: row;
  justify-content: flex-end;
  align-items: baseline;
  margin-bottom: 50px;
  margin-right: 10%;*/
  position: absolute;
  top: 140px;
  right: 15%;
}

.searchBar {
  border-color: black;
  border-width: 3px;
  height: 40px;
  font-size: 30px;
}
</style>