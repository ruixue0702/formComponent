<template>
    <div>
        <input class="x_input" :class="formItem.isError ? 'x_error' : ''" :value="value" @input="onInput" @focus="onFocus" v-bind="$attrs">
    </div>
</template>

<script>
    export default {
        inject: ["formItem"],
        inheritAttrs: false, // inheritAttrs:false 禁用特性继承; inheritAttrs默认为true；即允许继承的意思; $attrs为组件标签内没有在组件内用props声明的属性（除style和class外）
        props: { // 父组件传value
            value: { // 类型 Sting  默认 ''
                type: String,
                default: ''
            }
        },
        data(){
            return {
                isInput: false
            }
        },
        methods: {
            onInput(e){ // @input 事件响应 获取input的值
                console.log('oninput', e.target.value)
                this.$emit("input", e.target.value,this.formItem.isError)
                if (this.isInput){
                    this.$parent.$emit('validate') // this.$parent.$emit('eventName') 向兄弟组件传值 / 触发事件,向公共父组件派送事件（把事件沿作用域链向上派送）
                } else {
                    this.isInput = true
                }
            },
            onFocus(e){
                console.log('onFocus',this.formItem.isError)
                if (this.formItem.isError ){
                    this.formItem.isError = false
                }
                this.$parent.$emit('focus')
            }
        }
    }
</script>
<style scoped>
    input.x_input {
        width: auto;
        height: 32px;
        line-height: 20px;
        padding: 0 12px;
        background: #fff;
        border: 1px solid #eee;
        border-radius: 4px;
        outline: 0;
        box-shadow: inset #fff 100px 100px;
        color: #333 !important;
        transition: border-color 0.3s ease-in-out;
        -webkit-transition: border-color 0.3s ease-in-out;
    }
    input.x_input:hover {
        border: 1px solid rgba(27, 141, 245, 1);
    }
    input.x_input.x_error,input.x_input.x_error:hover {
        border: 1px solid rgba(245,100,100,1);
    }
    input:-webkit-autofill, textarea:-webkit-autofill, select:-webkit-autofill{
        color: #333 !important;
    }
</style>
