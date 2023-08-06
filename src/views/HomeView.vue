<template>
    <div class="home">
        <img alt="Vue logo" src="../assets/logo.png">
    </div>

    <h1>Hello World</h1>
    <button @click="gotToDaybook" class="btn btn-primary">Primary</button>
    <button @click="gotToDaybook" class="btn btn-secondary">Secondary</button>
    <button @click="gotToDaybook" class="btn btn-success">Success</button>

</template>

<script>


export default ({
    methods: {
        gotToDaybook() {
            this.$router.push({name: 'no-entry'})
        }
    },
})
</script>

