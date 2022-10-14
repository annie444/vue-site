<template>
  <div id="tiles" @resize="createGrid()"></div>
</template>

<script>
import anime from "animejs";

export default {
  name: "home",
  data() {
    return {
      columns: 0,
      rows: 0,
      count: -1,
      colors: [
        "rgb(229, 57, 53)",
        "rgb(253, 216, 53)",
        "rgb(244, 81, 30)",
        "rgb(76, 175, 80)",
        "rgb(33, 150, 243)",
        "rgb(156, 39, 176)"
      ]
    };
  },
  methods: {
    animateClick(index) {
      count = count + 1;

      anime({
        targets: ".tile",
        backgroundColor: colors[ count % (colors.length - 1)],
        delay: anime.stagger(50, {
          grid: [columns, rows],
          from: index
        })
      });
    },
    createTile(index) {
      const tile = document.createElement("div");
      tile.classList.add("tile");
      tile.onClick = (e) => animateClick(index);
      return tile;
    },
    createTiles(quantity) {
      Array.from(Array(quantity)).map((tile, index) => {
        this.appendChild(createTile(index));
      })
    },
    createGrid() {
      this.innerHTML = "";

      let columns = Math.floor(document.body.clientWidth / 50);
      let rows = Math.floor(document.body.clientHeight / 50);

      this.style.setProperty("--columns", columns);
      this.style.setProperty("--rows", rows);

      createTiles(columns * rows);
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
</style>
