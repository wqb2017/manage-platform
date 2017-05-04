<template>
    <div class="list">
        <div class="button-right">
            <el-button type="primary" @click="editManage">新 增</el-button>
        </div>
        <el-table :data="tableData" style="width: 100%">
            <el-table-column prop="date" label="日期" width="180"></el-table-column>
            <el-table-column prop="name"  label="姓名"  width="180"></el-table-column>
            <el-table-column prop="address"  label="地址"> </el-table-column>
        </el-table>
        <div class="block">
            <el-pagination layout="prev, pager, next" :total="50"></el-pagination>
        </div>
        <el-dialog v-model="dialogTableVisible">
            <el-form :model="dynamicValidateForm" ref="dynamicValidateForm" label-width="100px" class="demo-dynamic">
                <el-form-item
                    prop="email"
                    label="邮箱"
                    :rules="[{ required: true, message: '请输入邮箱地址', trigger: 'blur' },
                            { type: 'email', message: '请输入正确的邮箱地址', trigger: 'blur,change' }]">
                    <el-input v-model="dynamicValidateForm.email"></el-input>
                </el-form-item>
                <el-form-item
                    v-for="(domain, index) in dynamicValidateForm.domains"
                    :label="'域名' + index"
                    :key="domain.key"
                    :prop="'domains.' + index + '.value'"
                    :rules="{ required: true, message: '域名不能为空', trigger: 'blur' }" >
                    <el-input v-model="domain.value"></el-input></el-form-item>
                <el-form-item>
                    <el-button type="primary" @click="submitForm('dynamicValidateForm')">提交</el-button>
                    <el-button @click="addDomain">新增域名</el-button>
                    <el-button @click="resetForm('dynamicValidateForm')">重置</el-button>
                </el-form-item>
            </el-form>
        </el-dialog>
        <user-info></user-info>
    </div>
</template>
<script>
    import UserInfo from "./UserInfo.vue";
    export default {
        data() {
            return {
                dialogTableVisible: false,
                tableData: [{
                    date: '2016-05-02',
                    name: '王小虎',
                    address: '上海市普陀区金沙江路 1518 弄'
                }, {
                    date: '2016-05-04',
                    name: '王小虎',
                    address: '上海市普陀区金沙江路 1517 弄'
                }, {
                    date: '2016-05-01',
                    name: '王小虎',
                    address: '上海市普陀区金沙江路 1519 弄'
                }, {
                    date: '2016-05-03',
                    name: '王小虎',
                    address: '上海市普陀区金沙江路 1516 弄'
                }],
                dynamicValidateForm: {
                    domains: [{
                        value: ''
                    }],
                    email: ''
                }
            }
        },
        methods: {
            submitForm(formName) {
                this.$refs[formName].validate((valid) => {
                    if (valid) {
                        alert('submit!');
                    } else {
                        console.log('error submit!!');
                        return false;
                    }
                });
            },
            resetForm(formName) {
                this.$refs[formName].resetFields();
            },
            addDomain() {
                this.dynamicValidateForm.domains.push({
                    value: '',
                    key: Date.now()
                });
            },
            editManage: function () {
                this.dialogTableVisible = true;
            }
        },
        components:{
            'user-info':UserInfo
        }
    }
</script>
<style>
    .button-right {
        float: right;
        margin-bottom:20px;
    }
</style>
