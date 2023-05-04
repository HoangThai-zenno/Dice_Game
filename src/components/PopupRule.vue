<template>
    <div class="wrapper-popup" v-bind:class="getClassPopup">
        <div class="rule">
            <h3>
                Lorem ipsum dolor sit amet consectetur adipisicing elit. Excepturi nisi id beatae repellat explicabo amet quasi
                est, quos doloremque aperiam voluptas optio ut assumenda quia accusantium, itaque, illo officia suscipit?
            </h3>
            <button @click="confirm" class="confirm">Đã hiểu</button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'popup-rule',
    props:{
        isOpenPopup:{
            type:Boolean,
            default:false
        }
    },
    data() {
        return {

        }
    },
    methods:{
        confirm(){
            this.$emit('handleConfirm')
        }
    },
    computed:{
        getClassPopup:function(){
            return{
                'open-popup': this.isOpenPopup
            }
        }
    }
}
</script>

<style>
.wrapper-popup{
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, 0.4);
    opacity: 0;
    visibility: hidden;
    transition: all .4 ease;
}
.wrapper-popup.open-popup{
    opacity: 1;
    visibility: visible;
}
.rule{
    position: absolute;
    background-color: #fff;
    width: 350px;
    padding: 30px;
    font-family: Arial, Helvetica, sans-serif;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%) scale(1.2);
    transition: all .4 ease;
}
.open-popup .rule {
    transform: translate(-50%, -50%) scale(1);;
}
.rule h3{
    margin-bottom: 10px;
}
.confirm{
    border: 2px solid #333;
    margin-top: 20px;
    background-color: #fff;
    color: #333;
    padding: 8px 15px;
    cursor: pointer;
    transition: all .4s ease;
}
.confirm:hover{
    background-color: #333;
    color: #fff;
}
</style>