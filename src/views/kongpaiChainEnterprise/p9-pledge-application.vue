<template>
  <div class="sub-content-box">
    <div class="sub-content-header">
      <div class="sub-content-title-left">
        <div class="sub-content-title-left-title">碳配额质押申请  </div>
  
      </div>
    </div>

    <div class="sub-content-body">
      <div class="description-title">
        <div class="table-rec"></div>
       申请表单
      </div>
      <div class="form-body">
        <el-row :gutter="40">
          <el-col :span="10">
            <el-form
              :label-position="labelPositionForm"
              label-width="80px"
              :model="formLabelAlign"
            >
              <el-form-item label="配额所有者">
                <el-input
                  placeholder="某控排链企业"
                  v-model="formLabelAlign.kongpai"
                ></el-input>
              </el-form-item>
               <el-form-item label="所属控排链">
                <el-input
                  placeholder="某控排链"
                  v-model="formLabelAlign.kongpai"
                ></el-input>
              </el-form-item>
              <el-form-item label="质押金额">
                <el-input
                  placeholder="￥￥￥￥￥"
                  v-model="formLabelAlign.sendername"
                ></el-input>
              </el-form-item>
              <el-form-item label="贷款期限">
                <el-input
                  placeholder="180天"
                  v-model="formLabelAlign.tradeAmount"
                ></el-input>
              </el-form-item>
              
            </el-form>
          </el-col>
          <el-col :span="10">
            <el-form
              :label-position="labelPositionForm"
              label-width="80px"
              :model="formLabelAlign"
            >
              <el-form-item label="操作日期">
                <el-date-picker
                  v-model="formLabelAlign.launchedDate"
                  type="date"
                  placeholder="选择日期"
                >
                </el-date-picker>
              </el-form-item>
              <el-form-item label="配额量">
                <el-input
                  placeholder="￥￥￥￥￥"
                  v-model="formLabelAlign.carbonCreditBalance"
                ></el-input>
              </el-form-item>
               <el-form-item label="质押率">
                <el-input
                  placeholder="1.4%"
                  v-model="formLabelAlign.carbonCreditBalance"
                ></el-input>
              </el-form-item>
              <el-form-item label="质押率">
                <el-input
                  placeholder="1.4%"
                  v-model="formLabelAlign.carbonCreditBalance"
                ></el-input>
              </el-form-item>
            </el-form>
          </el-col>
        </el-row>
      </div>

      
      <div class="sub-content-submit-button">
          
        <el-button class="button-style" @click="dialogVisible=true">提交</el-button>
      </div>

      <!-- 提交弹出操作密码面板 -->
      <el-dialog title="操作密码" :visible.sync="dialogVisible" width="30%">
        <el-form
          :model="ruleForm"
          status-icon
          :rules="rules"
          ref="ruleForm"
          label-width="100px"
          class="demo-ruleForm"
        >
          <el-form-item label="密码" prop="pass">
            <el-input
              type="password"
              v-model="ruleForm.pass"
              autocomplete="off"
            ></el-input>
          </el-form-item>
          <el-form-item>

              <el-popover
            placement="right"
            width="160"
            v-model="visible">
            <p>确认</p>
            <div style="text-align: right; margin: 0">
                <el-button size="mini" type="text" @click="visible = false">取消</el-button>
                <el-button type="primary" size="mini" @click="visible = false">确定</el-button>
            </div>
            <el-button slot="reference" type="primary" @click="submitForm('ruleForm', formLabelAlign)">
                            提交
                        </el-button>
            </el-popover>
           
          </el-form-item>
        </el-form>
      </el-dialog>
      <!-- 操作密码面板结束 -->
    </div>
  </div>
</template>
<script>
export default {
  data() {
    var validatePass = (rule, value, callback) => {
      if (value === "") {
        callback(new Error("请输入密码"));
      } else {
        if (this.ruleForm.checkPass !== "") {
          this.$refs.ruleForm.validateField("checkPass");
        }
        callback();
      }
    };
    return {
      active: 1,
      textarea: "",
      dialogVisible:false,
      labelPositionTabs: "right",
      labelPositionForm: "top",
      formLabelAlign: {
        kongpai: "",
        sendername: "",
        tradeAmount: "",
        launchedDate: "",
        carbonCreditBalance: "",
        tradingDescription: "",
        receivername: "",
        jianpai: "",
      },
      ruleForm: {
        pass: "",
      },
      rules: {
        pass: [{ validator: validatePass, trigger: "blur" }],
      },
    };
  },
  methods: {
    submitForm(formName,formLabelAlign){
            

            console.log(formLabelAlign)

            this.$refs[formName].validate((valid) => {

            if (valid) {//操作密码正确
                this.dialogVisible=false
                 this.$message({
                    message: '操作成功',
                    type: 'success'
                });


            } else {//操作密码不正确
                console.log('error submit!!');
                return false;
            }
            });
      },
  },
};
</script>
<style scoped>
.sub-content-body {
  background: #fff;
  margin: 20px 40px 40px;
  border-radius: 25px;
}
.form-body {
  margin: 20px 40px 0px;
}
.description-title {
  padding-top: 20px;
  margin-left: 40px;
  line-height: 30px;
}
.description-title .table-rec {
  float: left;
  width: 4px;
  height: 30px;
  border-radius: 50px;
  background-color: #f2a626;
  margin-right: 10px;
}
::v-deep .el-descriptions {
  padding: 10px 40px;
}
/* ::v-deep .el-form-item {
  margin-bottom: 10px;
} */
::v-deep .el-form-item__label {
  line-height: 14px;
}
::v-deep .el-form--label-top .el-form-item__label {
  padding: 0 0 5px;
}
::v-deep .el-input__inner {
  border-radius: 5px;
  height: 35px;
  background-color: #fafcfe;
}
::v-deep .el-input__icon {
  height: 0;
}
::v-deep .el-input--suffix .el-input__inner {
  margin: 0;
}
.el-date-editor.el-input,
.el-date-editor.el-input__inner {
  width: 100%;
}
.sub-content-submit-button {
  /* height: 33px; */
  margin: 20px 40px 40px;
  padding-bottom: 40px;
}
/* .sub-content-submit-button .el-button {
  margin: 0;
} */
.sub-content-submit-button .button-style {
  padding: 0;
  margin-right: 20px;
  width: 100px;
  font-size: 14px;
  line-height: 33px;
  height: 33px;
  border-radius: 7px;
  transition: 0.1s;
  border: none;
  text-align: center;
  box-sizing: border-box;
  background: #209f85;
  color: #fff;
}
.button-style:hover {
  background: transparent;
  border: 1px solid #209f85;
  color: #209f85;
  cursor: pointer;
}
</style>
