
<template>
<div class="wrap">

  <div v-if=" 1 == 3">
    안녕하세요
  </div>

  <div v-else-if="1 == 8">
    다시 만나요
  </div>
  
  <transition name="작명">
    <!-- <div class="start" :class="{end : 모달창}"> -->
      <Modal @closeModal="모달창 = false;" :원룸들="원룸들" :누른거="누른거" :모달창="모달창" :인적="인적" :작명="[11,2,3]"/>
  <!-- </div> -->
  </transition>
  

  
  <nav>
    <ul>
      <li><a href="#" v-for="(작명,i) in 메뉴들" :key="i" >{{ 작명 }}</a></li>
    </ul>
  </nav>
  <Discount v-if="showDiscount == true"/>
  <div class="sort-box">
    <button class="sort-btn" @click="priceSort()" >가격 낮은 순</button>
    <button class="sort-btn" @click="priceSort2()">가격 높은 순</button>
    <button class="sort-btn" @click="sortBack()">원래대로 보기</button>
  </div>
  <Cards  :원룸들="원룸들[i]"  :신고수="신고수[i]" v-for="(작명, i) in 원룸들" :key="작명" @increased="increase(i)" @monthPrice="pricing(i, month)" @openModal="모달창 = true; 누른거= $event"></Cards>
  <!-- <ul>
    <li :id="i" v-for="(작명,i) in products" :key="i">{{작명}}</li>
  </ul> -->
  </div>
  

</template>

<script>
import data from './db/oneroom.js';
import Modal from './GoodModal.vue';
import Cards from './CardTemplate.vue'
import Discount from './DisCount.vue';



export default {
  name:'App',
  data(){
    return{
      showDiscount:true,
      누른거:0,
      모달창:false,
      메뉴들 : ['Home', 'Shop', 'About'],
      products:['역삼동원룸','천호동원룸','마포구원룸'],
      imgs:['assets/room0.jpg', 'assets/room1.jpg', 'assets/room2.jpg'],
      price:[50,70,80],
      스타일 : 'color:blue',
      신고수 : [0,0,0,0,0,0],
      // 배열로 각 상품의 신고 수를 관리하려면 그만큼 숫자를 입력해둬야 하는데 다른 방법이 없을까... 늘어나면 번거로울듯
      원룸들 : [...data],
      인적 : {name:'anna', age:10},
      원룸들오리지널:[...data]
    }
  },
  mounted(){
    // setTimeout(()=>{this.showDiscount = false},10000)
  },
  components:{
    Modal,
    Cards,
    Discount
  },
  methods:{
    activeBack(){
      document.getElementsByClassName("sort-btn")[0].classList.remove("active")
      document.getElementsByClassName("sort-btn")[1].classList.remove("active")
      document.getElementsByClassName("sort-btn")[2].classList.add("active")
    },
    activeFirst(){
      document.getElementsByClassName("sort-btn")[0].classList.add("active")
      document.getElementsByClassName("sort-btn")[1].classList.remove("active")
      document.getElementsByClassName("sort-btn")[2].classList.remove("active")
    },
    activeSecond(){
      document.getElementsByClassName("sort-btn")[0].classList.remove("active")
      document.getElementsByClassName("sort-btn")[1].classList.add("active")
      document.getElementsByClassName("sort-btn")[2].classList.remove("active")
    },
    priceSort(){
      this.원룸들.sort((a,b)=> a.price - b.price);
      this.activeFirst();
    },
    priceSort2(){
      this.원룸들.sort(function(a,b){
        return b.price - a.price;
      })
      this.activeSecond();
    },
    sortBack(){
      this.원룸들 = [...this.원룸들오리지널]
      this.activeBack();
    },

    increase(i){
      this.신고수[i] += 1;
    },
    pricing(i, month){
      this.원룸들[i].price * month
    },
    clicked(){
      document.querySelector(".black-bg").classList.add("d-block")
    },
    closed(){
      document.querySelector(".black-bg").classList.remove("d-block")
  }
}}
</script>



<style>
@font-face {
    font-family: 'Pretendard-Regular';
    src: url('https://fastly.jsdelivr.net/gh/Project-Noonnu/noonfonts_2107@1.1/Pretendard-Regular.woff') format('woff');
    font-weight: 400;
    font-style: normal;
}

*{
  font-family: 'Pretendard-Regular';
  text-decoration: none;
  list-style: none;
  padding: 0;
  margin: 0;
}

.d-block{
  display: block !important;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav > ul > li {
  background : darkslateblue;
  padding : 20px;
  /* border-radius : 8px; */
}
nav > ul > li > a {
  color : white;
  padding : 10px;
}



.ml-15{
  margin-left: 15px;
}


.img{
  object-fit: contain;
  width: 500px;
  height: auto;
}
.modal{
  width: 100%;
  height: 100%;
  position: relative;
  /* overflow: hidden; */
  z-index: 9999;

}

.작명-enter-from { opacity: 0;  }
.작명-enter-active { transition: all 1s; }
.작명-enter-to { opacity: 1; }


/* .start{
  opacity: 0;
  transition:all 1s;
}
.end{
  opacity: 1;
} */

/* modal 컴포넌트에 줄 각각의 애니메이션 */

.d-none{
  display: none;
}

.black-bg{
  /* display: none; */
  width: 100%; height:100%;
  background: rgba(0,0,0,0.5);
  position: fixed; padding: 20px;
}

.box{
  width: 1200px;
  height: 600px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  border-radius: 8px;
  overflow: hidden
  /* overflow scroll을 적용한 white-bg의 부모인 box에게 overflow hidden을 준 상태로 boder-radius를 해야 모서리가 네개 다 둥글어진다 */
}

.white-bg{
  width: 100%; 
  height: 600px;
  background: white;
  border-radius: 8px;
  padding: 20px;
  /* padding 값이 들어가 있기 때문에 box-sizing을 border-box로 해주지 않으면 값이 넘쳐나서 스크롤바가 보이지 않는다. */
  box-sizing: border-box;
  overflow-y: scroll;
  overflow-x: hidden;
  /* overflow-y:scroll은 컨텐츠 높이가 태그의 높이를 넘어설 때 스크롤을 만들어준다.  */
}

/* .white-bg::-webkit-scrollbar{
  width: 20px;

} */

.white-bg > img{
  width: 500px;
  height: 500px;
  object-fit: contain;
}

.sort-btn{
  margin-top: 30px;
  padding: 12px 15px;
  border: none;
  transition: 0.3s;
  border-radius: 8px;
  cursor: pointer;
  margin-left: 15px;
}

.sort-btn:hover{
  background-color: rgb(40, 40, 40);
  color: white;
}

.sort-btn.active{
  background-color: rgb(40, 40, 40);
  color: white;
}

.sort-box .sort-btn:nth-child(3){
  margin-right: 0 !important
}

</style>
