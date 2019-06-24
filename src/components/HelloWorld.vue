<template>
  <div>
    <form action style="width: 300px; margin: 0 auto;">
      <input type="text" v-model="rowHeight" class="form-control">
    </form>
    <br>

    <div
      class="wrapper table table-bordered"
      :style="wrapperStyles"
      @scroll="scrolled"
      ref="wrapper"
    >
      <table :style="containerStyles">
        <tbody>
          <Item v-for="row in visible" :key="row.id" :row="row" :height="rowHeight"></Item>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import data from "../1000.json";
import Item from "./Item.vue";

export default {
  name: "HelloWorld",
  components: {
    Item
  },
  data: function() {
    return {
      rows: data,
      scrollTop: 0,
      height: 600,
      working: data.map((ele, i) => ({ ...ele, index: i })),
      rowHeight: 50
    };
  },
  methods: {
    scrolled() {
      const scrollTop = this.$refs.wrapper.scrollTop;
      this.scrollTop = scrollTop;
    }
  },
  computed: {
    visible: function() {
      const lookAhead = this.height / this.rowHeight + 10;
      const init = this.scrollTop / this.rowHeight;
      const leadingIndex = Math.floor(init);
      return this.working.slice(leadingIndex, leadingIndex + lookAhead);
    },
    containerStyles: function() {
      return {
        height: `${this.rows.length * this.rowHeight}px`
      };
    },
    wrapperStyles: function() {
      return {
        height: `${this.height}px`
      };
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.wrapper {
  width: 300px;
  overflow-y: scroll;
  margin: 0 auto;
}

table {
  overflow: hidden;
  position: relative;
  display: block;
}
</style>
