<!-- WishList.vue -->
<template lang="html">
<section>
    <transition-group name="list" tag="ul">
        <li v-for="(wishItem, index) in propsData" v-bind:key="wishItem" class="shadow">
            <i class="checkBtn fas fa-check" aria-hidden="true"></i>
            {{ wishItem}}
            <span class="removeBtn" type="button" @click="removeWish(wishItem, index)">
            <!--@ = v.on:Click  의 줄임말-->
                <i class="far fa-trash-alt" aria-hidden="true"></i>
            </span>
         </li>
    </transition-group>
</section>
</template>
<script>
    export default{
        props:['propsData'],
        //상위에서 하위 컴포넌트로 데이터를 전달함.
        //data(){
        //    return{
        //        wishItems: []
        //    }
        //},
        methods:{
            removeWish(wishItem, index){
                //console.log(wishItem, index);
                //localStorage.removeItem(wishItem);
                //this.wishItems.splice(index, 1);
                //여기서는 상위로 삭제할 내용을 전달해서 올리고 App.vue에서 실제로 삭제
                this.$emit('removeWish', wishItem, index);
            }
        }
    }
</script>
<style lang="css" scoped>
    .list-enter-active, .list-leave-active{
        transition: all 0.5s;
    }
    .list-enter, .list-leave-to{
        opacity: 0;
        transform: translateY(30px);
    }
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
