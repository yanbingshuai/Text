<template>
    <div v-show="isShow">
        <div class="alert" :class="type">
            <div class="flex" >{{msg}}</div>
            <div class="space-around" v-if="type === 'alert'">
                <div class="btnCommon success" @click="close">确定</div>
            </div>
            <div class="space-around" v-else-if="type === 'confirm'">
                <div class="btnCommon cancel" @click="cancelEvent">取消</div>
                <div class="btnCommon success" @click="successEvent">确定</div>
            </div>

        </div>
        <!-- 背景遮罩 -->
        <div class="mask" @click="closeMask" v-if="type !== 'msg'"></div>
    </div>
</template>

<script>
    export default {
        name: 'Alert',
        props: {
            msg: {
                type: String,
                default: ''
            },
            isShow: {
                type: Boolean,
                default: false
            },
            type: {
                type: String,
                default: 'alert'
            },
            success: {
                type: Function,
                default: () => {
                    console.log('点击了success');
                }
            },
            cancel: {
                type: Function,
                default: () => {
                    console.log('点击了cancel');
                }
            }
        },
        methods: {
            close() {
                this.isShow = false
            },
            closeMask() {
                if(this.type === 'alert') {
                    this.close();
                }
            },
            cancelEvent() {
                this.cancel();
                this.close();
            },
            successEvent() {
                this.success();
                this.close();
            }
        },
        updated(){
            var _this = this;
            if(_this.type == 'msg'){
                setTimeout(function(){_this.close()},1500);
            }
        }
    }

</script>


