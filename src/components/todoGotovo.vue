<template>
    <div class="todo">
      <!-- <p class="black">{{ tasks }}</p> -->
      <div class="todo_foot first">
        <button class="clear" @click="$emit('back', index)">
            <svg width="19.000000" height="15.000000" viewBox="0 0 19 15" fill="none" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
                <defs/>
                <path id="Многоугольник 3" d="M1.5 8.36L9.75 13.12C10.41 13.51 11.25 13.03 11.25 12.26L11.25 2.73C11.25 1.96 10.41 1.48 9.75 1.87L1.5 6.63C0.83 7.01 0.83 7.98 1.5 8.36Z" fill="#FFFFFF" fill-opacity="1.000000" fill-rule="evenodd"/>
                <rect id="Прямоугольник 3" rx="1.000000" width="13.000000" height="2.000000" transform="matrix(1 0 0 -1 6 8.5)" fill="#FFFFFF" fill-opacity="1.000000"/>
            </svg>
        </button>
        <button class="clear" @click="$emit('clear_all', index)">
          <svg width="15.000000" height="15.001953" viewBox="0 0 15 15.002" fill="none" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
            <defs/>
            <rect id="Прямоугольник 2" x="0.798828" y="0.091797" rx="0.502092" width="20.083683" height="1.004184" transform="rotate(45 0.798828 0.091797)" fill="#FFFFFF" fill-opacity="1.000000"/>
            <rect id="Прямоугольник 2" y="14.199219" rx="0.563873" width="20.083683" height="1.127746" transform="rotate(-45 0.000000 14.199219)" fill="#FFFFFF" fill-opacity="1.000000"/>
          </svg>
        </button>
      </div>
      <div class="item" v-for="(el, i) in tasks" :key="el">
        <div class="checkbox-rect">
          <div class="byfer">
            <input v-model="el.task" type="text" autocomplete="off">
          </div> 
          <button class="clear" @click="$emit('clear', {index, i})">
            <svg width="15.000000" height="15.001953" viewBox="0 0 15 15.002" fill="none" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
              <defs/>
              <rect id="Прямоугольник 2" x="0.798828" y="0.091797" rx="0.502092" width="20.083683" height="1.004184" transform="rotate(45 0.798828 0.091797)" fill="#FFFFFF" fill-opacity="1.000000"/>
              <rect id="Прямоугольник 2" y="14.199219" rx="0.563873" width="20.083683" height="1.127746" transform="rotate(-45 0.000000 14.199219)" fill="#FFFFFF" fill-opacity="1.000000"/>
            </svg>
          </button>
        </div>
      </div>
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

      .todo_foot{
        margin-bottom: 10px;
      }
    }
    .item {
      margin-bottom: 10px;
    }
    .item:last-child{
      margin-bottom: 0;
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
    .clear:hover svg rect, .clear:hover svg path{
      fill: #d794b4;
    }
    .clear:active svg rect, .clear:active svg path{
      fill: #81A645;
    } 
    textarea{
      width: 100px;
    }
    .first{
      display: flex;
      justify-content: space-between;
    }
</style>