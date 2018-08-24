<template>
<div>
    <div class="container"  @click="swipetap">
        {{$store.state.nowIndex+1}}
        <v-touch tag="div" v-bind:style='styleObj' class="content" @swiperight="onswiperight" @swipeleft="onSwipeLeft">Swipe me!</v-touch>
        <img src="../.././../public/img/photo/2.jpg" alt="">
    </div>
</div>
</template>

<script>
    import Vue from 'vue'
    import VueTouch from 'vue-touch'
    Vue.use(VueTouch, {name: 'v-touch'})

    export default {
        created(){
          this.$emit('routerChange','photo');
          if(this.$store.state.nowIndex== -1){
              this.$router.push("/photo")
          }

        },
        data(){
            return{
                nowIndex2:this.$store.state.nowIndex+1,
                thisLength:this.$store.state.nowIndex,
            }
        },
        computed:{  //计算属性 实现
            styleObj(){
                console.log(this.nowIndex2)
                return{
                    background:'#000 url("../.././../public/img/photo/${this.nowIndex2}.jpg") no-repeat center/contain' //字符串模板
                }
            }
        },
        methods:{
            onSwipeLeft(){
                console.log("left")
                    this.nowIndex2++;
                // 边界判断
                if(this.nowIndex2 == this.thisLength +1){
                    this.nowIndex2 = 1
                }


            },
            swipetap(){
                console.log("click")
                this.$router.push("/photo")
                //图片闪烁 ajax tap点透问题 fastclick.js
            },
            onswiperight(){
                console.log("Right")
                this.nowIn--
                if(this.nowIndex2 == 0){
                    this.nowIndex2 = this.thisLength
                }
            }
        }
    }
</script>

<style scoped>
    .content{
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
    }
</style>