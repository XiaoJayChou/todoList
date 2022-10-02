<template>
  <div>
    <input type="text" v-model="keyword" placeholder="请输入。。。" @keyup.enter="enter"> 
    <input type="text" v-model="searchKwd" placeholder="请输入查询字段。。。"> <button>查询</button>
  </div>
</template>

<script>
  
  export default {
    name:'MyHeader',
    data() {
      return {
        keyword: '',
        searchKwd:''
      }
    },
    props: {
      todolist: {
      type: Array,
      default:()=>{} 
    },
    },
    watch: {
      searchKwd:{
        immediate:true,
        handler(val){
          this.$emit('search',val)
          console.log(val)
        }
      }
    },
    methods: {
      // search(){
      //   this.$emit('search',this.searchKwd)
      // },
      enter() {
        if(this.keyword.trim() === '') return alert('不能为空！！！')
        const todoObj = {id:Date.now(),name:this.keyword,done:false}
        this.$emit('addTodoObj',todoObj)
        this.keyword = ''
      }
    },
  }
</script>

<style lang="scss" scoped>

</style>