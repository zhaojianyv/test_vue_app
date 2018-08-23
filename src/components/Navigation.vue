<template>
    <div v-bind:class=" active">
        <header>
            <span @click="routerPush({
                        name:'book',
                        title:'书籍',
                        id:'101',
                        path:'/book'
            })">首页</span>
            <h3>{{title}}</h3>
        </header>
        <footer>
            <ul>
                <!--<li>书籍</li>-->
                <!--<li>电影</li>-->
                <!--<li>音乐</li>-->
                <!--<li>图片键值对</li>-->
                <li :class="{liactive:active == items.name}" @click='routerPush(items)' v-for="(items,index) in navList" :key="index+'nav'">
                    {{items.title}}
                </li>
            </ul>
        </footer>
    </div>
</template>

<script>
    export default {
        props:['booktitle'],
        mounted(){
            this.$nextTick(function () {
                this.navList.forEach(val =>{
                    if (val.name == this.booktitle){ //被选中
                        this.active = val.name;
                        this.title = val.title;
                    }
                })
            })
          // console.log(this);
          // console.log(this.booktitle)
        },
        methods:{
            routerPush(obj){
                this.$router.push(obj.path);
                this.active= obj.name;
                this.title = obj.title;
            }
        },
        // name: "navigation"
        data(){
            return{
                active:"book",
                title:"书籍",
                navList:[
                    {
                        name:'book',
                        title:'书籍',
                        id:'101',
                        path:'/book'
                    },                    {
                        name:'movie',
                        title:'电影',
                        id:'102',
                        path:'/movie'
                    },                    {
                        name:'music',
                        title:'音乐',
                        id:'103',
                        path:'/music'
                    },                    {
                        name:'photo',
                        title:'图片',
                        id:'104',
                        path:'/photo'
                    },
                ]
            }
        }
    }
</script>

<style scoped>
    .liactive{
        color: #fff;
    }
    .movie header,.movie nav{
        background-color: black;
    }
    .music header,.music nav{
        background-color: aqua;
    }
    .photo header,.photo nav{
        background-color: blueviolet;
    }
    .book header,.book nav{
        background-color:pink;
    }
    header,footer{
        height: 2.5rem;
        width: 100%;
        position: fixed;
        background-color: rgb(40,150,200);
        color: gray;
    }
    header{
        top: 0;
    }
    footer{
        bottom: 0;
    }
    header h3{
        /*text-align: center;*/
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%,-50%);
    }
    header span{
        display: inline-block;
        height: 2.5rem;
        line-height: 2.5rem;
        margin-left: .3rem;
    }
    footer ul{
        display: flex;
    }
    footer ul li{
        list-style: none;
        flex-grow: 1;
        text-align: center;
        height: 2rem;
        line-height: 2rem;
    }
</style>