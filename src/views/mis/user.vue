<template>
  <div class="user-management">
    <!-- 搜索表单 -->
    <el-form :inline="true" :model="searchForm" class="search-form">
      <el-form-item label="姓名">
        <el-input v-model="searchForm.name" placeholder="请输入姓名"></el-input>
      </el-form-item>
      <el-form-item label="性别">
        <el-select v-model="searchForm.gender" placeholder="请选择性别">
          <el-option label="男" value="男"></el-option>
          <el-option label="女" value="女"></el-option>
        </el-select>
      </el-form-item>
      <el-form-item label="角色">
        <el-select v-model="searchForm.role" placeholder="请选择角色">
          <el-option label="管理员" value="管理员"></el-option>
          <el-option label="普通用户" value="普通用户"></el-option>
        </el-select>
      </el-form-item>
      <el-form-item label="部门">
        <el-input v-model="searchForm.department" placeholder="请输入部门"></el-input>
      </el-form-item>
      <el-form-item label="状态">
        <el-select v-model="searchForm.status" placeholder="请选择状态">
          <el-option label="在职" value="在职"></el-option>
          <el-option label="离职" value="离职"></el-option>
        </el-select>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="onSearch">查询</el-button>
        <el-button @click="onReset">重置</el-button>
      </el-form-item>
    </el-form>

    <!-- 操作按钮 -->
    <div class="btn-group">
      <el-button type="primary" @click="openDialog('add')">新增</el-button>
      <el-button type="danger" @click="handleDeleteBatch">批量删除</el-button>
    </div>

    <!-- 人员信息表格 -->
    <el-table :data="tableData" stripe style="width: 100%">
      <el-table-column type="selection" width="55"></el-table-column>
      <el-table-column prop="id" label="序号" width="70"></el-table-column>
      <el-table-column prop="name" label="姓名" min-width="120"></el-table-column>
      <el-table-column prop="gender" label="性别" min-width="80"></el-table-column>
      <el-table-column prop="phone" label="电话" min-width="120"></el-table-column>
      <el-table-column prop="email" label="邮箱" min-width="180"></el-table-column>
      <el-table-column prop="entryDate" label="入职日期" min-width="120"></el-table-column>
      <el-table-column prop="role" label="角色" min-width="150"></el-table-column>
      <el-table-column prop="department" label="部门" min-width="150"></el-table-column>
      <el-table-column prop="status" label="状态" min-width="80"></el-table-column>
      <el-table-column label="操作" min-width="150">
        <template v-slot="scope">
          <!-- 修改按钮 -->
          <el-button type="link" @click="openDialog('edit', scope.row)">修改</el-button>
          <!-- 删除按钮 -->
          <el-button type="link" @click="handleDelete(scope.row)">删除</el-button>
        </template>
      </el-table-column>
    </el-table>

    <!-- 分页组件 -->
    <el-pagination
      background
      layout="total, prev, pager, next"
      :total="total"
      :page-size="pageSize"
      @current-change="handlePageChange"
    ></el-pagination>

    <!-- 新增/修改用户的弹窗 -->
    <el-dialog :title="dialogTitle" :visible.sync=true width="500px">
      <el-form :model="formData">
        <el-form-item label="用户名" required>
          <el-input v-model="formData.username"></el-input>
        </el-form-item>
        <el-form-item label="姓名" required>
          <el-input v-model="formData.name"></el-input>
        </el-form-item>
        <el-form-item label="性别" required>
          <el-select v-model="formData.gender" placeholder="请选择性别">
            <el-option label="男" value="男"></el-option>
            <el-option label="女" value="女"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="电话" required>
          <el-input v-model="formData.phone"></el-input>
        </el-form-item>
        <el-form-item label="邮箱" required>
          <el-input v-model="formData.email"></el-input>
        </el-form-item>
        <el-form-item label="入职日期" required>
          <el-date-picker v-model="formData.entryDate" type="date" placeholder="选择日期"></el-date-picker>
        </el-form-item>
        <el-form-item label="角色" required>
          <el-select v-model="formData.role" multiple placeholder="请选择角色">
            <el-option label="超级管理员" value="超级管理员"></el-option>
            <el-option label="总经理" value="总经理"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="部门" required>
          <el-input v-model="formData.department"></el-input>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogVisible = false">取消</el-button>
        <el-button type="primary" @click="submitForm">确定</el-button>
      </div>
    </el-dialog>

  </div>
</template>

<script>
export default {
  data() {
    return {
      searchForm: {
        name: '',
        gender: '',
        role: '',
        department: '',
        status: ''
      },
      tableData: [
        { id: 1, name: '超级管理员', gender: '男', phone: '13312345678', email: 'admin@163.com', entryDate: '2023-03-15', role: '总经理, 超级管理员', department: '总经理办公室', status: '在职' },
        { id: 2, name: '李四', gender: '女', phone: '13312346789', email: 'lisi@163.com', entryDate: '2023-01-05', role: '管理员', department: '技术部', status: '在职' }
      ],
      total: 10,
      pageSize: 10,
      dialogVisible: true,
      dialogTitle: '',
      formData: {
        username: '',
        name: '',
        gender: '',
        phone: '',
        email: '',
        entryDate: '',
        role: [],
        department: ''
      },
      formType: '' // 用于区分是“新增”还是“修改”
    };
  },
  methods: {
    onSearch() {
      console.log('查询操作');
    },
    onReset() {
      this.searchForm = {
        name: '',
        gender: '',
        role: '',
        department: '',
        status: ''
      };
      console.log('重置操作');
    },
    handleDeleteBatch() {
      console.log('批量删除操作');
    },
    openDialog(type, row) {
      this.loading = false;
      console.log('openDialog called with type:', type);
      this.dialogVisible = true;
      console.log('dialogVisible:', this.dialogVisible);  
      this.formType = type;
      if (type === 'edit') {
        this.dialogTitle = '修改用户';
        // 复制当前行数据到 formData
        this.formData = { ...row };
      } else {
        this.dialogTitle = '新增用户';
        // 重置表单
        this.formData = {
          username: '',
          name: '',
          gender: '',
          phone: '',
          email: '',
          entryDate: '',
          role: [],
          department: ''
        };
      }
    },
    submitForm() {
      if (this.formType === 'edit') {
        console.log('提交修改', this.formData);
        // 调用接口更新用户信息
      } else {
        console.log('提交新增', this.formData);
        // 调用接口新增用户
      }
      this.dialogVisible = false;
    }
  }
};
</script>

<style scoped>
.search-form {
  margin-bottom: 20px;
}

.btn-group {
  margin-bottom: 20px;
}

.dialog-footer {
  text-align: right;
}

.el-dialog__wrapper {
  z-index: 3000 !important;
}
</style>
