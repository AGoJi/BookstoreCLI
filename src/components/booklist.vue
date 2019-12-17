<template>
  <div>
    <img v-if="books.length==0" src="@/assets/loader.gif" alt="Loading..." class="loader" />
    <p
      v-else-if="filteredBooks.length==0"
      class="message"
    >SORRY, WE COULD'NT FIND ANY RESULTS MATCHING.</p>
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

.loader {
  position: absolute;
  left: 40%;
}

.message {
  font-size: 40px;
  font-weight: bold;
  margin-right: 8%;
  margin-left: 8%;
}
</style>