<template>
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
</template>

<script>
export default {
  name: 'CustomPagination',
}
</script>

<style lang="scss" scoped>
</style>