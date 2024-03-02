<template>
  <input
    min="0"
    type="number"
    @input="changeAmount($event.target.value)"
  /><br />
  <button @click="convert()">Convert</button>
  <button @click="favourite()" className="fav-button">Favourite</button>
</template>

<script>
export default {
  props: {
    changeAmount: {
      type: Function,
      required: true,
    },
    convert: {
      type: Function,
      required: true,
    },
    favourite: {
      type: Function,
      required: true,
    },
  },
};
</script>

<style scoped>
input {
  text-align: center;
  border-radius: 3px;
  border: 0;
  padding: 10px 15px;
  background: aliceblue;
  outline: none;
  position: relative;
  top: -50px;
  width: 300px;
  font-family: "Kode Mono", monospace;
}
button {
  position: relative;
  top: -20px;
  padding: 10px 20px;
  color: #fff;
  background-color: blueviolet;
  cursor: pointer;
  text-transform: uppercase;
  border: 0;
  border-radius: 5px;
  transition: transform 500ms ease;
}
button:hover {
  transform: scale(1.1) translateY(-5px);
}

button.fav-button {
  margin-left: 20px;
}
</style>
