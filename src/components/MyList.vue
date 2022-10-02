<template>
  <div>
    <Item :todoObj="todoObj" v-for=" todoObj in todolist" :key="todoObj.id"></Item>
  </div>
</template>

<script>
import Item from './Item.vue'
export default {
  name: 'MyList',
  components: {
    Item,
  },
  props: {
    todolist: {
      type: Array,
      default:()=>{} 
    },
  },
  // methods: {
  //   addTodoObj(todoObj) {
  //     this.todolist.unshift(todoObj)
  //   }
  // },
}
</script>

<style lang="scss" scoped>

</style>