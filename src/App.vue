<template>
    <div class="container">
        <!-- 헤더 -->
        <Header :menus="menus" />
        <section>
            <!-- 배너 -->
            <Banner v-if="showBanner == true" />

            <!-- 아이템 sort -->
            <div class="sort-button-wrap">
                <button @click="toggleList" class="btn-md btn-32 btn-primary">
                    <!-- 꼭 논리연산자를 써야하나? -->
                    {{ currentType || '기본순' }}
                </button>


                <ul class="sort-list" v-if="visibleSortMenu">
                    <li v-for="(e, idx) in sortTypes" @click="sortItems(e)" :key="idx"
                        :class="{ 'active': e === currentType }">{{ e }}</li>
                </ul>
            </div>

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
            <Modal @close-modal="visibleModal = null" :products="products" :visibleModal="visibleModal"
                :closeModal="closeModal" />
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
            showBanner: true,
            // 상품 데이터
            products: productData,
            // 상품 데이터 원본 복사
            originalProducts: [...productData],

            // 모달 상태
            visibleModal: null,
            // 정렬버튼 상태
            visibleSortMenu: false,
            // 아이템 정렬
            currentType: "기본순",
            sortTypes: ['기본순', '이름순', '가격순'],
        }
    },
    // vue에서 함수 만들 때
    methods: {
        openModal(idx) {
            this.visibleModal = idx;
        },
        closeModal() {
            this.visibleModal = null;
        },
        // 메뉴 토글 
        toggleList() {
            this.visibleSortMenu = !this.visibleSortMenu;
        },
        // 아이템 정렬
        sortItems(type) {
            this.currentType = type;
            this.visibleSortMenu = false;
            if (type == '기본순') {
                this.products = [...this.originalProducts]
            } else if (type == '이름순') {
                this.products.sort((a, b) => { return a.title.localeCompare(b.title) })
            } else if (type == '가격순') {
                this.products.sort((a, b) => { return Number(a.price.replace(/,/g, "")) - Number(b.price.replace(/,/g, "")) })
            }
        },

    },
    components: {
        Header, Banner, Card, Modal
    },
    // vue의 라이프사이클 훅 9가지
    // beforeCreate (생성단계) 데이터와 이벤트 초기화 전
    // created (생성단계) 데이터, computed, methods, watch만 있을떄
    // beforeMount (마운트 단계) 컴포넌트가 DOM에 붙기 직전
    // mounted (마운트 단계) 컴포넌트가 DOM에 완전히 붙은 후
    // beforeUpdate (업데이트 단계) 데이터 변경 => DOM 업데이트 전
    // updated (업데이트 단계) DOM 업데이트 완료 후
    // beforeUnmount (제거 단계) 컴포넌트 제거 직전
    // unmounted (제거 단계) 컴포넌트가 DOM에서 제거된 후
    // errorCaptured (에러 처리) 하위 컴포넌트에서 에러 발생시



}
</script>

<style></style>