<template>
  <div id="app">
    <div class="container">
      <h1>Vue2 + Element UI 表格示例</h1>

      <el-table
        :data="tableData"
        style="width: 100%"
        border
        stripe
        highlight-current-row
      >
        <el-table-column
          prop="id"
          label="ID"
          width="80">
        </el-table-column>

        <el-table-column
          prop="name"
          label="姓名"
          width="120">
        </el-table-column>

        <el-table-column
          prop="age"
          label="年龄"
          width="80">
        </el-table-column>

        <el-table-column
          prop="email"
          label="邮箱"
          width="200">
        </el-table-column>

        <el-table-column
          prop="department"
          label="部门"
          width="120">
        </el-table-column>

        <el-table-column
          prop="salary"
          label="薪资"
          width="100">
          <template slot-scope="scope">
            ¥{{ scope.row.salary.toLocaleString() }}
          </template>
        </el-table-column>

        <el-table-column
          prop="status"
          label="状态"
          width="100">
          <template slot-scope="scope">
            <el-tag
              :type="scope.row.status === '在职' ? 'success' : 'danger'"
              size="small">
              {{ scope.row.status }}
            </el-tag>
          </template>
        </el-table-column>

        <el-table-column
          label="操作"
          width="180">
          <template slot-scope="scope">
            <el-button
              @click="handleEdit(scope.$index, scope.row)"
              type="primary"
              size="mini">
              编辑
            </el-button>
            <el-button
              @click="handleDelete(scope.$index, scope.row)"
              type="danger"
              size="mini">
              删除
            </el-button>
          </template>
        </el-table-column>
      </el-table>

      <div class="pagination-wrapper">
        <el-pagination
          @size-change="handleSizeChange"
          @current-change="handleCurrentChange"
          :current-page="currentPage"
          :page-sizes="[10, 20, 50, 100]"
          :page-size="pageSize"
          layout="total, sizes, prev, pager, next, jumper"
          :total="total">
        </el-pagination>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      currentPage: 1,
      pageSize: 10,
      total: 50,
      tableData: [
        {
          id: 1,
          name: '张三',
          age: 28,
          email: 'zhangsan@example.com',
          department: '技术部',
          salary: 15000,
          status: '在职'
        },
        {
          id: 2,
          name: '李四',
          age: 32,
          email: 'lisi@example.com',
          department: '销售部',
          salary: 12000,
          status: '在职'
        },
        {
          id: 3,
          name: '王五',
          age: 25,
          email: 'wangwu@example.com',
          department: '市场部',
          salary: 10000,
          status: '离职'
        },
        {
          id: 4,
          name: '赵六',
          age: 35,
          email: 'zhaoliu@example.com',
          department: '人事部',
          salary: 13000,
          status: '在职'
        },
        {
          id: 5,
          name: '钱七',
          age: 29,
          email: 'qianqi@example.com',
          department: '技术部',
          salary: 16000,
          status: '在职'
        },
        {
          id: 6,
          name: '孙八',
          age: 26,
          email: 'sunba@example.com',
          department: '设计部',
          salary: 11000,
          status: '在职'
        },
        {
          id: 7,
          name: '周九',
          age: 31,
          email: 'zhoujiu@example.com',
          department: '财务部',
          salary: 14000,
          status: '在职'
        },
        {
          id: 8,
          name: '吴十',
          age: 27,
          email: 'wushi@example.com',
          department: '运营部',
          salary: 9000,
          status: '离职'
        }
      ]
    }
  },
  methods: {
    handleEdit(index, row) {
      this.$message({
        message: `编辑用户: ${row.name}`,
        type: 'info'
      });
    },
    handleDelete(index, row) {
      this.$confirm(`确定要删除用户 ${row.name} 吗?`, '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      }).then(() => {
        this.tableData.splice(index, 1);
        this.$message({
          type: 'success',
          message: '删除成功!'
        });
      }).catch(() => {
        this.$message({
          type: 'info',
          message: '已取消删除'
        });
      });
    },
    handleSizeChange(val) {
      this.pageSize = val;
      console.log(`每页 ${val} 条`);
    },
    handleCurrentChange(val) {
      this.currentPage = val;
      console.log(`当前页: ${val}`);
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}

h1 {
  text-align: center;
  margin-bottom: 30px;
  color: #409eff;
}

.pagination-wrapper {
  margin-top: 20px;
  text-align: center;
}
</style>