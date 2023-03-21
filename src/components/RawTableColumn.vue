<script>
export default {
  name: "RawTableColumn",
  inject: ["pushColumn"],
  render(h) {
    return h("div", this.$slots.default);
  },
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
    console.log(this);
    let item = {
      prop: this.prop,
      label: this.label,
    };
    item.renderCell = (rowData) => {
      let children = null;
      if (this.$scopedSlots.default) {
        children = this.$scopedSlots.default(rowData);
      } else {
        const { row, column } = rowData;
        children = row[column.prop];
      }
      return <div>{children}</div>;
    };
    this.pushColumn(item);
  },
};
</script>
