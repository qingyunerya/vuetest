<template>
    <div>
        <el-form style="width: 60%" :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px"  class="demo-ruleForm">
            <el-form-item label="书名" prop="name">
                <el-input v-model="ruleForm.name"></el-input>
            </el-form-item>
            <el-form-item label="作者" prop="author">
                <el-input v-model="ruleForm.author"></el-input>
            </el-form-item>
            <el-form-item>
                <el-button type="primary" @click="submitForm('ruleForm')">立即创建</el-button>
                <el-button @click="resetForm('ruleForm')">重置</el-button>
                <el-button @click="test()">test</el-button>
            </el-form-item>
        </el-form>
    </div>

</template>

<script>

    export default {
        name: "PageOne",
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
                        axios.post("http://localhost:8181/book/add",_this.ruleForm).then(function () {
                            // _this.$message({
                            //     message: '恭喜你，这是一条成功消息',
                            //     type: 'success'
                            // });
                            _this.$alert('《'+_this.ruleForm.name+'》'+'添加成功', '消息', {
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
