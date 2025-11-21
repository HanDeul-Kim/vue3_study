<template>
    <header>
        <div class="menu">
            <a :href="e.link" v-for="(e, idx) in menus" :key="idx">{{ e.name }}</a>
        </div>
    </header>

</template>

<script>
    export default {
    name: 'Header',
    props: {
        menus : Array
    },
    data() {}
}
</script>

<style></style>
