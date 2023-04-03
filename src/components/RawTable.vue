<script>
export default {
  name: "RawTable",
  provide() {
    return {
      pushColumn: this.pushColumn,
    };
  },

  props: {
    data: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      columns: [],
    };
  },
  created() {
    this.columns.length = 0;
  },
  methods: {
    pushColumn(column) {
      this.columns.push(column);
    },
  },
  render(h) {
    const thead = h("thead", [
      h(
        "tr",
        this.columns.map((column) => h("th", column.label))
      ),
    ]);
    const tbody = h(
      "tbody",
      this.data.map((row) =>
        h(
          "tr",
          this.columns.map((column) => {
            const data = {
              column: { ...column },
              row: row,
            };
            return h("td", column.getTemplate(data));
          })
        )
      )
    );
    return h("div", { class: "raw-table" }, [
      h("div", this.$slots.default),
      h(
        "table",
        {
          border: 0,
          cellspacing: 0,
          cellpadding: 0,
        },
        [thead, tbody]
      ),
    ]);
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
