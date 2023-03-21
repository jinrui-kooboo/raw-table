<script>
export default {
  name: "RawTableColumn",
  inject: ["pushColumn"],
  props: {
    prop: {
      type: String,
      required: true,
    },
    label: {
      type: String,
      required: true,
    },
  },
  created() {
    let item = {
      prop: this.prop,
      label: this.label,
    };
    item.renderCell = (h, rowData) => {
      let children = null;
      if (this.$slots.default) {
        children = this.$slots.default(rowData);
      } else {
        const { row, column } = rowData;
        children = row[column.prop];
      }
      return h("div", children);
    };
    this.pushColumn(item);
  },
  render(h) {
    return h("div", this.$slots.default);
  },
};
</script>
