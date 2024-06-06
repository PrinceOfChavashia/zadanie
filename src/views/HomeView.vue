<template>
  <section class="container progress">
    <transition-group name="anim_todo">
      <todoPrigress v-for="(el, index) in this.$store.state.progress" :key="el" 
      :tasks = "el.tasks"
      :index = "index"
      @add_task="add_task"
      @clear="clear"
      @clear_all="clear_all"
      @check="check"
      @check_all="check_all"
      />
    </transition-group>
    <div class="todo_add" @click="todo_add()">
      <svg width="150.000000" height="150.000000" viewBox="0 0 150 150" fill="none" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
        <defs/>
        <circle id="Эллипс 1" cx="75.000000" cy="75.000000" r="75.000000" fill="#B784D2" fill-opacity="1.000000"/>
        <rect id="Прямоугольник 1" x="15.000000" y="73.000000" rx="2.500000" width="120.000000" height="5.000000" fill="#FFFFFF" fill-opacity="1.000000"/>
        <rect id="Прямоугольник 1" rx="2.500000" width="120.000000" height="5.000000" transform="matrix(0 1 1 0 73 15)" fill="#FFFFFF" fill-opacity="1.000000"/>
      </svg>
    </div>
  </section>
</template>

<script>
import todoPrigress from "../components/todoPrigress.vue";

export default {
  name: 'HomeView',
  components: {
    todoPrigress
  },
  // mounted() {
  //   if(typeof JSON.parse(localStorage.getItem('progress')) === !null){
  //     this.$store.state.progress = JSON.parse(localStorage.getItem('progress'));
  //   }
  //   if(typeof JSON.parse(localStorage.getItem('newtaskmas')) === !null){
  //     this.$store.state.new_task_mas = JSON.parse(localStorage.getItem('newtaskmas'));
  //   }
  //   console.log(this.$store.state.progress);
  //   console.log(this.$store.state.new_task_mas);
  //   //this.initialize();
  // },
  methods: {
    todo_add(){
      this.$store.state.progress.push({tasks:[]});
      this.$store.state.new_task_mas.push({new_task: ""});
      //console.log(this.$store.state.progress);
      //console.log(this.$store.state.new_task_mas);
    },
    add_task(index){
      let new_task = this.$store.state.new_task_mas[index].new_task;
      this.$store.state.progress[index].tasks.push({task: new_task, check: false});
      this.$store.state.new_task_mas[index].new_task="";
      //console.log(new_task);
      //console.log(this.$store.state.progress);
      localStorage.setItem('progress', JSON.stringify(this.$store.state.progress));
      localStorage.setItem('newtaskmas', JSON.stringify(this.$store.state.new_task_mas));
    },
    clear(obj){
      this.$store.state.progress[obj.index].tasks.splice(obj.i, 1);
      if(this.$store.state.progress[obj.index].tasks.length == 0){
        this.$store.state.progress.splice(obj.index, 1);
        this.$store.state.new_task_mas.splice(obj.index, 1);
      }
      localStorage.setItem('progress', JSON.stringify(this.$store.state.progress));
      localStorage.setItem('newtaskmas', JSON.stringify(this.$store.state.new_task_mas));
    },
    clear_all(index){
      this.$store.state.progress.splice(index, 1);
      this.$store.state.new_task_mas.splice(index, 1);
      localStorage.setItem('progress', JSON.stringify(this.$store.state.progress));
      localStorage.setItem('newtaskmas', JSON.stringify(this.$store.state.new_task_mas));
    },
    check(obj){
      this.$store.state.progress[obj.index].tasks[obj.i].check = !this.$store.state.progress[obj.index].tasks[obj.i].check;
      this.readiness(obj.index);  
      localStorage.setItem('progress', JSON.stringify(this.$store.state.progress));
      localStorage.setItem('newtaskmas', JSON.stringify(this.$store.state.new_task_mas));
    },
    check_all(index){
      this.$store.state.progress[index].tasks.forEach(element=> {
        if(!element.check){
          element.check = !element.check; 
        }
      })
      this.readiness(index);
      localStorage.setItem('progress', JSON.stringify(this.$store.state.progress));
      localStorage.setItem('newtaskmas', JSON.stringify(this.$store.state.new_task_mas));
    },
    readiness(index){
      let sum = 0;
      this.$store.state.progress[index].tasks.forEach(element=> {
        if(element.check){
          sum++;
        }
      })
      if(sum == this.$store.state.progress[index].tasks.length){
        this.$store.state.gotovo.push(this.$store.state.progress[index]);
        localStorage.setItem('gotovo', JSON.stringify(this.$store.state.gotovo));
        this.$store.state.progress.splice(index, 1);
        //console.log(this.$store.state.gotovo);
      }
    },
    // initialize(){
    //   if(typeof JSON.parse(localStorage.getItem('progress')) == "object"){
    //     this.$store.state.progress = JSON.parse(localStorage.getItem('progress'));
    //   }
    //   if(typeof JSON.parse(localStorage.getItem('newtaskmas')) == "object"){
    //     this.$store.state.new_task_mas = JSON.parse(localStorage.getItem('newtaskmas'));
    //   }
    //   //console.log(JSON.parse(localStorage.getItem('user')));
    // },
  },
}
</script>

<style lang="scss">
  .progress{
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
  }
  .todo_add{
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .anim_todo-enter-active, .anim_todo-leave-active {
    transition: all .5s ease;
  }
  .anim_todo-enter-from{
    opacity: 0;
  }
  .anim_todo-leave-to{
    transform: scale(0, 0);
  }

  // .anim_todo-enter-from .todo_add{
  //   opacity: 0;
  // }
  // .anim_todo-leave-to .todo_add{
  //   transform: scale(0, 0);
  // }
  // .anim_todo_add-enter-active, .anim_todo_add-leave-active {
  //   transition: all .5s ease;
  // }
</style>
