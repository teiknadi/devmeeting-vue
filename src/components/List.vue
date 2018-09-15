<template>
<div>
    <ul>
        <li v-for="(p, key) in products" v-bind:key="key">
            {{ p.name }}
            <button v-on:click="removeItem(key)">REMOVE</button>
        </li>
    </ul>
    <form @submit.prevent="onSubmit()">
        <input
            type="text"
            name="newItem"
            v-model="newItem"
            v-validate="'required|min:3'"
            placeholder="Enter a new list postion"
        />
        <button v-on:click="onSubmit">ADD</button>

        <div v-show="errors.has('newItem')">
            {{ errors.first('newItem') }}
        </div>
    </form>
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
    onSubmit() {
        this.$validator.validateAll().then(result => {
            if (!result) {
                return;
            }

            const id = uuid();

            this.products.push({
                id,
                name: this.newItem
            });

            this.newItem = '';
            this.$validator.reset();
        });
    },
    removeItem(key) {
      Vue.delete(this.products, key);
    }
  },
};
</script>

<style>
ul {list-style: none}
</style>