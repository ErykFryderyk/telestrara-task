<template>
  <div class="search-banner">
    <h1 class="search-banner__title">Rick and Morty API</h1>
    <form class="search-form" @submit.prevent="$emit('show-value', inputValue, selectValue)">
      <div class="">
        <input class="search-input" v-model="inputValue" placeholder="Search character" />
        <button class="submit-btn">Search</button>
      </div>
      <select class="search-filter" name="filter" v-model="selectValue">
        <option value="alive">Alive</option>
        <option value="dead">Dead</option>
        <option value="unknow">Unknow</option>
      </select>
    </form>
  </div>
</template>

<script>
export default {
  name: 'SearchBanner',
  data() {
    return {
      inputValue: '',
      selectValue: '',
    }
  }
}
</script>

<style scoped>
.search-banner {
  background-color: black;
  width: 100%;
  height: 300px;
  background-image: url('../assets/rick-and-morty-run-the-jewels-vector-graphics-wallpaper-preview.jpeg');
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  margin-bottom: 70px;
}

.search-banner__title {
  font-size: 36px;
  color: #fcfcfc;
  margin-bottom: 10px;
  font-family: 'Roboto', sans-serif;
}
.search-form{
  display: flex;
  flex-direction: column;
}

.search-input {
  width: 200px;
  height: 40px;
  border: 1px solid #9a9a9a;
  border-right: none;
  background-color: white;
  border-radius: 5px 0 0 5px;
  font-size: 18px;
  font-weight: 300;
  font-family: 'Roboto', sans-serif;
  letter-spacing: .2px;
  padding-left: 10px;
}

.submit-btn {
  width: 100px;
  height: 40px;
  border: 1px solid #9a9a9a;
  border-radius: 0 5px 5px 0;
  border-left: none;
  cursor: pointer;
  font-size: 18px;
  font-weight: 100;
  font-family: 'Roboto', sans-serif;
  background-color: #6cac6c;
  letter-spacing: .2px;
  color: #fff;
}

.search-filter{
  width: 300px;
  height: 40px;
  border: 1px solid #9a9a9a;
  border-right: none;
  background-color: white;
  border-radius: 5px;
  font-size: 18px;
  font-weight: 300;
  font-family: 'Roboto', sans-serif;
  letter-spacing: .2px;
  padding-left: 10px;
  margin-top: 10px;
}
</style>