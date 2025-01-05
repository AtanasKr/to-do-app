<template>
    <div class="main">
        <div class="left" v-if="!isEditing">{{ item }}</div>
        <div class="left" v-else>
            <input v-model="editedItem" @keyup.enter="saveEdit" @blur="saveEdit" />
        </div>
        <div class="right">
            <img v-if="!isEditing" :src="require('@/assets/Edit.png')" alt="edit-btn" @click="isEditing = !isEditing">
            <img v-if="isEditing" :src="require('@/assets/Edit.png')" alt="edit-btn" @click="saveItem">
            <img v-if="!isEditing" :src="require('@/assets/Delete.png')" alt="delete-btn" @click="removeItem">
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            isEditing: false,
            editedItem: this.item
        }
    },
    props: {
        item: {
            type: String,
            required: true
        },
        index: {
            type: Number,
            require: true
        }
    },
    methods: {
        removeItem() {
            this.$emit('remove-item', this.index)
        },
        saveItem() {
            if (this.editedItem.trim() !== '') {
                this.$emit('edit-item', { index: this.index, value: this.editedItem });
            }
            this.isEditing = false;
        }
    }

}
</script>

<style scoped>
.main {
    background-color: #C4DB42;
    margin-right: 2em;
    margin-left: 2em;
    padding-top: 1em;
    padding-bottom: 1em;
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-radius: 15px;
    max-height: 2.5em;
    box-shadow: 4px 4px 8px rgba(0, 0, 0, 0.2);
}

.left {
    margin-left: 1em;
    color: white;
    flex-grow: 1;
}

.right {
    display: flex;
    gap: 1em;
    margin-right: 1em;
}

img {
    height: 30px;
    width: 30px;
    cursor: pointer;
}

input {
    all: unset;
    background-color: rgb(94, 200, 94);
    border-radius: 20px;
    padding: 5px;
}
</style>