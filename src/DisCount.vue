<template>
    <wrap>
       <div class="txtbox">
            <p>지금 결제하면 {{amount}} 할인!</p>
       </div>
    </wrap>
</template>

<script>
export default{
    name:'DisCount',
    data(){
       return {
        amount:5,
       } 
    },
    mounted(){
        let inter = setInterval(()=>{
            this.amount--;
            if(this.amount == 0){
            clearInterval(inter);
        }
        },1000)
    }
}
</script>

<style>
.txtbox{
    margin: 10px;
    height: 100px;
    background-color: gray;
    color: white;
    line-height: 100px;
    font-size: 16pt;
    font-weight: bold;
    border-radius: 10px;
}
</style>