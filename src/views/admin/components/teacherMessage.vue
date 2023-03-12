<template>
    <div class="all">
        <div class="l-content">
            <el-input class="input" v-model="input" placeholder="请输入姓名"></el-input>
            <el-button class="button" type="primary" icon="el-icon-search">搜索</el-button>
        </div>
        <el-upload
                class="upload-demo"
                action="https://jsonplaceholder.typicode.com/posts/"
                :on-preview="handlePreview"
                :on-remove="handleRemove"
                :before-remove="beforeRemove"
                multiple
                :limit="3"
                :on-exceed="handleExceed"
                :on-success="handleSuccess"
                :file-list="fileList">
                <el-button type="primary">导入教师信息</el-button>
                <div slot="tip" class="el-upload__tip">只能上传Excel,且不超过500kb</div>
        </el-upload>
        <el-dialog
            title="信息编辑"
            :visible.sync="dialogVisible"
            width="50%"
            :before-close="handleClose">
            <el-form ref="form" :inline="true" :rules="rules" :model="form" label-width="80px">
                <el-form-item label="id" prop="id">
                    <el-input placeholder="请输入id" v-model="form.id"></el-input>
                </el-form-item>
                <el-form-item label="用户名" prop="username">
                    <el-input placeholder="请输入用户名" v-model="form.username"></el-input>
                </el-form-item>
                <el-form-item label="密码" prop="password">
                    <el-input placeholder="请输入密码" v-model="form.password"></el-input>
                </el-form-item>
            </el-form>
            <span slot="footer" class="dialog-footer">
                <el-button @click="cancel">取 消</el-button>
                <el-button @click="submit" type="primary" >确 定</el-button>
            </span>
        </el-dialog>
        <div class="table">
            <el-table
                :data="tableData"
                style="width: 100%">
                <el-table-column
                prop="id"
                label="id"
                width="180">
                </el-table-column>
                <el-table-column
                prop="username"
                label="用户名"
                width="180">
                </el-table-column>
               <el-table-column
                prop="password"
                label="密码"
                width="180">
                </el-table-column>
                <el-table-column
                prop="handle"
                label="操作">
                <template slot-scope="scope">
                    <el-button size="mini" @click="handleEdit(scope.row)">编辑</el-button>
                    <el-button type="danger" size="mini" @click="handleDelete(scope.row,scope.$index)">删除</el-button>
                </template>
                </el-table-column>
            </el-table>
        </div>
    </div>
        
</template>

<script>
    export default {
        name: 'studentMessage',
        data() {
            return {
                tableData: [
                    {id:7,username:'小明',password:123},
                    {id:8,username:'小红',password:123},
                    {id:9,username:'小黄',password:123},
                ],
                form: {
                    id: '',
                    username: '',
                    password: '',
                },
                dialogVisible: false,
                rules: {
                    id: [
                        { required: true, message: '请输入id' }
                    ],
                    username: [
                        { required: true, message: '请输入用户名' }
                    ],
                    password: [
                        { required: true, message: '请选择密码' }
                    ],
                },
                fileList:[],
                input: '',
            }
        },
        methods:{
            //取消
            cancel(){

            },
            //提交表单
            submit(){

            },
            //关闭表单
            handleClose(){

            },
            //编辑表单
            handleEdit(){
                //this.dialogVisible = true
            },
            //简易删除
            handleDelete(row,index){
                this.$confirm('此操作将永久删除该列, 是否继续?', '提示', {
                    confirmButtonText: '确定',
                    cancelButtonText: '取消',
                    type: 'warning'
                    }).then(() => {     
                        this.tableData.splice(index,1)                   
                        this.$message({
                            type: 'success',
                            message: '删除成功!'
                        });
                    })
            },
            //excel
            handleRemove(file, fileList) {
                console.log(file, fileList);
            },
            handlePreview(file) {
                console.log(file);
            },
            handleSuccess(response, file, fileList){
                console.log(response,file);

            },
            handleExceed(files, fileList) {
                this.$message.warning(`当前限制选择 3 个文件，本次选择了 ${files.length} 个文件，共选择了 ${files.length + fileList.length} 个文件`);
            },
            beforeRemove(file, fileList) {
                return this.$confirm(`确定移除 ${ file.name }？`);
            }, 
        }
    }
</script>

<style lang="less" scoped>
        .all{
        position: relative;
            .l-content{
                .input{
                width: 200px;
                margin: 20px 0 0 20px;
                }
                .button{
                        position: absolute;
                        top: 20px;
                        left: 215px;
                    }
                }
            .upload-demo{
                float: right;
                margin: -42px 20px 0 20px;
            }
            .table{
                margin: 100px 0 0 350px;
            }    
    }
</style>