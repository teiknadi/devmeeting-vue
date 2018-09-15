<template>
<div>
    <ul>
        <li v-for="(p, key) in products" v-bind:key="key">
            {{ p.name }}
                <button v-on:click="removeItem(key)">REMOVE</button>
        </li>
    </ul>
    <input type="text" name="newItem" v-model="newItem" placeholder="Enter a new list postion" />
    <button v-on:click="addItem(newItem)">ADD</button>
</div>
</template>

<script>
import Vue from 'vue';
import uuid from 'uuid/v4';

export default {
  name: 'List',
  data() {
    return {
        newItem: '',
        products: [{
            id: 0,
            name: 'Coffee',
        }, {
            id: 1,
            name: 'Pizza',
        }],
    };
  },
  methods: {
    removeLast() {
      this.products.pop();
    },
    addItem(name) {
        if (!name) {
            return;
        }
        const id = uuid();

        this.products.push({
            id,
            name
        });

        this.newItem = ''
    },
    removeItem(key) {
      Vue.delete(this.products, key);
    }
  },
};
</script>
