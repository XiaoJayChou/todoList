<template>
  <div id="app">
   <MyHeader @search="search" @addTodoObj="addTodoObj"></MyHeader>
   <MyList :todolist="fillList"></MyList>
   <MyFooter @checkAll="checkAll" :todolist="todolist"></MyFooter>
  </div>
</template>

<script>
import MyHeader from './components/MyHeader.vue'
import MyFooter from './components/MyFooter.vue'
import MyList from './components/MyList.vue'
export default {
  name: 'App',
  components: {
    MyHeader,
    MyFooter,
    MyList
  },
  data() {
    return {
      todolist: [
          {id:'001',name:'吃饭',done:true},
          {id:'002',name:'睡觉',done:true},
          {id:'003',name:'打豆豆',done:false}
        ],
        fillList:[]
    }
  },
  mounted(){
    console.log(this);
    this.$bus.$on('deleteObj',this.deleteObj)
    this.$bus.$on('handleChecked',this.handleChecked)
    this.$bus.$on('handleUpdate',this.handleUpdate)
  },
  methods: {
    search(kwd){
      this.fillList = this.todolist.filter(item =>{
        return item.name.indexOf(kwd) != -1
      })
    },
    handleUpdate(id,name){
      this.todolist.forEach(item => {
      if(item.id === id ) {
        item.name = name
      }
     })
    },
    checkAll(done){
      this.todolist.forEach(item =>{
        item.done = done
      })
    },
    handleChecked(todoObj){
     console.log(todoObj)
     this.todolist.forEach(item => {
      if(item.id === todoObj.id ) {
        item.done = !item.done
      }
     })
    },
    addTodoObj(todoObj) {
      this.todolist.unshift(todoObj)
    },
    deleteObj(id){
      this.todolist = this.todolist.filter(item =>{
        return item.id != id 
      })
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
