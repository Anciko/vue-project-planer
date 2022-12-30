<template>
    <nav class="fileter-nav">
        <button @click="updateFilter('all')" :class="{active : this.current == 'all'}">All</button>
        <button @click="updateFilter('completed')" :class="{ active: this.current == 'completed' }">Completed</button>
        <button @click="updateFilter('ongoing')" :class="{ active: this.current == 'ongoing' }">Ongoing</button>
    </nav>
</template>

<script>
export default {
    props: ['current'],
    data() {
        return {

        }
    },
    methods: {
        updateFilter(by) {
            this.$emit('filter', by)
        }
    }
}
</script>

<style scoped>
button {
    border: none;
    background: none;
    padding: 8px 18px;
    border-radius: 5px;
}

.active {
    background: #F0F0F0;
}
</style>