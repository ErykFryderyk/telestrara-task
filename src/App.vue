<template>
  <div id="app">
    <SearchBanner @show-value="getChracterByName" />
    <main>
      <ErrorMessage v-if='notFound' />
      <CharactersList />
      <div class="characters-list" v-if="!notFound">
        <ul class="characters-card-list">
          <li class="character-card" v-for="character in myCharacters" :key="character.id">
            <h2 class="character-card__title">{{ character.name }}</h2>
            <p class="character-card__value">
              <span class="character-card__label">Species:</span> {{ character.species }} - {{ character.gender }}
            </p>
            <p class="character-card__value">
              <span class="character-card__label">Status:</span> {{ character.status }}
            </p>
            <p class="character-card__value" v-if="character.type != ''">
              <span class="character-card__label">Type: </span> {{ character.type }}
            </p>
            <div class="">
              <img class="character-card__image" :src="character.image" alt="">
            </div>
            <p class="character-card__created">
              <span>Created:</span> {{ character.created }}
            </p>
          </li>
        </ul>
      </div>
      <div class="pagination">
        <ul class="pagination__items">
          <li class="pagination__item">
            <button class="pagination__btn" @click="getData">First page</button>
          </li>
          <li class="pagination__item">
            <button class="pagination__btn">Prev page</button>
          </li>
          <li class="pagination__item">
            <span class="pagination__current-page">{{ currentPage }}</span>
          </li>
          <li class="pagination__item">
            <button class="pagination__btn">Next page</button>
          </li>
          <li class="pagination__item">
            <button class="pagination__btn">Last page</button>
          </li>
          <!-- <p>Pages: <span>{{ lastPage }}</span></p> -->
        </ul>

      </div>
    </main>
  </div>
</template>

<script>
import SearchBanner from './components/SearchBanner.vue';
import ErrorMessage from './components/ErrorMessage.vue';
import CharactersList from './components/CharactersList.vue';

// eslint-disable-next-line no-unused-vars
import axios from "axios";
// eslint-disable-next-line no-unused-vars
const linkAPI = 'https://rickandmortyapi.com/api/character/';

export default {
  name: 'App',
  components: {
    SearchBanner,
    ErrorMessage,
    CharactersList
  },
  data() {
    return {
      notFound: false,
      currentPage: 1,
      lastPage: null,
      info: [
        // -------- example object
        // {
        //   count: 826,
        //   pages: 42,
        //   next: "https://rickandmortyapi.com/api/character/?page=2",
        //   prev: null
        // }
      ],
      myCharacters: [
        {
          // ------- example object
          // id: 1,
          // name: "Rick Sanchez",
          // status: "Alive",
          // species: "Human",
          // type: "",
          // gender: "Male",
          // image: "https://rickandmortyapi.com/api/character/avatar/1.jpeg",
          // created: "2017-11-04T18:48:46.250Z"
        }
      ]
    }
  },
  methods: {
    getData() {
      axios.get(linkAPI)
        .then(res => {
          this.notFound = false;
          this.myCharacters = res.data.results;
          this.info = res.info;
        })
        .catch(err => {
          this.notFound = true;
          console.log(err);
        })
    },
    getChracterByName(name, filter) {
      axios.get(`${linkAPI}?name=${name}&status=${filter}`)
        .then(res => {
          this.notFound = false;
          this.myCharacters = res.data.results;
          this.lastPage = res.data.info.pages;
        })
        .catch(err => {
          this.notFound = true;
          console.log(err);
        })
    },
  },
  mounted() {
    this.getData();
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@100;300;500;700&display=swap');

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

img {
  width: 100%;
}

li {
  list-style: none;
}

#app {
  color: white;
  font-family: 'Roboto', sans-serif;
}

main {
  padding: 0 15px;
}

.character-list {
  width: 100%;
  margin-bottom: 50px;
}

.characters-card-list {
  width: 100%;
  display: flex;
  flex-direction: column;
}

.character-card {
  border: 1px solid black;
  background-color: #f0ffff;
  color: #414141;
  padding: 5px 10px;
  border-radius: 5px;
  margin-bottom: 20px;
  position: relative;
}

.character-card__title {
  font-size: 30px;
  margin-bottom: 5px;
}

.character-card__value {
  font-size: 18px;
  margin-bottom: 2px;
}

.character-card__created {
  font-size: 12px;
  font-weight: 300;
  position: absolute;
  bottom: 2px;
}

.character-card__label {
  font-size: 14px;
  font-weight: 400;
}

.character-card__image {
  border-radius: 2.5px;
  margin-bottom: 10px;
}

.pagination {
  width: 100%;
  margin-bottom: 50px;
}

.pagination__items {
  display: flex;
  justify-content: center;
  align-items: center;
}

.pagination__item {
  border: 1px solid #e3e3e3;
  padding: 7px;
  border-radius: 2.5px;
  margin: 0 1px;
}

.pagination__btn {
  background: none;
  border: none;
  cursor: pointer;
}

.pagination__current-page {
  font-weight: bold;
  font-size: 16px;
  color: #868686;
}

@media (min-width: 560px) {
  .characters-card-list {
    display: flex;
    justify-content: space-around;
    flex-wrap: wrap;
    flex-direction: row;
  }

  .character-card {
    width: 250px;
  }
}

@media (min-width: 768px) {
  main {
    width: 750px;
    margin: 0 auto;
  }

  .character-card {
    width: 300px;
  }
}

@media (min-width: 1024px) {
  main {
    width: 1000px;
  }
}

@media (min-width: 1324px) {
  main {
    width: 1300px;
  }
}
</style>