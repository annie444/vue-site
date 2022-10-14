<template>
  <div id="tiles">
    <div class="tile" @resize="createGrid()"></div>
  </div>
</template>

<script>
import { isExpressionWrapper } from '@babel/types';

export default {
  name: "home",
  props: {
    methods: {
      createGrid() {
        const createTile = index => {
          const tile = document.createElement("div");
          tile.classList.add("tile");
          return tile;
        }

        const createTiles = quantity => {
          Array.from(Array(quantity)).map((tile, index) => {
            wrapper.appendChild(createTile(index));
          })
        }

        wrapper.innerHTML = "";

        let columns = Math.floor(document.body.clientWidth / 50);
        let rows = Math.floor(document.body.clientHeight / 50);

        createTiles(columns * rows);
      },
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  #tiles{
    height: 100vh;
    width: 100vh;

    display: grid;
  }

  .tile {
    outline: 1px solid white;
  }
</style>
