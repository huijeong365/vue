<!-- WishInput.vue -->
<template lang="html">
    <div class="inputBox shadow">
        <input type="text" v-focus v-model="newWishItem" v-on:keyup.enter="addWish"
                placeholder="해야할 일을 입력하세요." />
        <span class="addContainer" v-on:click="addWish">
            <i class="addBtn fas fa-plus" aria-hidden="true"></i>
        </span>

        <modal v-if="showModal" @close="showModal = false">
            <!-- 모달 제목 -->
            <h3 slot="header">경고</h3>
            <!-- 모달 내용 -->
            <span slot="footer" @click="showModal = false">
                할 일을 입력하세요.
                <i class="closeModalBtn fas fa-times" aria-hidden="true"></i>
            </span>
        </modal>
    </div>
</template>
<script>
// Modal.vue 불러오기
import Modal from './common/Modal.vue'

export default {
    data(){
        return {
            newWishItem:'',
            // 모달 동작을 위한 플래그 값
            showModal: false
        }
    },
    // v-focus 디렉티브
    directives: {
        focus: {
            // directive definition
            inserted: function (el) {
                el.focus()
            }
        }
    },
    methods:{
        addWish(){
            //console.log(this.newWishItem);
            // 인풋 박스의 입력 값이 있을 때만 저장
            if(this.newWishItem !== ""){
                // 인풋 박스에 입력된 텍스트의 앞뒤 공백 문자열 제거
                const value = this.newWishItem && this.newWishItem.trim();
                const key = "vue-wish-" + new Date().getTime();
                this.$emit("addWish", key, value, new Date().getTime());
                // 인풋 박스의 입력 값을 초기화
                this.clearInput();
            } else {
                this.showModal = !this.showModal;
            }
        },
        clearInput(){
            this.newWishItem = '';
        }
    },
    // 모달 컴포넌트 등록
    components: {
        Modal: Modal
    }
}
</script>
<style lang="css" scoped>
input:focus {
    outline: none;
}
.inputBox {
    background: white;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
    margin-bottom: 25px;
}
.inputBox input {
    border-style: none;
    font-size: 1.2em;
    font-weight: bold;
    width: 12.5em;
    color: #2f3b52;
}
.addContainer {
    float: right;
    background: linear-gradient(to right, #ff4c4d, #b30000);
    display: inline-block;
    width: 3em;
    border-radius: 0 5px 5px 0;
}
.addBtn {
    color: white;
    vertical-align: middle;
}
</style>
