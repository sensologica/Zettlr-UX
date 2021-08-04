<template>
  <div class="table-generator">
    <!-- Display a 12x12 grid -->
    <div
      v-for="row in 12"
      v-bind:key="row"
      class="row"
    >
      <div
        v-for="col in 12"
        v-bind:key="col"
        v-bind:class="{
          'cell': true,
          'active': intermediaryTableSize.rows >= row && intermediaryTableSize.cols >= col
        }"
        v-on:mouseover="setIntermediarySize(row, col)"
        v-on:click="handleClick()"
      ></div>
    </div>
  </div>
</template>

<script>
/**
 * @ignore
 * BEGIN HEADER
 *
 * Contains:        Table Popover
 * CVM-Role:        View
 * Maintainer:      Hendrik Erz
 * License:         GNU GPL v3
 *
 * Description:     A popover which allows you to select a number of rows and
 *                  columns to create a new table.
 *
 * END HEADER
 */
export default {
  name: 'PopoverTable',
  components: {
  },
  data: function () {
    return {
      tableSize: undefined,
      intermediaryTableSize: {
        rows: 0,
        cols: 0
      }
    }
  },
  computed: {
    popoverData: function () {
      return {
        tableSize: this.tableSize
      }
    }
  },
  methods: {
    handleClick: function () {
      // Write the intermediary size into our returned variable to result in a
      // table being generated.
      this.tableSize = this.intermediaryTableSize
    },
    setIntermediarySize: function (row, col) {
      this.intermediaryTableSize = {
        rows: row,
        cols: col
      }
    }
  }
}
</script>

<style lang="less">
body {
  .table-generator {
    padding: 5px;
  }

  .table-generator .row .cell {
    background-color: rgb(200, 200, 200);
    border: 1px solid rgb(80, 80, 80);
    width: 10px;
    height: 10px;
    margin: 1px;

    &.active {
      background-color: rgb(230, 230, 230);
    }
  }
}
</style>