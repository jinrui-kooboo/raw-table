<template>
  <div class="raw-table">
    <table cellspacing="0" border="0" cellpadding="0">
      <!-- <div class="hidden-columns" ref="hiddenColumns">
        <slot></slot>
      </div> -->
      <thead>
        <tr>
          <th v-for="field in columns" :key="field.prop">{{ field.label }}</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(row, idx) in data" :key="idx">
          <td v-for="field in columns" :key="field.prop">
            <slot :$index="idx" :row="row">
              {{ row[field.prop] }}
            </slot>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "RawTable",
  props: {
    data: {
      type: Array,
      hiddenColumns: null,
      required: true,
      templates: null,
    },
  },
  mounted() {
    console.log(this);
  },
  computed: {
    columnNode() {
      return this.$slots.default.filter(
        (node) => node?.componentOptions?.tag === "raw-table-column"
      );
    },
    columns() {
      return this.columnNode.map((c) => ({ ...c.componentOptions?.propsData }));
    },
    // templates() {
    //   return [...this.$refs.hiddenColumns.childNodes];
    // },
  },
};
</script>

<style scoped lang="scss">
$borderColor: #c2c2c2;
.raw-table {
  width: 100%;
  overflow: hidden;
  border: 1px solid $borderColor;
  &:hover {
    overflow: overlay;
  }
  table {
    border-collapse: separate;
    width: 100%;
    .hidden-columns {
      display: none;
    }
    td,
    th {
      border-right: 1px solid $borderColor;
      border-bottom: 1px solid $borderColor;
      padding-left: 10px;
      padding-right: 10px;
      font-size: 12px;
      text-align: left;
      box-sizing: border-box;
    }
    thead {
      th {
        position: sticky;
        color: #606266;
        height: 40px;
        background-color: #fff;
        top: 0;
      }
    }
    tbody {
      td {
        color: #606266;
        padding-top: 8px;
        padding-bottom: 8px;
        line-height: 22px;
      }
      tr:nth-child(even) {
        background-color: #fafafa;
      }
    }
    th:first-child {
      z-index: 2;
    }
  }
}
</style>
