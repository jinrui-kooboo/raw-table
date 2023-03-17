<template>
  <div id="app">
    <raw-table :data="data">
      <raw-table-column prop="name" label="Name"></raw-table-column>
      <raw-table-column prop="age" label="Age">
        <template #default="scope">{{ scope }}</template>
      </raw-table-column>
    </raw-table>
  </div>
</template>

<script>
import RawTable from "./components/RawTable.vue";
import RawTableColumn from "./components/RawTableColumn.vue";

export default {
  name: "App",
  data() {
    return {
      data: [
        {
          name: "Kangkang",
          age: 18,
        },
        {
          name: "Michael",
          age: 17,
        },
      ],
    };
  },
  components: {
    RawTable,
    RawTableColumn,
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
