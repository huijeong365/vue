<!-- WishInput.vue -->
<template lang="html">
    <div class="inputBox shadow">
        <input type="text" v-model="newWishItem" v-on:keyup.enter="addWish" placeholder="해야 할 일을 입력하세요.">
        <!--v-on:keyup.enter="addWish" 엔터키를 치는 효과-->
        <span class="addContainer" v-on:click="addWish">
            <i class="addBtn fas fa-plus" aria-hidden="true"></i>
        </span>

        <modal v-if="showModal" @close="showModal=false">
            <!--모달 제목-->
            <h3 slot="header">경고</h3>
            <!--모달 내용-->
            <span slot="footer" @click="showModal=false">
                위시 리스트를 입력하세요.
                <i class="closeModalBtn fas fa-times" aria-hidden="true"></i>
            </span>
        </modal>

    </div>
</template>
<script>
import Modal from './common/Modal.vue'
    export default{
        data(){
            return{
                newWishItem:'',
                showModal: false
            }
        },
        methods:{
            addWish(){
                if(this.newWishItem !==""){
                    var value = this.newWishItem && this.newWishItem.trim();
                    this.$emit('addWish', value);
                    //console.log(this.newWishItem);
                    //localStorage.setItem(value, value);
                    //inputBox의 입력값을 초기화
                    this.clearInput();
                } else {
                    this.showModal = !this.showModal;
                }
            },
            clearInput(){
                this.newWishItem ='';
            }
        },
        components:{
            Modal : Modal
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
