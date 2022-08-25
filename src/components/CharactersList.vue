<template>
  <div class="characters-list">
    <h1>Lista bohaterów</h1>
    <!-- <ul v-for="character in characters" :key="character.id">
      <li>
        <h1>character.id</h1>
      </li>
    </ul> -->
  </div>
</template>

<script>
export default {
  name: 'CharactersList.vue',
  data() {
    return {
      props: [
        'message',
      ]
    }
  },
}
</script>

<style land="scss">
.character-list {
  color: black;
  background-color: black;
}
</style>