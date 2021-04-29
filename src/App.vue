<template>
  <div id="app">
    <div class="container">
      <section class="users">
        <article v-for="user in users" :key="user.id" class="user" @click="userClicked(user)">
          <h3>{{user.name}}</h3>
        </article>
      </section>
      <section class="events">
        <h1>{{showText ? showText : 'Klikni usera'}}</h1>
      </section>

    </div>
  </div>
</template>

<script>
import Axios from 'axios'
export default {
  name: 'App',
 data() {
   return {
     users: [],
     showText:''
   }
 },
  mounted () {
    this.getUsers();
  },
  methods:{
    async getUsers(){
      let res = await Axios.get('https://jsonblob.com/api/jsonBlob/https://jsonblob.com/5259b955-a8de-11eb-aa02-7be69287a894');
      let users = res.data.data;
      this.users = users;
    },
    userClicked(user){
      this.showText = user.name;
    }
  }
}
</script>

<style>
@import './assets/style.css';
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}

.container{
  max-width: 700px;
  background: whitesmoke;
  margin: 0 auto;
  display: flex;
  margin-top: 5rem;
}

.user{
  padding: .5rem;
  margin: 1rem;
  background: rgb(172, 172, 172);
  padding: 2rem;
  border-radius: 15px;
  box-shadow: 0 7px 10px -10px black;
  cursor: pointer;
}

.user:hover{
  background: rgb(158, 157, 157);
}

.events{
  background: darkcyan;
  width: 60%;
  margin-left: auto;
  color: white;
  display: grid;
  place-content: center;
}
</style>
