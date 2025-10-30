<template>
    <div class="container">
        <header>
            <div class="menu">
                <a :href="e.link" v-for="(e, idx) in menus" :key="idx">{{ e.title }}</a>
            </div>
        </header>
        <section>
            <div class="item-info-inner">
                <!-- 반복문 -->
                <ul>
                    <li v-for="(e, idx) in products" :key="idx">
                        <div class="product-img">
                            <img :src="e.imgSrc" alt="원룸 이미지"></img>
                        </div>
                        <a href="javascript:void(0);" @click="openModal(idx)">{{e.title}}</a>
                        <p>{{e.price}}원</p>
                        <div class="btn-wrap report">
                            <button @click="e.currentNum++">좋아요</button>
                            <span>누적 수 : {{e.currentNum}}</span>
                        </div>
                    </li>
                </ul>

            </div>


        </section>
    </div>


    
    <!-- vue도 props같은게 있는지 보고 재사용성 고려해보자 -->
    <div class="modal-wrap" v-if="visibleModal !== null">
        <div class="modal">
            <button @click="closeModal" class="modal-close">닫기</button>
            <h2>상세 페이지({{products[visibleModal].modalCont}})</h2>
            <p>상세 페이지 내용 상세 페이지 내용상세 페이지 내용상세 페이지 내용 상세 페이지 내용 상세 페이지 내용 상세 페이지 내용 상세 페이지 내용 상세 페이지 내용 상세 페이지 내용 상세 페이지 내용</p>
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
                { name: 'Home', link: 'javascript:void(0);' },
                { name: 'Products', link: 'javascript:void(0);' },
                { name: 'About', link: 'javascript:void(0);' }
            ],
            // 상품 데이터
            products: productData,
            // 모달 상태
            visibleModal: null
        }
    },
    // vue에서 함수 만들 때
    methods : {
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
section {
    padding: 0 20px;
}
.menu {
    display: flex;
    gap: 12px;
    background-color: dodgerblue;
    padding: 16px;
    border-radius: 10px;
}

.menu>a {
    color: #fff;
}

.item-info-inner>ul {
    display: flex;
    flex-direction: column;
}

.item-info-inner>ul>li {
    padding:16px;
    margin-top: 20px;
    border: 1px solid #000;
    border-radius: 12px;
}
.product-img img{
    width: 100%;
    max-width:200px;
}
.btn-wrap.report {}
.btn-wrap.report button {
    padding: 0 4px;
    height: 28px;
    background-color: #b71919;
    color:#fff;
    border-radius: 4px;
    border: 1px solid #fff;
    margin-right: 12px;
}
.btn-wrap.report span {
    font-size: 14px;
    color:#111;
}
/********************** 모달 **********************/
.modal-wrap {
    width: 100%;
    height: 100vh;
    position: fixed;
    top: 0;
    left: 0;
    background-color: rgba(0,0,0,0.7);
    display:flex;
    justify-content: center;
    align-items: center;
    padding: 20px;
}
.modal {
    position: relative;
    width: 100%;
    max-width:700px;
    background-color: #fff;
    padding: 20px 40px;
    display:flex;
    flex-direction: column;
    align-items: center;
    gap:12px;
}
.modal-close {
    position: absolute;
    top: 20px;
    right: 20px;
    font-weight: 500;
    font-size: 14px;
}
.modal > h2 {
    font-size: 28px;
    color:#000;
}
.modal > p {
    color: #333;
}
</style>