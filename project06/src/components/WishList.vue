<!-- WishList.vue -->
<template lang="html">
<section>
    <ul>
        <li v-for="wishItem in wishItems" class="shadow">
            <i class="checkBtn fas fa-check" aria-hidden="true"></i>
            {{ wishItem}}
            <span class="removeBtn" type="button" @click="removeWish">
            <!--@ = v.on:Click  의 줄임말-->
                <i class="far fa-trash-alt" aria-hidden="true"></i>
            </span>
         </li>
    </ul>
</section>
</template>
<script>
    export default{
        data(){
            return{
                wishItems: []
            }
        },
        methods:{
            removeWish(){
                console.log('clicked');
            }
        },
        created(){
            if(localStorage.length > 0){
                for(var i=0; i< localStorage.length; i++){
                    this.wishItems.push(localStorage.key(i));
                }
            }
        }
    }
</script>
<style lang="css" scoped>
    ul{
        list-style-type: none;
        padding-left: 0px;
        margin-top: 0px;
        text-align: left;
    }
    li{
        display: flex; /* 비율 기준의 레이아웃 방식인 flex로 지정*/
        min-height: 50px;
        height: 50px;
        line-height: 50px;
        margin: 0.5em 0;
        padding: 0 0.9em;
        background: #fefefe;
        border-radius: 5px;
        overflow: hidden;
        text-overflow: ellipsis;
     }
     .checkBtn{
         line-height: 50px;
         color: #ff8000;
         margin-right: 5px;
     }
     .removeBtn {
        margin-left: auto;
        color: #de4343;
    }


</style>
