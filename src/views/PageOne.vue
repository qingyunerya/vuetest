<template>
    <div>
        <el-table
                :data="tableData"
                border
                style="width: 500px">
            <el-table-column
                    fixed
                    prop="id"
                    label="id"
                    width="150">
            </el-table-column>
            <el-table-column
                    prop="name"
                    label="书名"
                    width="120">
            </el-table-column>
            <el-table-column
                    prop="author"
                    label="作者"
                    width="120">
            </el-table-column>
            <el-table-column
                    fixed="right"
                    label="操作"
                    width="100">
                <template slot-scope="scope">
                    <el-button @click="edit(scope.row)" type="text" size="small">修改</el-button>
                    <el-button @click="deleteBook(scope.row)" type="text" size="small">删除</el-button>
                </template>
            </el-table-column>
        </el-table>
        <el-pagination
                background
                layout="prev, pager, next"
                :total="total"
                @current-change="page"
        >
        </el-pagination>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                total:null,
                tableData: null
            }
        },
        methods: {
            edit(row) {
                this.$router.push({
                    path:'/bookUpdate',
                    query:{
                        id:row.id
                    }
                    }
                )
            },
            deleteBook(row){
                const _this= this
                axios.delete('http://localhost:8181/book/deleteById/'+row.id).then(function (resp) {
                    _this.$alert('《'+row.name+'》'+'删除成功', '消息', {
                        confirmButtonText: '确定',
                        callback: action => {
                            window.location.reload()
                        }
                    });
                })
            },
            page(currentPage){
                const _this= this
                axios.get('http://localhost:8181/book/findAll/'+currentPage+'/10').then(function (resp) {
                    _this.tableData=resp.data.content;
                    _this.total=resp.data.totalElements
                })
            }
        },
        created(){
            const _this= this;
            axios.get("http://localhost:8181/book/findAll/1/10").then(function (resp) {
                console.log(resp.data)
                _this.tableData=resp.data.content;
                _this.total=resp.data.totalElements

            })
        }
    }
</script>

<style scoped>

</style>
