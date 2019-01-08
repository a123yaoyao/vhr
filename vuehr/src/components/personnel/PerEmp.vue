<template>
  <div>
    <el-header style="padding: 0px;display:flex;justify-content:space-between;align-items: center">
      <div style="display: inline">
        <el-input
          placeholder="通过员工名搜索员工,记得回车哦..."
          clearable
          @change="keywordsChange"
          style="width: 300px;margin: 0px;padding: 0px;"
          size="mini"


          prefix-icon="el-icon-search"
       >
        </el-input>
        <el-button type="primary" size="mini" style="margin-left: 5px" icon="el-icon-search" @click="searchEmp">搜索</el-button>
      </div>

    </el-header>
    <el-table
      :data="emps"  style="width: 100%">

      <el-table-column
        prop="name"
        align="left"
        fixed
        label="姓名"
        width="90">
      </el-table-column>
      <el-table-column
        prop="workID"
        width="85"
        align="left"
        label="工号">
      </el-table-column>
      <el-table-column
        prop="gender"
        label="性别"
        width="50">
      </el-table-column>
<!--      <el-table-column
        width="85"
        align="left"
        label="出生日期">
        <template slot-scope="scope">{{ scope.row.birthday | formatDate}}</template>
      </el-table-column>-->
      <el-table-column
        prop="idCard"
        width="150"
        align="left"
        label="身份证号码">
      </el-table-column>
      <el-table-column
        prop="wedlock"
        width="70"
        label="婚姻状况">
      </el-table-column>
      <el-table-column
        width="50"
        prop="nation.name"
        label="民族">
      </el-table-column>
      <!--<el-table-column
        prop="nativePlace"
        width="80"
        label="籍贯">
      </el-table-column>
      <el-table-column
        prop="politicsStatus.name"
        label="政治面貌">
      </el-table-column>
      <el-table-column
        prop="email"
        width="180"
        align="left"
        label="电子邮件">
      </el-table-column>-->
     <!-- <el-table-column
        prop="phone"
        width="100"
        label="电话号码">
      </el-table-column>
      <el-table-column
        prop="address"
        width="220"
        align="left"
        label="联系地址">
      </el-table-column>
      <el-table-column
        prop="department.name"
        align="left"
        width="100"
        label="所属部门">
      </el-table-column>-->
    </el-table>
  </div>
</template>
<script>

  export default {
    data(){
      return {
        emps: [],
        emp: {
          name: '',
          gender: 'xxxxxxxxxxxxxxxx',
          birthday: '',
          idCard: '',
          wedlock: '',

        },


      }
    },
    methods:{
      loadEmps(){
        var _this = this;
        this.tableLoading = true;
        this.getRequest("/employee/basic/emp?page=1&size=10&keywords=&politicId=&nationId=&posId=&jobLevelId=&engageForm=&departmentId=&beginDateScope=").then(resp=> {
          this.tableLoading = false;
          if (resp && resp.status == 200) {
            var data = resp.data;
            _this.emps = data.emps;


          }
        })
      },
      keywordsChange(val){
        if (val == '') {
          this.loadEmps();
        }
      },
      searchEmp(){
        this.loadEmps();
      },
    },
    mounted: function () {
      this.loadEmps();
    },
  }
</script>
