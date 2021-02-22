<template>
    <el-form style="width: 60%" :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px"  class="demo-ruleForm">
        <el-form-item label="书名" prop="name">
            <el-input v-model="ruleForm.name"></el-input>
        </el-form-item>
        <el-form-item label="作者" prop="author">
            <el-input v-model="ruleForm.author"></el-input>
        </el-form-item>
        <el-form-item>
            <el-button type="primary" @click="submitForm('ruleForm')">立即修改</el-button>
            <el-button @click="resetForm('ruleForm')">重置</el-button>
            <el-button @click="test()">test</el-button>
        </el-form-item>
    </el-form>
</template>

<script>
    export default {
        name: "PageThree",
        data() {
            return {
                ruleForm: {
                    name: '',
                    author: '',
                },
                rules: {
                    name: [
                        { required: true, message: '请输入书名', trigger: 'blur' },
                    ],
                    author: [
                        { required: true, message: '请选择书作者', trigger: 'change' }
                    ],
                }
            };
        },
        methods: {
            submitForm(formName) {
                const _this =this;
                this.$refs[formName].validate((valid) => {
                    if (valid) {
                        // console.log(this.ruleForm);
                        axios.post("http://localhost:8181/book/update",_this.ruleForm).then(function () {
                            _this.$alert('修改成功', '消息', {
                                confirmButtonText: '确定',
                                callback: action => {
                                    _this.$router.push('/')
                                }
                            });
                        })
                    }
                });
            },
            resetForm(formName) {
                this.$refs[formName].resetFields();
            },
            test(){
                const _this =this;
                alert(this.ruleForm.author+this.ruleForm.author)
            }
        }
    }
</script>

<style scoped>

</style>
