<template>
  <div class="modal" v-if="모달창 == true">
    <div class="black-bg">
    <div class="box">
      <div class="white-bg" >
      <h4>상세페이지</h4>
      <div :id="원룸들[누른거].id">
        <h4>{{원룸들[누른거].title}}</h4>
        <img :src="원룸들[누른거].image" alt="">
        <p>{{원룸들[누른거].content}}</p>
        <input type="text" v-model.trim="month">개월
        <h3>{{원룸들[누른거].price * month}}</h3>
        <p>{{ 인적.age }}</p>
        <p>{{ 작명[0] }}</p>
      </div>
      <button @click="$emit('closeModal')">닫기</button>
       <!-- 위의 닫기 창은 전달받은 props의 속성을 true에서 false로 변경하는 기능을 갖고 있기 때문에 
        주석을 풀면 오류가 난다. 받아서 사용만 하는 ready only data -->
    </div>
    </div>
  </div>
  </div>
  </template>
  
  <script>
  export default {
    name:'GoodModal',
    data(){
      return{
        month:0,
        }
    },
      watch:{
        month(a){
          if(a >= 13 || isNaN(a) == true){
            alert("숫자만 입력해주세요");
            this.month = 1;
          }
        }
      },
      beforeUpdate(){
        if(this.month == 2){
          alert("꺼져")
          this.month = 3
        }
      },
    props:{
        원룸들 : Array,
        누른거 : Number,
        모달창: Boolean,
        인적:Object,
        작명:Array,
    },
    methods:{
    increase(i){
      this.신고수[i] += 1;
    },
    clicked(){
      document.querySelector(".black-bg").classList.remove("d-none")
    },
    closed(){
      document.querySelector(".black-bg").classList.add("d-none")
    }
  }
  }
  </script>
  
  <style>

.modal{
  width: 100%;
  height: 100%;
  position: relative;
  /* overflow: hidden; */


}




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
  </style>