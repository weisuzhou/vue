
<template>
  <div style="padding:10px">
    <div style="margin: 10px 0">
      <el-button type="primary" @click="add">新增</el-button>
      <el-button type="primary">导入</el-button>
      <el-button type="primary">导出</el-button>
    </div>
    <div style="margin: 10px 0">
      <el-input v-model="search" placeholder="Please input nickname" style="width: 300px" clearable />
      <el-button type="primary" style="margin-left: 5px" @click="load">查询</el-button>
    </div>
  <el-table :data="tableData" border stripe style="width: 100%">
    <el-table-column fixed prop="id" label="ID" sortable/>
    <el-table-column prop="username" label="用户名" />
    <el-table-column prop="nickname" label="昵称" />
    <el-table-column prop="age" label="年龄"  />
    <el-table-column prop="sex" label="性别" />
    <el-table-column prop="address" label="联系方式"  />
    <el-table-column fixed="right" label="操作" >
      <template #default="scope">
        <el-button  size="mini" type="primary" @click="handleEdit(scope.row)">编辑</el-button>
        <el-popconfirm title="Are you sure to delete this?" @confirm="handleDelete(scope.row.id)">
          <template #reference>
            <el-button type="danger" size="mini">删除</el-button>
          </template>
        </el-popconfirm>


      </template>
    </el-table-column>
  </el-table>
    <div style="margin: 10px 0">
      <el-pagination
          v-model:currentPage="currentPage"
          :page-sizes="[5, 10, 15, 20]"
          :page-size="pageSize"
          layout="total, sizes, prev, pager, next, jumper"
          :total="total"
          @size-change="handleSizeChange"
          @current-change="handleCurrentChange"
      >
      </el-pagination>

      <el-dialog
          v-model="dialogVisible"
          title="Tips"
          width="30%">
       <el-form :model="form" label-width="120px">
         <el-form-item label="用户名">
           <el-input v-model="form.username" style="width:80%"></el-input>
         </el-form-item>
         <el-form-item label="昵称">
           <el-input v-model="form.nickname" style="width:80%"></el-input>
         </el-form-item>
         <el-form-item label="年龄">
           <el-input v-model="form.age" style="width:80%"></el-input>
         </el-form-item>
         <el-form-item label="性别">
           <el-radio v-model="form.sex" label="男">男</el-radio>
           <el-radio v-model="form.sex" label="女">女</el-radio>
           <el-radio v-model="form.sex" label="未知">未知</el-radio>
         </el-form-item>
         <el-form-item label="联系方式">
           <el-input type="textarea" v-model="form.address" style="width:80%"></el-input>
         </el-form-item>



       </el-form>
        <template #footer>
      <span class="dialog-footer">
        <el-button @click="dialogVisible = false">Cancel</el-button>
        <el-button type="primary" @click="save">Confirm</el-button>
      </span>
        </template>
      </el-dialog>

    </div>
    </div>
</template>

<script>
import request from "../utils/request";

export default {
  name:'Home',
  components:{

  },
  data() {
    return {
      form:{},
      search:'',
      dialogVisible:false,
      currentPage:1,
      pageSize:10,
      total:0,
      tableData: [
      ],
    }
  },
  created() {
    this.load()
  },
  methods: {
    load(){
      request.get("/api/user",{
       params:{ pageNum:this.currentPage,
        pageSize:this.pageSize,
        search:this.search
       }
      }).then(res=>{
        console.log(res)
        this.tableData=res.data.records
        this.total=res.data.total
      })
    },
    add(){
      this.dialogVisible=true
      this.form={}
    },
    handleEdit(row) {
      this.form=JSON.parse(JSON.stringify(row))
      this.dialogVisible=true
    },
    handleSizeChange(pageSize){
      this.pageSize=pageSize
       this.load()
    },
    save(){
      if(this.form.id){
        request.put("/api/user",this.form).then(res=>{
          console.log(res)
          if(res.code==='0')
          {
          this.$message({
            type:"success",
            message:"更新成功"
          })
          }
      else {
            this.$message({
              type:"error",
              message:res.msg
            })
          }
      this.load()
          this.dialogVisible=false
        })
      }

      else{
        request.post("/api/user",this.form).then(res=>{
          console.log(res)
          if(res.code==='0')
          {
            this.$message({
              type:"success",
              message:"新增成功"
            })
          }
          else {
            this.$message({
              type:"error",
              message:res.msg
            })
          }
          this.load()
          this.dialogVisible=false
      })
       }
    },
    handleDelete(id){
      console.log(id)
      request.delete("/api/user/"+id).then(res=>{
        if(res.code==='0')
        {
          this.$message({
            type:"success",
            message:"删除成功"
          })
        }
        else {
          this.$message({
            type:"error",
            message:res.msg
          })
        }
        this.load()
      })
    },
    handleCurrentChange(pageNum){
      this.pageNum=pageNum
        this.load()
    },
  },
}
</script>