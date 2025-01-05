<template>
    <div>
        <Item v-for="(item, index) in itemsHolder" :index="index" :item="item" @remove-item="handleRemoveItem"
            @edit-item="handleEditItem" />
    </div>
</template>

<script>
import Item from './Item.vue';
export default {
    props: {
        itemsHolder: {
            type: Array,
            required: false,
        }
    },
    data() {
        return {

        }
    },
    methods: {
        handleRemoveItem(index) {
            this.$emit('remove-item', index);
        },
        handleEditItem({ index, value }) {
            this.$emit('edit-item', { index, value })
        }
    },
    components: {
        Item,
    }
}
</script>

<style scoped>
div {
    margin-top: 1em;
    height: 28em;
    overflow-y: auto;
}

/* Hide the scrollbar */
div::-webkit-scrollbar {
    width: 0;
    /* Hides the vertical scrollbar */
    height: 0;
    /* Hides the horizontal scrollbar */
}

div::-webkit-scrollbar-thumb {
    background: transparent;
    /* Makes the scrollbar thumb transparent */
}

/* Firefox-specific rule to hide the scrollbar */
div {
    scrollbar-width: none;
    /* Firefox hides the scrollbar */
}
</style>