<template>
    <div class="content">
        <div class="search">
            <input type="text" placeholder="Add new item..." v-model="newItem">
        </div>
        <img :src="require('@/assets/Add.png')" alt="add-btn" style="height: 55px; width: 55px;" @click="addDataToList">
    </div>
</template>

<script>
export default {
    data() {
        return {
            newItem: '',
        }
    },
    methods: {
        addDataToList() {
            if (this.newItem.trim() !== '') {
                this.$emit('addItems', this.newItem)
            }
        }
    }

}
</script>

<style scoped>
.content {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 4em;
    padding-top: 2em;
}

.search {
    background-color: rgba(68, 151, 107, 0.6);
    border-radius: 10px;
    width: 25em;
    height: 3em;
    box-shadow: 4px 4px 8px rgba(0, 0, 0, 0.2);
    display: flex;
}

input {
    all: unset;
    color: white;
    padding-left: 1em;
}

input::placeholder {
    color: white;
}

img {
    cursor: pointer;
}

img:hover {
    opacity: 70%;
}
</style>