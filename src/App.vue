<template>
  <div id="app">
    <MyTitle>Rick and Morty</MyTitle>
    <button @click="getData">Get Data</button>
    <main>
      <ul v-for="character in myCharacters" :key="character.id">
        <li>
          <span>{{ character.id }}</span>
          <h2>{{ character.name }}</h2>
          <p>{{ character.status }}</p>
          <p>{{ character.species }}</p>
          <p>{{ character.type }}</p>
          <p>{{ character.gender }}</p>
          <img :src="character.image" alt="">
          <span style="display:block;">{{ character.created }}</span>
        </li>
      </ul>
    </main>
  </div>
</template>

<script>
import MyTitle from './components/Mytitle.vue';

// eslint-disable-next-line no-unused-vars
import axios from "axios";

// eslint-disable-next-line no-unused-vars
const linkAPI = 'https://rickandmortyapi.com/api/character/';
export default {
  name: 'App',
  components: {
    MyTitle,
  },
  data() {
    return {
      greetings: 'Witam',
      myCharacters: [
        {
          id: 1,
          name: "Rick Sanchez",
          status: "Alive",
          species: "Human",
          type: "",
          gender: "Male",
          image: "http://picsum.photos/602/693/",
          created: "2017-11-04T18:48:46.250Z"
        }
      ]
    }
  },
  methods: {
    getData() {
      axios.get(linkAPI)
        .then(res => {
          console.log(res.data.results);
          this.myCharacters = res.data.results;
        })
        .catch(err => {
          console.log(err);
        })
    },
  },
}
</script>

<style>
:root {
  font-size: 16px;
}

*,
*::after,
*::before {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  outline: none;
  -webkit-tap-highlight-color: transparent;
}

li {
  margin-bottom: 50px;
  border: 1px solid #6cac6c;
  background-color: #6cac6c;
  color:#315759;
  box-shadow:0px 0px 12px 2px #6cac6c;
}


#app {}
</style>
