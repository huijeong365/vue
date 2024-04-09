<template lang="html">
    <div id="app">
        <WishHeader></WishHeader>
        <!-- 앞에 addWish는 이벤트 (하위에서 함수 호출하는 이름), 뒤의 addWish는 App.vue에 정의한 함수-->
        <WishInput v-on:addWish="addWish"></WishInput>
        <WishList v-bind:propsData="wishItems" @removeWish="removeWish"></WishList>
        <WishFooter v-on:removeAll="clearAll"></WishFooter>
    </div>

</template>
<script>
    import WishHeader from './components/WishHeader.vue'
    import WishInput from './components/WishInput.vue'
    import WishList from './components/WishList.vue'
    import WishFooter from './components/WishFooter.vue'

    export default{
        data() {
            return{
                wishItems: []
            }
        },
        created(){
            if(localStorage.length > 0){
                for(var i=0; i< localStorage.length; i++){
                    this.wishItems.push(localStorage.key(i));
                }
            }
        },
        methods: {
            addWish(wishItem){
                //로컬 스토리지에 데이터를 추가하는 로직
                localStorage.setItem(wishItem, wishItem);
                this.wishItems.push(wishItem);
            },
            clearAll(){
                localStorage.clear();
                this.wishItems = [];
            },
            removeWish(wishItem, index){
                localStorage.removeItem(wishItem);
                this.wishItems.splice(index, 1);
            }
        },
        components:{
            'WishHeader': WishHeader,
            'WishInput' : WishInput,
            'WishList' : WishList,
            'WishFooter' : WishFooter
        }

    }
</script>
<style lang="css">
    body{
        text-align: center;
        background-color: #f6f6f8;
    }
    input{
        border-style: groove;
        width: 200px;
    }
    button{
        border-style: groove;
    }
    .shadow{
        box-shadow: 5px 10px 10px rgba(0,0,0,0.03);
    }
</style>
