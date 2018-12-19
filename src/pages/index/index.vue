<template>
  <div class="container">
    <header>
      <input type="text" v-model="newwork" placeholder="待办事项" @confirm="addwork">
    </header>
    <section class="nonetodo">
      <h1>未完成事项</h1>
      <ul>
        <li v-if="!item.status" v-for="(item,index) of todolist" @click="addtodo(index)" :key="index">
          {{item.todo}}
        </li>
      </ul>
      <p v-if="isShow">未添加任何事项</p>
    </section>
    <section>
      <h1>已完成事项</h1>
      <ul>
        <li v-if="item.status" v-for="(item,index) of todolist" @click="addtodo(index)" :key="index">
          {{item.todo}}
        </li>
      </ul>
      <p v-if="isShow2">没有完成事项</p>
    </section>
  </div>
</template>

<script>
/* eslint-disable */
export default {
  data () {
    return {
      newwork: '',
      todolist:[]
    }
  },
  methods:{
    addtodo(index){
      this.todolist[index].status = !this.todolist[index].status;
    },
    addwork(){
      if (this.newwork){
        this.todolist.push({
            todo:this.newwork,
            status:false
        });
        this.newwork = '';
      }
    }
  },
  computed:{
    isShow(){
      for(let i of this.todolist){
        if(!i.status){
          return false;
        }
      }
      return true;
    },
    isShow2(){
      let n=0;
      for(let i of this.todolist){
        if(i.status){
          n++;
        }
      }
      if(n!=0){
        return false;
      }else{
        return true;
      }
    }
  }
}
</script>

<style scoped>
  header{
    width: 100%;
    background-color: skyblue;
    margin-bottom: .5rem;
    text-align: center;
  }
  header input{
    width: 80%;
    height: .8rem;
    line-height: .8rem;
    padding-left: .3rem;
    margin: .15rem .5rem;
    display: inline-block;
    border: 1px solid #fff;
  }
  section{
    margin: 0 .5rem .5rem .5rem;
  }
  section li{
    background-color: #f3f3f3;
    margin: .2rem 0;
    border-radius: 0.05rem;
    line-height: .8rem;
    padding-left: .6rem;
    color: #666;
    box-shadow: -0.1rem 0 0 0 rgba(0, 0, 255, 0.5);
  }
  section.nonetodo li{
    background-color: rgba(255, 0, 0, 0.2);
  }
  p{
    margin-top: .5rem;
    color: #f00;
  }
</style>
