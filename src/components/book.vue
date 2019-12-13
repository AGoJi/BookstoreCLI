<template>
  <div class="flip-card">
    <div class="flip-card-inner">
      <div class="flip-card-front">
        <img class="coverIMG" alt="Cover" v-bind:src="book.cover" />
      </div>
      <div class="flip-card-back">
        <h1 class="margin">{{ book.title }}</h1>
        <p class="margin">{{ book.description }}</p>
        <a data-fancybox="gallery" v-bind:href="book.detail">
          <button>More info</button>
        </a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["book"]
};
</script>

<style scoped>
.flip-card {
  background-color: transparent;
  width: 300px;
  height: 400px;
  perspective: 1000px;
}

.flip-card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.6s;
  transform-style: preserve-3d;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
}

.flip-card:hover .flip-card-inner {
  transform: rotateY(180deg);
}

.flip-card-front,
.flip-card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
}

.flip-card-front {
  background-color: #bbb;
}

.flip-card-back {
  background-color: rgb(158, 158, 158);
  transform: rotateY(180deg);
  border: solid;
  border-width: 3px;
}

.coverIMG {
  width: 300px;
  height: 400px;
  border: solid;
  border-width: 3px;
}

.margin {
  margin-right: 20px;
  margin-left: 20px;
}

button {
  background-color: rgb(102, 102, 102);
  border: solid;
  border-width: 1px;
  border-color: black;
  font-size: 15px;
}
</style>