<template>
  <div id="tiles">
    <div class="tile" @resize="reloadGrid()" @click="animateClick()"></div>
  </div>
</template>

<script>
import { isExpressionWrapper } from '@babel/types';
import anime from 'animejs';

export default {
  name: "home",
  data() {
    return {

    }
  },
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

      wrapper.style.setProperty("--columns", columns);
      wrapper.style.setProperty("--rows", rows);

      createTiles(columns * rows);
    },
    animateClick() {
      const count = count + 1

      anime({
        targets: ".tile",
        backgroundColor: colors[ count % (colors.length - 1)]
      })
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

    grid-template-rows: repeat(var(--rows), 1fr);
    grid-template-columns: repeat(var(--columns), 1fr);
  }

  .tile {
    outline: 1px solid white;
  }
</style>
