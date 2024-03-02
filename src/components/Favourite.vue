<template>
  <h2>Favourite options</h2>
  <div @click="getFromFavs(index)" v-for="(el, index) in favs" :key="index">
    <span>{{ el.from }}</span>
    <span>{{ el.to }}</span>
  </div>
</template>
<script>
export default {
  props: {
    favs: {
      type: Array,
      required: true,
    },
    getFromFavs: {
      type: Function,
      required: true,
    },
  },
};
</script>
<style scoped>
h2 {
  color: white;
}
div {
  display: flex;
  justify-content: space-between;
  width: 350px;
  margin: 0 auto;
}

span {
  padding: 10px 15px;
  background: purple;
  color: white;
  transition: all 500ms ease;
}
span:hover {
  opacity: 0.7;
  transform: scale(1.1);
  cursor: pointer;
}
</style>
