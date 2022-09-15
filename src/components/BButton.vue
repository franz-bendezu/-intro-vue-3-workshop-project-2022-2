<template>
  <button class="button" :type="type" :class="buttonClasses">
    <slot name="icon"> </slot>
    <slot :count="count"> </slot>
  </button>
</template>

<script>
export default {
  props: {
    color: {
      type: String,
      default: () => "primary",
    },
    type: {
      type: String,
      default: () => "button",
    },
  },
  data: () => ({
    count: 0,
  }),
  computed: {
    buttonClasses() {
      const colorClass = "is-" + this.color;
      return [colorClass];
    },
  },
};
</script>
