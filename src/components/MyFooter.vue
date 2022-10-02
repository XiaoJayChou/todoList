<template>
  <div v-if="todolist.length">
    <input @change="checkAll"  type="checkbox" :checked="isAll"> 已完成{{completed}} / 全部{{todolist.length}}
  </div>
</template>

<script>
  export default {
    name:'MyFooter',
    props: {
      todolist: {
      type: Array,
      default:()=>{} 
    },
    },
    computed: {
      completed() {
        return this.todolist.reduce((pre,cur)=>{
            return pre + (cur.done ? 1 : 0)
        },0)
      },
      isAll(){
        return this.completed === this.todolist.length && this.todolist.length > 0
      }
    },
    methods: {
      checkAll(e) {
        console.log(e)
        this.$emit('checkAll',e.target.checked)
      }
    },
  }
</script>

<style lang="scss" scoped>

</style>