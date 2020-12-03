<template>
  <div class="home-page">
    <div class="home-table">
      <div>
        <h1 class="table-title">数据展示</h1>
        <h1 class="table-buttun">
          <el-button size="mini" type="primary" icon="el-icon-plus" @click="dialogVisible = true">添加记录</el-button>
        </h1>
      </div>
      <el-table :data="datas" style="width: 90vw; position: absolute; left: 5vw;" height="80vh" border stripe>
        <el-table-column prop="name" label="名称">
        </el-table-column>
        <el-table-column prop="size" label="规格">
        </el-table-column>
        <el-table-column prop="factoryName" label="厂家名称">
        </el-table-column>
        <el-table-column prop="addDate" label="入库日期">
        </el-table-column>
        <el-table-column prop="addNum" label="入库数量">
        </el-table-column>
        <el-table-column prop="borrowDate" label="借出日期">
        </el-table-column>
        <el-table-column prop="borrowNum" label="借出数量">
        </el-table-column>
        <el-table-column prop="nowNum" label="剩余数量">
        </el-table-column>
        <el-table-column prop="borrowUserName" label="借用人">
        </el-table-column>
      </el-table>
    </div>
    <el-dialog
      title="添加记录" :visible.sync="dialogVisible" width="80%" :before-close="handleClose">
      <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
        <el-form-item label="名称" prop="name">
          <el-input v-model="ruleForm.name"></el-input>
        </el-form-item>
        <el-form-item label="规格" prop="size">
          <el-input v-model="ruleForm.size"></el-input>
        </el-form-item>
        <el-form-item label="厂家名称" prop="factoryName">
          <el-input v-model="ruleForm.factoryName"></el-input>
        </el-form-item>
        <el-form-item label="入库日期" prop="addDate">
          <el-input v-model="ruleForm.addDate"></el-input>
        </el-form-item>
        <el-form-item label="入库数量" prop="addNum">
          <el-input v-model="ruleForm.addNum"></el-input>
        </el-form-item>
        <el-form-item label="借出日期" prop="borrowDate">
          <el-input v-model="ruleForm.borrowDate"></el-input>
        </el-form-item>
        <el-form-item label="借出数量" prop="borrowNum">
          <el-input v-model="ruleForm.borrowNum"></el-input>
        </el-form-item>
        <el-form-item label="剩余数量" prop="nowNum">
          <el-input v-model="ruleForm.nowNum"></el-input>
        </el-form-item>
        <el-form-item label="借用人" prop="borrowUserName">
          <el-input v-model="ruleForm.borrowUserName"></el-input>
        </el-form-item>
      </el-form>
      <span slot="footer" class="dialog-footer">
        <el-button @click="dialogVisible = false">取 消</el-button>
        <el-button @click="resetForm('ruleForm')">重 置</el-button>
        <el-button type="primary" @click="addButton('ruleForm')">添 加</el-button>
      </span>
    </el-dialog>
  </div>
</template>

<script>

  import {datas} from "../assets/data/data"

  export default {
    name: "HomePage",
    data() {
      return {
        datas: [],
        dialogVisible: false,
        ruleForm: {
          name: "",
          size: "",
          factoryName: "",
          addDate: "",
          addNum: "",
          borrowDate: "",
          borrowNum: "",
          nowNum: "",
          borrowUserName: ""
        },
        rules: {
          name: [{required: true, message: '请输入名称', trigger: 'blur'}],
          size: [{required: true, message: '请输入规格', trigger: 'blur'}],
          factoryName: [{required: true, message: '请输入厂家名称', trigger: 'blur'}],
          addDate: [{required: true, message: '请输入入库日期', trigger: 'blur'}],
          addNum: [{required: true, message: '请输入入库数量', trigger: 'blur'}],
          borrowDate: [{required: true, message: '请输入借出日期', trigger: 'blur'}],
          borrowNum: [{required: true, message: '请输入借出数量', trigger: 'blur'}],
          nowNum: [{required: true, message: '请输入剩余数量', trigger: 'blur'}],
          borrowUserName: [{required: true, message: '请输入借用人', trigger: 'blur'}],
        },
      }
    },
    created() {
      this.datas = datas;
    },
    methods: {
      handleClose(done) {
        this.$confirm('确认关闭？')
          .then(res => {
            done();
          })
          .catch(err => {
            console.log(err)
          });
      },
      addButton(ruleForm){
        this.$refs[ruleForm].validate((valid) => {
          if (valid) {
            this.datas.unshift(this.ruleForm);
            console.log(this.ruleForm);
            this.dialogVisible = false;
          } else {
            console.log('error submit!!');
            return false;
          }
        });
      },
      resetForm(ruleForm) {
        this.$refs[ruleForm].resetFields();
      }
    }
  }
</script>

<style scoped>
  .home-table {
    width: 100vw;
    position: absolute;
    top: 2vh;
    left: 0;
  }

  .table-title {
    display: inline-block;
    margin-left: 5vw;
  }

  .table-buttun {
    display: inline-block;
    position: absolute;
    right: 5vw;
  }
</style>
