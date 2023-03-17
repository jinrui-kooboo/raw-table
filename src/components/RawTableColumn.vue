<template>
  <div>
    <slot v-bind="scope"></slot>
  </div>
</template>

<script>
export default {
  name: "RawTableColumn",
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
  },
  computed: {
    tableData() {
      return this.$vnode.context?.data ?? [];
    },
    index() {
      return this.$parent.$children
        .filter((c) => c.$options.name === "RawTableColumn")
        .indexOf(this);
    },
    scope() {
      return {
        $index: this.index,
        row: this.tableData[this.index],
      };
    },
  },
};
</script>
