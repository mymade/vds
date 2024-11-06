<template>
    <div class="cards">
      <div>
        <h4>{{원룸들.title}}</h4>
        <img class="img" :src="원룸들.image">
        <p>월세 : {{원룸들.price}}</p>
        <div>
          <button class="more-btn" @click="sended">More <i class="bi bi-chevron-double-right"></i></button>
        </div>
        <button class="report-btn" @click="increasing">허위매물신고 <i class="bi bi-exclamation-diamond-fill"></i></button>
        <span class="ml-15">신고수 : {{ 신고수 }}</span>
    </div>
    </div>
</template>
<script>
    export default {
        name:'CardTemplate',
        // 다중 단어로 해주어야 should multi-words 오류가 발생하지 않는다.
        props:{
                모달창:Boolean,
                원룸들:Object,
                신고수:Number,
                누른거:Number,
            },
        methods:{
          increasing(){
            this.$emit('increased', this.신고수)
          },
            sended(){
                this.$emit('openModal', this.원룸들.id)
            }
        }
    } 
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


.cards div{
  margin-top: 60px;
  margin-bottom: 100px;
}

.cards h4{
  margin-bottom: 25px;
  font-size: 18pt;
}

.cards img{
  margin-bottom: 20px;
}

.more-btn{
  padding: 15px 40px;
  font-size: 12pt;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: 0.4s;
}

.report-btn{
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: 0.4s;
}

.more-btn:hover{
  background-color: rgb(36, 36, 107);
  color: white;
  transform: scale(1.1);

}

.report-btn:hover{
  background-color: rgb(190, 0, 0);
  color: white;

}
</style>