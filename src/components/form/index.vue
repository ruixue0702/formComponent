<template>
    <div>
        <x-form :model="model" :rules="rules" ref="loginForm" :labelWidth="'120px'">
            <x-form-item class="x_mt32" label="用户名" prop="username">
                <x-input type="text" v-model="model.username" placeholder="输入用户名"/>            
            </x-form-item>
            <x-form-item class="x_mt32" label="确认密码" prop="password">
                <x-input type="password" v-model="model.password" placeholder="输入密码"/>
            </x-form-item>
            <x-form-item class="x_mt32">
                <button @click="submitForm('loginForm')">提交</button>
            </x-form-item>
        </x-form>
    </div>
</template>

<script>
    import XForm from '@/components/form/Form.vue'
    import XFormItem from '@/components/form/FormItem.vue'
    import XInput from '@/components/form/Input.vue'
    import Notice from "@/components/notice/notice"
    export default {
        data() {
            return {
                model: { username: "", password: "" },
                rules: {
                    username: [{ required: true, message: "请输入用户名" }],
                    password: [{ required: true, message: "请输入密码" }]
                }
            };
        },
        components: {
            XForm,
            XFormItem,
            XInput
        },
        methods: {
            submitForm(form) {
                this.$refs[form].validate(valid => {
                    if (valid){
                        const notice = this.$create(Notice, {
                            message: valid ? "请求登录!" : "校验失败!",
                            duration: 3000
                        });
                        notice.show();
                    }
                    
                });
            }
        }
    }
</script>

<style lang="less" scoped>
    // npm install less-loader --save-dev
    .x_mt32 {
        margin-top: 32px;
    }
</style>
