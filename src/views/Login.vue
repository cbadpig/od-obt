<template>
    <div class="main">
        <div class="Login">
            <div class="login-title">证券业从业资格考试</div>
            <div class="login-form">
                <div class="login-kc-title">{{formValidate.kcmc}}</div>
                <Form ref="formValidate" :model="formValidate" :rules="ruleValidate" :label-width="90">
                    <FormItem label="准考证号：" prop="zkzh">
                        <Input v-model="formValidate.zkzh" size="small"/>
                    </FormItem>
                    <FormItem  label="证件编码：" prop="zjbm">
                        <Input v-model="formValidate.zjbm" size="small"/>
                    </FormItem>
                    <FormItem class="login-form-button">
                        <Button type="primary" @click="handleSubmit('formValidate')">登录</Button>
                        <Button @click="handleReset('formValidate')" style="margin-left: 8px">重置</Button>
                    </FormItem>
                </Form>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "Login",
        data() {
            const validateZkzh = (rule, value, callback) => {
                if (value === '') {
                    callback(new Error('请输入准考账号'));
                } else {

                    callback();
                }
            };
            const validateZjbm = (rule, value, callback) => {
                if (value === '') {
                    callback(new Error('请输入证件编码'));
                } else {

                    callback();
                }
            };
            return {
                formValidate:{
                    zkzh:'',
                    zjbm:'',
                    kcmc:'考场1'
                },
                ruleValidate:{
                    zkzh:[{validator:validateZkzh, trigger: 'blur'}],
                    zjbm:[{validator:validateZjbm, trigger: 'blur'}]
                }
            }
        },
        methods: {
            handleSubmit(name) {
                console.log(this.formValidate);
                this.$refs[name].validate((valid) => {
                    if (valid) {
                        this.$Message.success('成功!');
                    } else {
                        this.$Message.error('失败!');
                    }
                })
            },
            handleReset(name) {
                this.$refs[name].resetFields();
            }
        },
        computed: {

        }
    }
</script>
<style>
    body {
        background-color: #2d6dae;
        overflow: hidden;
        font-family:"宋体";
    }
</style>
<style scoped>
    .main {
        width:768px;
        height: calc(100vh - 60px);
        max-height: 1024px;
        min-height: 400px;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translateY(-50%) translateX(-50%);
        background-image: url("../assets/images/back.gif");
    }
    .Login {
        width: 526px;
        height: 291px;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translateY(-50%) translateX(-50%);
        background-image: url("../assets/images/login.png");
    }
    .login-title {
        margin-top:20px;
        text-align: center;
        height:50px;
        line-height: 50px;
        color: #2d6dae;
        font-size: 21px;
        font-weight: bold;
        letter-spacing: 4px;

    }
    .login-form {
        width:290px;
        margin-left:180px;
    }
    .login-kc-title {
        text-align: center;
        color: red ;
        font-weight: bold;
        font-size: 26px;
        margin-top: 6px;
    }
    .ivu-form >>> .ivu-form-item-label {
        color:#000000 !important;
    }
    .ivu-form >>> .ivu-form-item-error-tip {
        font-size: 12px;
        padding-top: 0;
    }
    .ivu-form >>> .ivu-form-item {
        margin-bottom: 10px;
    }
    .login-form-button {
        margin-top: 22px;
    }

</style>