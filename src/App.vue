<template>
    <div class="container">
        <header>
            <div class="menu">
                <a :href="e.link" v-for="(e, idx) in menus" :key="idx">{{ e.name }}</a>
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
                        <a href="javascript:void(0);">{{e.name}}</a>
                        <p>{{e.price}}</p>
                        <div class="btn-wrap report">
                            <button @click="e.reportNum++">허위매물신고</button>
                            <span>누적 신고 : {{e.reportNum}}</span>
                        </div>
                    </li>
                </ul>


                <!-- 이벤트 핸들러 -->
                <!-- <ul>
                    <li>
                        <a href="javascript:void(0);">{{products[0].name}}</a>
                        <p>80만원</p>
                        <div class="btn-wrap report">
                            <button @click="plus">허위매물신고</button>
                            <span>누적 신고 : {{products[0].reportNum}}</span>
                        </div>
                    </li>
                    <li>
                        <a href="javascript:void(0);">{{products[1].name}}</a>
                        <p>60만원</p>
                        <div class="btn-wrap report">
                            <button @click="plus">허위매물신고</button>
                            <span>누적 신고 : {{products[1].reportNum}}</span>
                        </div>
                    </li>
                    <li>
                        <a href="javascript:void(0);">{{products[2].name}}</a>
                        <p>70만원</p>
                        <div class="btn-wrap report">
                            <button @click="plus">허위매물신고</button>
                            <span>누적 신고 : {{products[2].reportNum}}</span>
                        </div>
                    </li>
                </ul> -->
            </div>


        </section>
    </div>
</template>

<script>
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
            products: [
                {name:'역삼동 원룸', price:'80만원', reportNum: 0, imgSrc: '/img/room0.jpg'},
                {name:'대방동 원룸', price:'60만원', reportNum: 0, imgSrc: '/img/room1.jpg'},
                {name:'자양동 원룸', price:'70만원', reportNum: 0, imgSrc: '/img/room2.jpg'}
            ],
            // currentNum1: 0,
            // currentNum2: 0,
            // currentNum3: 0,
        }
    },
    // vue에서 함수 만들 때
    methods : {
        // plus() {
        //     this.products.reportNum++;
        // }
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
    width: 500px;
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
</style>