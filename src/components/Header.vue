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

    data() {
        return {
            menus: [
                { name: '메뉴', link: 'javascript:void(0);' },
                { name: '스토어 찾기', link: 'javascript:void(0);' },
                { name: '오시는길', link: 'javascript:void(0);' }
            ],
        }
    },
}
</script>

<style></style>
