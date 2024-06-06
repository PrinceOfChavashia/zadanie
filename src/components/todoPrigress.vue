<template>
    <div class="todo">
      <!-- <p class="black">{{ tasks }}</p> -->
        <div class="item" v-for="(el, i) in tasks" :key="el">
          <div class="checkbox-rect">
            <div class="byfer">
              <input v-on:click="$emit('check', {i, index})" type="checkbox" :id="index+'_'+i" name="check">
              <label :for="index+'_'+i"></label>
              <!-- <textarea v-model="el.task" contenteditable rows="1" cols="15" autocorrect="off">
              </textarea> -->
              <input v-model="el.task" type="text" autocomplete="off">
            </div> 
            <button class="clear" @click="$emit('clear', {i, index})">
              <svg width="15.000000" height="15.001953" viewBox="0 0 15 15.002" fill="none" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
                <defs/>
                <rect id="Прямоугольник 2" x="0.798828" y="0.091797" rx="0.502092" width="20.083683" height="1.004184" transform="rotate(45 0.798828 0.091797)" fill="#FFFFFF" fill-opacity="1.000000"/>
                <rect id="Прямоугольник 2" y="14.199219" rx="0.563873" width="20.083683" height="1.127746" transform="rotate(-45 0.000000 14.199219)" fill="#FFFFFF" fill-opacity="1.000000"/>
              </svg>
            </button>
          </div>
        </div>
        <div class="todo_foot">
          <div class="todo_foot_left">
            <div class="checkbox-rect">
              <div class="byfer">
                <input v-on:click="$emit('check_all', index)" type="checkbox" :id="index+'_'+i" name="check">
                <label :for="index+'_'+i"></label>
              </div> 
            </div>
            <input v-model="this.$store.state.new_task_mas[index].new_task" type="text" autocomplete="off" placeholder="+ Добавить элемент" v-on:keyup.enter="$emit('add_task', index)" >
          </div>
          <button class="clear" @click="$emit('clear_all', index)">
            <svg width="15.000000" height="15.001953" viewBox="0 0 15 15.002" fill="none" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
                <defs/>
                <rect id="Прямоугольник 2" x="0.798828" y="0.091797" rx="0.502092" width="20.083683" height="1.004184" transform="rotate(45 0.798828 0.091797)" fill="#FFFFFF" fill-opacity="1.000000"/>
                <rect id="Прямоугольник 2" y="14.199219" rx="0.563873" width="20.083683" height="1.127746" transform="rotate(-45 0.000000 14.199219)" fill="#FFFFFF" fill-opacity="1.000000"/>
            </svg>
          </button>
        </div>
        <!-- <p class="black">{{ this.$store.state.new_task_mas[index].new_task }}</p> -->
    </div>
</template>

<script>
    export default {
        data(){
          return{
            //new_tasksssss:"",
          }
        },
        props:
        {
            tasks:
            {
              type: Array
            },
            // new_task:{
            //     type: String,
            //     default:"NONE"
            // },
            index:{
              type: Int32Array,
              default: 0
            },
        },
        methods:{
            Enter(){
              //console.log(this.$store.state.new_task_mas[this.props.index].new_task);
            }
        }
    }
</script>

<style lang="scss">
    // .black{
    //   color: #000;
    // }
    .todo{
      width: 300px;
      background: #A64574;
      padding: 5px;
      border-radius: 5px;
    }
    .item {
      margin-bottom: 10px;
    }
    /* checkbox-rect */
    .checkbox-rect{
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    .checkbox-rect .byfer{
      display: flex;
    }
    .checkbox-rect .byfer input[type="checkbox"] {display: none;}
    .checkbox-rect .byfer input[type="checkbox"] + label {
      display: block;
      position: relative;
      padding-left: 25px;
      margin-bottom: 20px;
      cursor: pointer;
      -webkit-user-select: none;
      -moz-user-select: none;
      -ms-user-select: none;
    }
    // .checkbox-rect input[type="checkbox"]:hover + label:hover {
    //   color: rgb(23, 86, 228);
    // }
    .checkbox-rect .byfer input[type="checkbox"]:hover + label:before {
      background: #81A645;
      box-shadow: inset 0px 0px 0px 2px #fff;
    }
    .checkbox-rect .byfer input[type="checkbox"] + label:last-child {margin-bottom: 0;}
    .checkbox-rect .byfer input[type="checkbox"] + label:before {
      content: "";
      display: block;
      width: 1.4em;
      height: 1.4em;
      border: 1px solid #81A645;
      border-radius: 0.2em;
      position: absolute;
      left: 0;
      top: 0;
      -webkit-transition: all 0.2s, background 0.2s ease-in-out;
      transition: all 0.2s, background 0.2s ease-in-out;
      background: #fff;
    }
    .checkbox-rect .byfer input[type="checkbox"]:checked + label:before {
      width: 1.3em;
      height: 1.3em;
      border-radius: 0.2em;
      border: 2px solid #fff;
      -webkit-transform: rotate(90deg);
      transform: rotate(90deg);
      background: #81A645;
      box-shadow: 0 0 0 1px #81A645;
    }
    /* checkbox-rect end */
    input[type="text"]{
      background: #A64574;
      color: #fff;
    }
    ::-webkit-input-placeholder {
      color:#fff;
      margin: auto;
    }
    .clear{
      background-color: #A64574;
    }
    .clear:hover svg rect{
      fill: #d794b4;
    }
    .clear:active svg rect{
      fill: #81A645;
    } 
    textarea{
      width: 100px;
    }
    .todo_foot{
      display: flex;
      justify-content: space-between;
      align-items: center;

      .todo_foot_left{
        display: flex;

        .checkbox-rect{
          margin-top: -20px;
        }
      }
    }
</style>