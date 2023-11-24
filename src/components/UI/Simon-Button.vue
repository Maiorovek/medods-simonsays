<template>
    <div class="simon-button" :style="{ backgroundColor: color }">
    </div>
</template>

<script>
export default {
    name: 'SimonButton',

    props: {
        color: {
            type: String,
            required: true,
        },
    },

}
</script>

<style scoped>
.simon-button {
    height: 200px;
    width: 200px;
    transition: opacity .1s ease;
    opacity: .5;
}

.simon-button:active {
    transition: opacity .1s ease;
    opacity: 1;
}
.active {
    transition: opacity .1s ease;
    opacity: 1;
}
</style>