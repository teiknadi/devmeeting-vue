<template>
  <div>
      {{ itemName }}
      <button @click="removeItem(itemKey)">REMOVE</button>
  </div>
</template>

<script>
export default {
  name: 'ListItem',
  props: {
    itemName: String,
    itemKey: Number,
  },
  methods: {
    removeItem(itemKey) {
      this.$parent.removeItem(itemKey);
    },
  },
};
</script>
