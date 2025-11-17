<template>
    <div class="container">
        <header>
            <div class="menu">
                <a :href="e.link" v-for="(e, idx) in menus" :key="idx">{{ e.name }}</a>
            </div>
        </header>
        
        <section>
            <div class="banner-promotion">
                <h2>시즌 음료 프로모션</h2>
                <p>
                    새롭게 선보이는 디카페인 아메리카노, 에티오피아 시다모 원두를 정성껏 로스팅하여 만들어졌습니다.<br>
                    풍부한 과일 향과 부드러운 초콜릿 뉘앙스가 조화를 이루며, 카페인 걱정 없이 여유로운 한 모금을 경험해보세요.
                </p>
            </div>

            <div class="item-info-inner">
                <!-- 반복문 -->
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


        
    </div>



    <!-- vue도 props같은게 있는지 보고 재사용성 고려해보자 -->
    <div class="modal-wrap" v-if="visibleModal !== null">
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
                    <p v-if="products[visibleModal].modalCont2 !== ''">{{products[visibleModal].modalCont2}}</p>
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
// 상품 데이터 import
import productData from './assets/data'

export default {
    name: 'App',

    // 데이터 보관함. 변수같은 거 여기에 만든다고 보면 됨
    data() {
        return {
            menus: [
                { name: '메뉴', link: 'javascript:void(0);' },
                { name: '스토어 찾기', link: 'javascript:void(0);' },
                { name: '오시는길', link: 'javascript:void(0);' }
            ],
            // 상품 데이터
            products: productData,
            // 모달 상태
            visibleModal: null
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

    }
}
</script>

<style>



</style>