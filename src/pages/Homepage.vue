<template>
    <div>
        <h1>
            Eurosong voting app!
        </h1>

        <button class="butt" @click="goToPage('game')">
            Show game
        </button>

        <button class="butt" @click="goToPage('ranking')">
            Show ranking
        </button>
    </div>
</template>

<script>
    export default {
        name: "Homepage",
        methods: {
            goToPage(page) {
                this.$emit("change-page", page);
            }
        }
    }
</script>