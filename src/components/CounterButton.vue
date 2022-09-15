<template>
  <button @click="incrementCount" class="button" :class="buttonClasses">
    <slot name="icon"> </slot>
    <slot :count="count"> Incrementar ({{ count }}) </slot>
  </button>
</template>

<script>
export default {
  props: {
    color: {
      type: String,
      default: () => "primary",
      required: false,
    },
  },
  data: () => ({
    count: 0,
  }),
  methods: {
    incrementCount() {
      this.count++;
    },
  },
  computed: {
    buttonClasses() {
      const colorClass = "is-" + this.color;
      return [colorClass];
    },
  },
};
</script>
