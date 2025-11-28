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
                <input v-model="quantity" type="text" class="input-32" placeholder="수량 input">
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
    // input으로 받은 data값 감시하는 함수
    watch: {
        // quantity가 변경 될 때마다 아래 함수 실행 됨
        quantity(a, b) {
            // a는 지금 변경된 최신 값. 즉, 마지막으로 입력된 quantity값
            // b는 바뀌기 이전의 값
            

            if(isNaN(a)) {
                alert('숫자만 입력 가능합니다.')
                this.quantity = b;
            }
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
        },



    },
}
</script>

<style></style>
