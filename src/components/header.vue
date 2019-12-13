<template>
  <div class="header">
    <img class="logo" src="~@/assets/UBSlogo.png" />
    <div class="flexSearch">
      <input type="text" placeholder="Search books" class="searchBar" />
      <!-- v-model="search" -->
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
.header {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
}

.flexSearch {
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.searchBar {
  border-color: black;
  border-width: 3px;
  height: 40px;
  font-size: 30px;
}

.logo {
  width: 250px;
  height: auto;
}
</style>