<template>
    <div class="form">
        <!-- 登录的表单 -->
        <!-- this.$refs.form -->
        <el-form :rules="rules" ref="form" :model="form">
            <!-- 用户名 -->
            <el-form-item prop="username">
                <el-input 
                placeholder="用户名/手机"
                v-model="form.username">
                </el-input>
            </el-form-item>

             <!-- 密码 -->
            <el-form-item prop="password">
                <el-input 
                placeholder="密码" 
                type="password"
                v-model="form.password"
                ></el-input>
            </el-form-item>

            <el-button 
            type="primary" 
            class="submit"
            @click="handleSubmit">
            登录
            </el-button>
        </el-form>

    </div>
</template>

<script>
export default {
    data(){
        return {
            form: {
                username: "",
                password: ""
            },

            // 表单的验证规则
            rules: {
                username: [
                    { required: true, message: '请输入手机号码', trigger: 'blur' },
                ],
                password: [
                    { required: true, message: '请输入密码', trigger: 'blur' },
                ],
            }
        }
    },

    methods: {
        // 登录提交
        handleSubmit(){

            // 验证表单
            this.$refs.form.validate( valid => {
                if(valid){             
                    // 调用actions
                    this.$store.dispatch("user/login", this.form).then(v => {
                        this.$message.success("登录成功，正在跳转...");

                        setTimeout(() => {
                            this.$router.push("/");
                        }, 1000);
                    });
                }
            })
        }
    },

    mounted(){
        // this.$store.commit()
        // this.$store.dispatch("user/login", {});
    }
}
</script>

<style scoped lang="less">
    .form{
        padding:25px;
    }

    .submit{
        display:block;
        width:100%;
    }
</style>
