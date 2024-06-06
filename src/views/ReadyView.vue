<template>
  <section class="container progress">
    <transition-group name="anim_todo">
      <todoGotovo v-for="(el, index) in this.$store.state.gotovo" :key="el" 
      :tasks = "el.tasks"
      :index = "index"
      @back = "back"
      @clear = "clear"
      @clear_all = "clear_all"
      />
    </transition-group>
  </section>
</template>

<script>
import todoGotovo from "../components/todoGotovo.vue";

export default {
  name: 'HomeView',
  components: {
    todoGotovo
  },
  methods: {
    back(index){
      this.$store.state.gotovo[index].tasks.forEach(element=> {
        element.check = !element.check
      })
      //console.log(this.$store.state.gotovo);
      this.$store.state.progress.push(this.$store.state.gotovo[index]);
      this.$store.state.gotovo.splice(index, 1);
      localStorage.setItem('gotovo', JSON.stringify(this.$store.state.gotovo));
      localStorage.setItem('progress', JSON.stringify(this.$store.state.progress));
    },
    clear(obj){
      this.$store.state.gotovo[obj.index].tasks.splice(obj.i, 1);
      if(this.$store.state.gotovo[obj.index].tasks.length == 0){
        this.$store.state.gotovo.splice(obj.index, 1);
      }
      localStorage.setItem('gotovo', JSON.stringify(this.$store.state.gotovo));
    },
    clear_all(index){
      this.$store.state.gotovo.splice(index, 1);
      localStorage.setItem('gotovo', JSON.stringify(this.$store.state.gotovo));
    },
  },
  computed: {
  },
}
</script>