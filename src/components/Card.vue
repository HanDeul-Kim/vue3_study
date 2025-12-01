<template>
    <li>
        <div class="product-img">
            <img :src="e.imgSrc" alt="원룸 이미지"></img>
        </div>
        <a href="javascript:void(0);" @click="openModal(idx)">{{ e.title }}</a>
        <p>{{ e.price }}원</p>
        <div class="btn-wrap report">
            <button @click="e.currentNum++" class="btn-sm btn-28 btn-thumb">좋아요</button>
            <span>누적 수 : {{ e.currentNum }}</span>
        </div>
    </li>
</template>

<script>
export default {
    name: 'Card',
    props: {
        e: Array,
        idx: Number,
        openModal: Function
    },
    data() {
        return {}
    }
}
</script>

<style></style>
