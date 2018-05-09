<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <input type="text" v-model="newItem" @keyup.enter="addNew">
    <ul>
      <li v-for="item in items" v-bind:class="{finished: item.isFinished}" v-on:click="toggleFinish(item)">
        {{ item.label }}
      </li>
    </ul>
  </div>
</template>

<script>
import Store from '../store'
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'vue demo1',
      items: Store.fetch(),
      liClass: 'thisisLiClass',
      newItem: ''
    }
  },
  watch: {
    items: {
      handler: function(items){
        Store.save(items);
      },
      deep: true
    }
  },
  methods: {
    toggleFinish: function(item){
      item.isFinished = !item.isFinished
    },
    addNew: function(){
      this.items.push({
        label: this.newItem,
        isFinished: true
      })
      this.newItem = ''
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.finished{
  text-decoration: underline;
}
h1, h2 {
  font-weight: normal;
}
</style>
