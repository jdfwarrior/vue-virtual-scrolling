<template>
  <tr :style="styles" :class="{odd: (row.index%2)>0}">
    <td>{{row.index}}</td>
    <td>{{row.first_name}} {{row.last_name}}</td>
  </tr>
</template>

<script>
export default {
  props: ["position", "row", "height"],
  data: function() {
    return {
      styles: {
        top: `${this.row.index * this.height}px`,
        height: `${this.height}px`
      }
    };
  }
};
</script>

<style>
tr {
  position: absolute;
  left: 0;
  width: 100%;
  border-top: 1px solid #e8e8e8;
  border-bottom: 1px solid #e8e8e8;
}

td {
  border: none !important;
}

.odd {
  background: #f8f8f8;
}
</style>
