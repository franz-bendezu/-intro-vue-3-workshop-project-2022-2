<template>
  <input
    v-model="valueSync"
    class="input"
    :class="inputClasses"
    :type="type"
    :placeholder="placeholder"
  />
</template>

<script>
export default {
  name: "BulmaInput",
  props: {
    placeholder: {
      type: String,
      required: false,
      default: () => undefined,
    },
    type: {
      type: String,
      required: false,
      default: () => undefined,
    },
    color: {
      type: String,
      required: false,
      default: () => "primary",
    },
    modelValue: {
      type: [Number, String],
    },
    errors: {
      type: Array,
    },
  },
  emits: ["update:modelValue", "update:errors"],
  computed: {
    valueSync: {
      get() {
        return this.modelValue;
      },
      set(value) {
        this.$emit("update:modelValue", value);
      },
    },
    currentErrores() {
      const errors = [];
      if (this.valueSync?.length > 10) {
        errors.push("Longitud inválida!");
      }
      return errors;
    },
  },
  methods: {
    inputClasses() {
      const colorClass = " is-" + this.color;
      return [colorClass];
    },
  },
  watch: {
    currentErrores(errors) {
      this.$emit("update:errors", errors);
    },
  },
};
</script>
