<template>
  <div>
   <div>
    <input type="checkbox" :checked="todoObj.done" @change="handleChecked(todoObj)">
    <span v-if="isChecked">{{todoObj.name}}</span>
    <input @blur="handleBlur(todoObj.id)" ref="updateIpt" v-else type="text" v-model="name"> <button @click="handleUpdate(todoObj)">编辑</button> <button @click="deleteObj(todoObj.id)">删除</button>
   </div>
  </div>
</template>

<script>
  export default {
    name:'MyItem',
    data() {
      return {
        name:'',
        isChecked:true
      }
    },
    props: {
      todoObj: {
        type: Object,
        default: () =>{}
      },
    },
    methods: {
      handleBlur(id){
        this.isChecked = true
        this.$bus.$emit('handleUpdate',id,this.name)
      },
      handleUpdate(todoObj){
        this.isChecked = false
        this.name = todoObj.name
        this.$nextTick(()=>{
          this.$refs.updateIpt.focus()
        })
      },
      handleChecked(todoObj){
        this.$bus.$emit('handleChecked',todoObj)
      },
      deleteObj(id){
        this.$bus.$emit('deleteObj',id)
      }
    },
  }
</script>

<style lang="scss" scoped>

</style>