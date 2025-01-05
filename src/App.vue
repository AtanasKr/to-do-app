<template>
  <div class="main-content">
    <SearchInput @addItems="addItems" />
    <div class="line-pos">
      <div class="line">
      </div>
    </div>
    <ItemList :itemsHolder="itemsHolder" @remove-item="handleRemoveItem" @edit-item="handleEditItem" />
  </div>
</template>

<script>
import ItemList from './components/ItemList.vue';
import SearchInput from './components/SearchInput.vue';

export default {
  name: 'App',
  components: {
    SearchInput,
    ItemList
  },
  data() {
    return {
      itemsHolder: [],
    }
  },
  created() {
    const savedItems = localStorage.getItem('itemsHolder');
    if (savedItems) {
      this.itemsHolder = JSON.parse(savedItems);
    }
  },
  methods: {
    addItems(data) {
      this.itemsHolder.push(data);
      this.saveToLocalStorage();
    },
    handleRemoveItem(index) {
      this.itemsHolder.splice(index, 1)
      this.saveToLocalStorage();
    },
    handleEditItem({ index, value }) {
      this.itemsHolder.splice(index, 1, value);
      this.saveToLocalStorage();
    },
    saveToLocalStorage() {
      localStorage.setItem('itemsHolder', JSON.stringify(this.itemsHolder));
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700&display=swap');

body {
  font-family: 'Inter';
  background-color: #C7FD7A;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.main-content {
  background-color: rgba(255, 255, 255, 0.5);
  height: 40em;
  width: 38em;
  border-radius: 20px;
}

.line-pos {
  padding-top: 1em;
  display: flex;
  justify-content: center;
}

.line {
  width: 35em;
  background-color: #C4DB42;
  height: 0.4em;
  border-radius: 20px;
}
</style>
