<template>
    <div>
        <el-form style="width: 60%" :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px"  class="demo-ruleForm">
            <el-form-item label="编号" prop="id">
                <el-input v-model="ruleForm.id" readonly></el-input>
            </el-form-item>
            <el-form-item label="书名" prop="name">
                <el-input v-model="ruleForm.name"></el-input>
            </el-form-item>
            <el-form-item label="作者" prop="author">
                <el-input v-model="ruleForm.author"></el-input>
            </el-form-item>
            <el-form-item>
                <el-button type="primary" @click="submitForm('ruleForm')">立即修改</el-button>
                <el-button @click="resetForm('ruleForm')">重置</el-button>
            </el-form-item>
        </el-form>
    </div>
</template>

<script>

    export default {
        name: "bookUpdate",
        data() {
            return {
                ruleForm: {
                    id:'',
                    name: '',
                    author: '',
                },
                rules: {
                    id: [
                        { required: true},
                    ],
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
                        axios.post("http://localhost:8181/book/add",_this.ruleForm).then(function (resp) {
                            // _this.$message({
                            //     message: '恭喜你，这是一条成功消息',
                            //     type: 'success'
                            // });
                            if(resp.data!=null){
                                _this.$alert('《'+_this.ruleForm.name+'》'+'修改成功', '消息', {
                                    confirmButtonText: '确定',
                                    callback: action => {
                                        _this.$router.push('/')
                                    }
                                });
                            }
                        })
                    }
                });
            },
            resetForm(formName) {
                this.$refs[formName].resetFields();
            }
        },
        created(){
            console.log(''+this.$route.id);
            const _this = this
            axios.get('http://localhost:8181/book/findById/'+this.$route.query.id).then(function (resp) {
                console.log(resp.data)
                _this.ruleForm=resp.data
            })
        }
    }
</script>

<style scoped>

</style>
