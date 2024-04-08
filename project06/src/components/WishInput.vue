<!-- WishInput.vue -->
<template lang="html">
    <div class="inputBox shadow">
        <input type="text" v-model="newWishItem" v-on:keyup.enter="addWish" placeholder="해야 할 일을 입력하세요.">
        <!--v-on:keyup.enter="addWish" 엔터키를 치는 효과-->
        <span class="addContainer" v-on:click="addWish">
            <i class="addBtn fas fa-plus" aria-hidden="true"></i>
        </span>
    </div>
</template>
<script>
    export default{
        data(){
            return{
                newWishItem:''
            }
        },
        methods:{
            addWish(){
                if(this.newWishItem !==""){
                    var value = this.newWishItem && this.newWishItem.trim();
                    //console.log(this.newWishItem);
                    localStorage.setItem(value, value);
                    this.clearInput();
                }
            },
            clearInput(){
                this.newWishItem ='';
            }
        }
    }
</script>
<style lang="css" scoped>
    input:focus{
        outline: none;
    }
    .inputBox{
        background: white;
        height: 50px;
        line-height: 50px;
        border-radius: 5px;
        margin-bottom: 25px;
    }
    .inputBox input{
        border-style: none;
        font-size: 1.2em;
        font-weight: bold;
        width: 12.5em;
        color: #2f3b52;
    }
    .addContainer{
        float: right;
        background: linear-gradient(to right, #ff4c4d, #b30000);
        display: inline-block;
        width: 3em;
        border-radius: 0 5px 5px 0;
    }
    .addBtn{
        color: white;
        vertical-align: middle;
    }
</style>
