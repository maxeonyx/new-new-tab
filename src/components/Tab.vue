<template>
    <div class=tab-content>
        <Bookmark v-for="item in items" :key="item.name" :content="item" />
    </div>
</template>

<script>
import Bookmark from "./Bookmark";

export default {
    props: ['content'],
    computed: {
        items() {
            if (!this.content) return [];
            if (!this.content.items) return [];

            return Object.keys(this.content.items).map((name, i) => ({ name, ...this.content.items[name] }));
        }
    },
    components: {
        Bookmark,
    },
}
</script>

<style>

</style>
