<template>
    <div class="modal-wrap" v-if="visibleModal !== null">
        <div class="modal-overlay" @click="closeModal"></div>
        <div class="modal">
            <!-- <button @click="closeModal" class="modal-close">닫기</button> -->
            
            <!-- $emit -->
            <button @click="$emit('close-modal')" class="modal-close">
                닫기
            </button>
            <div class="modal-head">
                <h2>{{ products[visibleModal].modalHead }}</h2>
            </div>
            <div class="modal-content">
                <div class="modal-content-img">
                    <img :src="products[visibleModal].imgSrc" alt="음료 이미지">
                </div>
                <div class="modal-content-info">
                    <p v-if="products[visibleModal].modalCont2 !== ''">{{ products[visibleModal].modalCont2 }}</p>
                    <p v-else>데이터가 없습니다.</p>
                </div>
            </div>
            <div class="modal-footer">
                <span>{{ products[visibleModal].price }} won</span>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Modal',
    props: {
        products : Array,
        visibleModal: Boolean,
        closeModal: Function
    },
    data() {
        return {}
    },
}
</script>

<style></style>
