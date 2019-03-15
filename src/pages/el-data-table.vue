<template>
  <div class="table">
    <el-data-table
      dataPath="data"
      totalPath="totalElement"
      :url="url"
      :columns="columns"
      :searchForm="searchForm"
      :form="form"
      :beforeSearch="beforeSearch"
      :onNew="onNew"
      :onEdit="onEdit"
      :onDelete="onDelete"
      ></el-data-table>
    </div>
</template>

<script>
import Axios from 'axios'
export default {
  data() {
    return {
      url: '/api/v1/users',
      columns: [
        {type: 'selection', selectable: (row, index) => index > 0},//添加复选框
        {prop: 'code', label: '编号'},
        {prop: 'name', label: '姓名'},
        {prop: 'gender', label: '性别'},
        {prop: 'age', label: '年龄'},
        {
          prop: 'status',
          label: '状态',
          formatter: row => (row.status === 'normal' ? <span class="green">启用</span> : <span class="red">禁用</span>)
        }
      ],
      //查询
      searchForm: [
          {
            $type: 'input',
            $id: 'code',
            label: '编号',
            $el: {
              placeholder: '请输入'
            }
          }
        ],
      //增加,修改
      form: [
          {
            $type: 'input',
            $id: 'code',
            label: '编号',
            $el: {
              placeholder: '请输入'
            },
            rules: [
              {
                required: true,
                message: '请输入编号',
                trigger: 'blur'
              }
            ]
          },
          {
            $type: 'input',
            $id: 'name',
            label: '姓名',
            $el: {
              placeholder: '请输入'
            },
            rules: [
              {
                required: true,
                message: '请输入姓名',
                trigger: 'blur'
              }
            ]
          },
          {
            $type: 'input',
            $id: 'gender',
            label: '性别',

            rules: [
              {
                required: true,
                message: '请输入性别',
                trigger: 'blur'
              }
            ]
          },
          {
            $type: 'input',
            $id: 'age',
            label: '年龄',

            rules: [
              {
                required: true,
                message: '请输入年龄',
                trigger: 'blur'
              }
            ]
          }
      ],

      beforeSearch: () => {
        this.url = '/api/v1/users'
        return Promise.resolve()
      },
      onNew(data, row) {
    
        return Axios.post(
        '/api/v1/users',
        data
        )
      },
      onEdit(data, row) {
        return Axios.put(
        '/api/v1/users',
        data
        )
      },
      // 多选时, 参数为selected, 代表选中的行组成的数组
      onDelete: selected => {
        return Axios.delete(
          '/api/v1/users',
          {
            data: selected.map(v => v.code)
          }
        )
      }


    }
  },
  methods: {}
}
</script>
<style lang="less">

</style>