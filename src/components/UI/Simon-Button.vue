<template>
    <div 
        class="simon-button" 
        :style="{ backgroundColor: color }"
    />
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
    height: 15vw;
    width: 15vw;
    transition: opacity .2s ease;
    opacity: .5;
    box-shadow: none;
    transition: box-shadow .2s ease;
}

.simon-button:active {
    transition: opacity .2s ease;
    opacity: 1;
}

.simon-button:hover {
    box-shadow: 10px 5px 5px #1d1d1db4;
    transition: box-shadow .2s ease;
}

.active {
    transition: opacity .2s ease;
    opacity: 1;
}

</style>