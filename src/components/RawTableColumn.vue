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
    item.getTemplate = (rowData) => {
      let children = null;
      if (this.$scopedSlots.default) {
        // custom default template => VNode[]
        children = this.$scopedSlots.default(rowData);
      } else {
        // default slot result => text string
        const { row, column } = rowData;
        children = row[column.prop];
      }
      return children;
    };
    this.pushColumn(item);
  },
  render(h) {
    return h("div", this.$slots.default);
  },
};
</script>
