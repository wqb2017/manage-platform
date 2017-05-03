<template>
    <div class="list">
        <div class="button-right">
            <el-button type="primary" @click="editManage">新 增</el-button>
        </div>
        <el-table
            :data="tableData"
            style="width: 100%">
            <el-table-column
                prop="date"
                label="日期"
                width="180">
            </el-table-column>
            <el-table-column
                prop="name"
                label="姓名"
                width="180">
            </el-table-column>
            <el-table-column
                prop="address"
                label="地址">
            </el-table-column>
        </el-table>
        <el-dialog  v-model="dialogTableVisible">
            <el-form ref="formManifest" label-position="left" label-width="80px">
                <el-form-item label="日  期" prop="Date">
                    <el-date-picker></el-date-picker>
                </el-form-item>
                <el-form-item label="金  额" prop="Cost">
                    <el-input></el-input>
                </el-form-item>
                <el-form-item label="备  注" prop="Remark">
                    <el-input></el-input>
                </el-form-item>
                <el-form-item>
                    <el-button type="primary" @click="dialogTableVisible=false">确 定</el-button>
                    <el-button type="primary" @click="dialogTableVisible=false">取 消</el-button>
                </el-form-item>
            </el-form>
        </el-dialog>
    </div>
</template>
<script>
    export default {
        data() {
            return {
                dialogTableVisible:false,
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
            removeDomain(item) {
                var index = this.dynamicValidateForm.domains.indexOf(item)
                if (index !== -1) {
                    this.dynamicValidateForm.domains.splice(index, 1)
                }
            },
            addDomain() {
                this.dynamicValidateForm.domains.push({
                    value: '',
                    key: Date.now()
                });
            },
            editManage : function () {
                this.dialogTableVisible = true;
            }
        }
    }
</script>

<style>
    .button-right{
        float: right;
        margin-bottom:20px;
    }
</style>
