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
                <input v-model.number="quantity" type="text" class="input-32" placeholder="수량 input">
                <!-- <span v-if="quantity == ''">{{products[visibleModal].price}} won</span>
                <span v-else>{{ Number(products[visibleModal]?.price.replace(/,/g, '')) * quantity }} won</span> -->
                <span>{{ finalPrice() }} won</span>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Modal',
    data() {
        return {
            quantity: "",
        }
    },
    props: {
        products: Array,
        visibleModal: Boolean,
        closeModal: Function
    },
    methods: {
        // 수량에 의한 가격 결과값
        finalPrice() {
            if (isNaN(Number(this.quantity))) {
                return this.products[this.visibleModal].price;
            } else {
                const priceStr = this.products[this.visibleModal].price;
                const priceNum = Number(priceStr.replace(/,/g, ''));
                const qty = this.quantity === "" ? 1 : Number(this.quantity);
                return (priceNum * qty).toLocaleString();
            }

        }
    },
}
</script>

<style></style>
