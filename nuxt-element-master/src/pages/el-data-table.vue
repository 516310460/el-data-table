<template>
  <el-data-table
  :url="url"
  dataPath="data.content"
  totalPath="data.totalElements"
  :searchForm="searchForm"
  :columns="columns"
  :form="form"
  :extraButtons="extraButtons"
  :hasView = true
>
</el-data-table>
</template>

<script>
export default {
  data() {
    return {
     
        url: 'https://www.easy-mock.com/mock/5c7387173b7ff2219057c6b2/example/assembly',
        columns: [
          // type: 'selection' will show checkbox
          // see http://element.eleme.io/#/zh-CN/component/table#table-column-attributes
          {type: 'selection', selectable: (row, index) => index >= 0},
          {prop: 'name', label: '组件名称'},
          
          {prop: 'class', label: '分类'},
          {prop: 'edition', label: '版本'},
          {prop: 'dLanguage', label: '开发语言'},
          {prop: 'lastTime', label: '最后更新时间'},
          {
            prop: 'status',
            label: '状态',
            formatter: row => (row.status === 'top' ? '上架' : '下架')
          }
        ],
        searchForm: [
          {
            $el: {placeholder: '请输入'},
            label: '组件名称',
            $id: 'name',
            $type: 'input'
          },
          {
            $el: {placeholder: '请输入'},
            label: '分类',
            $id: 'class',
            $type: 'input'
          },
          {
            $el: {placeholder: '请输入'},
            label: '状态',
            $id: 'status',
            $type: 'input'
          }
        ],
        form: [
          {
            $type: 'input',
            $id: 'name',
            label: '组件名称',
            $el: {
              placeholder: '请输入'
            },
            rules: [
              {
                required: true,
                message: '请输入组件名称',
                trigger: 'blur'
              }
            ]
          },
          {
            $type: 'input',
            $id: 'edition',
            label: '版本',
            $el: {
              placeholder: '请输入'
            },
            rules: [
              {
                required: true,
                message: '请输入版本号',
                trigger: 'blur'
              }
            ]
          },
          {
            $type: 'input',
            $id: 'dLanguage',
            label: '开发语言',
            $el: {
              placeholder: '请输入'
            },
            rules: [
              {
                required: true,
                message: '开发语言',
                trigger: 'blur'
              }
            ]
          },
          {
            $type: 'select',
            $id: 'status',
            label: '状态',
            rules: [{required: true, message: '请选择状态', trigger: 'blur'}],
            $options: [{"title":"top",'value':"上架"}, {"title":"bottom",'value':"下架"}].map(f => ({label: f.value, value: f.title})),
            $el: {
              placeholder: '请选择'
            }
          },
        ],
        extraButtons: [
          {
            type: 'default',
            text:'上架',
            textFormatter: row =>{
              return row.status === 'top' ? '下架' : '上架'; 
            },
            // row 是单行的数据
            atClick: row => {
              alert(row.status)
              return Promise.resolve()
            }
          }
        ]
      }
    },
    mounted() {
      console.log(process.env.TESTING_VAR) // 输出 just-fot-testing
    }
  }

</script>
