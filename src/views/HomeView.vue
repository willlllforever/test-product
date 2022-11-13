<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <div class="formDialog">
      <el-dialog :title="dialogType == 'add' ? '新增用户' : '更新用户'" :visible.sync="dialogFormVisible">
        <custom-form
          :form="form"
          :formOption="formOption"
          :inline="inline"
          :rules="rules"
        ></custom-form>
        <!-- <el-form :model="form">
          <el-form-item label="活动名称" :label-width="formLabelWidth">
            <el-input v-model="form.name" autocomplete="off"></el-input>
          </el-form-item>
          <el-form-item label="活动区域" :label-width="formLabelWidth">
            <el-select v-model="form.region" placeholder="请选择活动区域">
              <el-option label="区域一" value="shanghai"></el-option>
              <el-option label="区域二" value="beijing"></el-option>
            </el-select>
          </el-form-item>
        </el-form>
        <div slot="footer" class="dialog-footer">
          <el-button @click="dialogFormVisible = false">取 消</el-button>
          <el-button type="primary" @click="dialogFormVisible = false">确 定</el-button>
        </div> -->
      </el-dialog>
    </div>
    <el-button class="adduser" type="primary" @click="addUser">新增</el-button>
    <el-table
      :data="tableData"
      border
      style="width: 100%">
      <el-table-column
        v-for="item in tableLabel"
        :key="item.props"
        :prop="item.props"
        :label="item.label"
        :width="item.width ? item.width : ''">
      </el-table-column>
      <el-table-column
        label="操作"
        width="150">
        <template slot-scope="scope">
          <el-button @click="handleClick(scope.row)" type="primary" size="small">编辑</el-button>
          <el-button type="danger" size="small">删除</el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
import CustomForm from '@/components/CustomForm.vue';
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'HomeView',
  components: {
    CustomForm
    
  },
  data() {
    return {
      dialogFormVisible: false,
      dialogType: 'add',
      tableData: [{
        date: '2016-05-02',
        name: '王小虎',
        province: '上海',
        city: '普陀区',
        address: '上海市普陀区金沙江路 1518 弄',
        zip: 200333
      }, {
        date: '2016-05-04',
        name: '王小虎',
        province: '上海',
        city: '普陀区',
        address: '上海市普陀区金沙江路 1517 弄',
        zip: 200333
      }, {
        date: '2016-05-01',
        name: '王小虎',
        province: '上海',
        city: '普陀区',
        address: '上海市普陀区金沙江路 1519 弄',
        zip: 200333
      }, {
        date: '2016-05-03',
        name: '王小虎',
        province: '上海',
        city: '普陀区',
        address: '上海市普陀区金沙江路 1516 弄',
        zip: 200333
      }],
      tableLabel: [{
        props: 'date',
        label: '日期',
        width: 150
      },{
        props: 'name',
        label: '姓名'
      },{
        props: 'province',
        label: '省份'
      },{
        props: 'city',
        label: '市区'
      },{
        props: 'address',
        label: '地址',
        width: 300
      },{
        props: 'zip',
        label: '邮编'
      }],

      inline: true,
      form: {
        id: '',
        name: '',
        phone: '',
        company: '',
        origin: '',
        level: '',
        remarks: '',
        province: '',
        address: ''
      },
      formOption: [{
        label: 'ID',
        type: 'input',
        model: 'id'
      },{
        label: '客户名称',
        type: 'input',
        model: 'name'
      },{
        label: '手机号码',
        type: 'input',
        model: 'phone'
      },{
        label: '公司名称',
        type: 'input',
        model: 'company',
        required: true
      },{
        label: '客户来源',
        type: 'input',
        model: 'origin'
      },{
        label: '客户级别',
        type: 'select',
        model: 'level',
        option: ['重点客户','普通客户'],
        required: true
      },{
        label: '备注',
        type: 'textarea',
        model: 'remarks'
      },{
        label: '省市区',
        type: 'input',
        model: 'province'
      },{
        label: '详细地址',
        type: 'input',
        model: 'address'
      }],
      rules: {
        id: [
            { required: true, message: '请输入ID', trigger: 'blur' },
            { min: 3, max: 5, message: '长度在 3 到 5 个字符', trigger: 'blur' }
        ],
        phone: [
            { required: true, message: '请输入手机号码', trigger: 'blur' },
            { type: 'number' }
        ],
        company: [
            { required: true, message: '请输入公司名称', trigger: 'blur' },
            { min: 5, max: 15, message: '长度在 5 到 15 个字符', trigger: 'blur' }
        ],
        level: [
            { required: true, message: '请选择客户级别', trigger: 'blur' },
        ],
      }
    }
  },
  methods: {
    handleClick(row) {
      console.log(row);
      this.dialogFormVisible = true,
      this.dialogType = 'edit'
    },
    addUser() {
      this.dialogFormVisible = true
      this.dialogType = 'add'
    }
  }
}
</script>
<style lang="scss" scoped>
  .el-button.adduser{
    margin-bottom: 1rem;
  }
</style>