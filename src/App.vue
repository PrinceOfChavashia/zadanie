<template>
  <section class="container">
    <nav>
      <router-link to="/">Home</router-link>
      <router-link to="/ready">Ready</router-link>
    </nav>
  </section>
  <router-view/>
</template>

<script>

export default {
  name: 'HomeView',
  mounted() {
    if(JSON.parse(localStorage.getItem('progress')) !== null){
      this.$store.state.progress = JSON.parse(localStorage.getItem('progress'));
    }
    if(JSON.parse(localStorage.getItem('newtaskmas')) !== null){
      this.$store.state.new_task_mas = JSON.parse(localStorage.getItem('newtaskmas'));
    }
    if(JSON.parse(localStorage.getItem('gotovo')) !== null){
      this.$store.state.gotovo = JSON.parse(localStorage.getItem('gotovo'));
    }
  },
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Nunito:ital,wght@0,200..1000;1,200..1000&display=swap');
/*Обнуление*/
*{
	padding: 0;
	margin: 0;
	border: 0;
}
*,*:before,*:after{
	-moz-box-sizing: border-box;
	-webkit-box-sizing: border-box;
	box-sizing: border-box;
}
:focus,:active{outline: none;}
a:focus,a:active{outline: none;}
nav,footer,header,aside{display: block;}
html,body{
	height: 100%;
	width: 100%;
	font-size: 100%;
	line-height: 1;
	font-size: 14px;
	-ms-text-size-adjust: 100%;
	-moz-text-size-adjust: 100%;
	-webkit-text-size-adjust: 100%;
}
input,button,textarea{font-family:inherit;}
input::-ms-clear{display: none;}
button{cursor: pointer;}
button::-moz-focus-inner {padding:0;border:0;}
a, a:visited{text-decoration: none;}
a:hover{text-decoration: none;}
ul li{list-style: none;}
img{vertical-align: top;}
h1,h2,h3,h4,h5,h6{font-size:inherit;font-weight: 400;}
/*--------------------*/
#app{
  font-family: Nunito;
}

.container{
  margin: auto;
  margin-top: 40px;
  width: 90%;
}
nav{
  color: #81A645;
  display: flex;
  justify-content: center;
  gap: 20px;
  font-size: 32px;
  a:visited{
    color: #81A645;
  }
  a:hover{
    color: #A64574;
  }
  a:active{
    color: #FFD4E9;
  }
}
</style>
