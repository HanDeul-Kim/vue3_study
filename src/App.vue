<template>
    <div class="container">
        <Header />
        <section>
            <Banner />

            <div class="item-info-inner">
                <ul>
                    <li v-for="(e, idx) in products" :key="idx">
                        <div class="product-img">
                            <img :src="e.imgSrc" alt="원룸 이미지"></img>
                        </div>
                        <a href="javascript:void(0);" @click="openModal(idx)">{{ e.title }}</a>
                        <p>{{ e.price }}원</p>
                        <div class="btn-wrap report">
                            <button @click="e.currentNum++">좋아요</button>
                            <span>누적 수 : {{ e.currentNum }}</span>
                        </div>
                    </li>
                </ul>
            </div>
        </section>

        <!-- vue에서의 if문 -->
        <!-- <div v-if="1 == 2">
            참일 때 보여줘
        </div>
        <div v-else>
            else문
        </div>
        <div v-else-if="1 == 1">
            else if 문
        </div> -->

        <!-- <div class="modal-wrap" v-if="visibleModal !== null">
            <div class="modal-overlay" @click="closeModal"></div>
            <div class="modal">
                <button @click="closeModal" class="modal-close">닫기</button>
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
        </div> -->
        <Modal />
    </div>
</template>

<script>
// 상품 데이터 import
import productData from './assets/data'
// 컴포넌트
import Header from './components/Header.vue'
import Banner from './components/Banner.vue'
import Modal from './components/Modal.vue'

export default {
    name: 'App',

    // 데이터 보관함. 변수같은 거 여기에 만든다고 보면 됨
    data() {
        return {
            // 상품 데이터
            products: productData,
            // 모달 상태
            visibleModal: null,
        }
    },
    // vue에서 함수 만들 때
    methods: {
        openModal(idx) {
            this.visibleModal = idx;
        },
        closeModal() {
            this.visibleModal = null;
        }
    },
    components: {
        Header, Banner, Modal
    }
}
</script>

<style></style>