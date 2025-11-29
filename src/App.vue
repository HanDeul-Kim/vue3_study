<template>
    <div class="container">
        <!-- 헤더 -->
        <Header :menus="menus" />
        <section>
            <!-- 배너 -->
            <Banner />

            <!-- Card 레이아웃 -->
            <div class="item-info-inner">
                <ul>
                    <Card v-for="(e, idx) in products" :e="e" :idx="idx" :openModal="openModal" :key="idx" />
                </ul>
            </div>
        </section>
        <!-- 모달 -->
        <!--
            애니메이션 방법1. 
            클래스명 : 조건 => 조건이 true일때 class명 적용, false일때 class명 없음
        -->
        <!-- <div class="modal-anim-start" :class="{'modal-anim-end' : visibleModal}">
            <Modal @close-modal="visibleModal=null" :products="products" :visibleModal="visibleModal" :closeModal="closeModal" />
        </div> -->

         <!--
            애니메이션 방법2. 
            vue 내장 컴포넌트 transition 사용하기
        -->
        <Transition name="fade">
            <Modal @close-modal="visibleModal=null" :products="products" :visibleModal="visibleModal" :closeModal="closeModal" />
        </Transition>
    </div>
</template>

<script>
// 상품 데이터 import
import productData from './assets/data'
// 컴포넌트
import Header from './components/Header.vue'
import Banner from './components/Banner.vue'
import Card from './components/Card.vue'
import Modal from './components/Modal.vue'

export default {
    name: 'App',

    // 데이터 보관함. 변수같은 거 여기에 만든다고 보면 됨
    data() {
        return {
            // gnb 메뉴
            menus: [
                { name: '메뉴', link: 'javascript:void(0);' },
                { name: '스토어 찾기', link: 'javascript:void(0);' },
                { name: '오시는길', link: 'javascript:void(0);' }
            ],
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
        Header, Banner, Card, Modal
    }
}
</script>

<style></style>