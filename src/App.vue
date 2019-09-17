<template>
  <div id="app">
    <bk-table :columns="columns" :tableData="list">
      <el-table-column slot="operate" label="操作" align="center" fixed="right" width="300">
                <template slot-scope="scope">
                    <el-button size="small" type="warning"
                               icon='el-icon-edit'
                               @click="edit(scope.row)">编辑
                    </el-button>
                    <el-button size="small" type="primary"
                               icon='el-icon-success'
                               @click="startUsing(scope.row)">启用
                    </el-button>          
                </template>
        </el-table-column>
    </bk-table>
  </div>
</template>

<script>
import BkTable from './components/BkTable.vue'

export default {
  name: 'app',
  components: {
    BkTable
  },
  data (){
    return {
      list:[
        {
          name:'张三',
          firstName: '张',
          lastName:'三',
          age:14,
          status:1,
          phone:12837373722,
          tags:['学生', '志愿者'],
          1:'奶茶',
          2:'咖啡',
        },
        {
          name:'李四',
          firstName: '李',
          lastName:'四',
          age:19,
          status:1,
          phone:12837373722,
          tags:['学生', '志愿者'],
          1:'可乐',
          2:'优酸乳',
          3:'椰树椰子汁'
        },
      ]
    }
  },
  computed:{
    columns (){
      let columns = [
        {
          label:'姓名',
          prop:'name',
          width:'300',
          type:'string',
          children:[
            {
              label:'姓',
              prop:'firstName',
              type:'string',
            },
            {
              label:'名',
              prop:'lastName',
              type:'string',
            }
          ]
        },
        {
          label:'年龄',
          prop:'age',
          width:'50',
          type:'string'
        },
        {
          label:'用户状态',
          prop:'status',
          width:'',
          type:'select',
          render: (row) => {
            if (row.status === 0) {
              return '停用'
            } else if (row.status === 1) {
              return '启用'
            } else {
              return '删除'
            } 
          }
        },
        {
          label:'联系电话',
          prop:'phone',
          width:'120',
          type:'string'
        },
        {
          label:'标签',
          prop:'tags',
          width:'',
          type:'array',
          render: (row) => {
            return row.tags.join(',')
          }
        },
        {
          slot:'operate'
        },
      ]
      return columns
    }
  },
  created(){
    this.poolColumns(this.columns,[{
      name:'C舱',
      id:1,
      code:'C'
    },{
      name:'F舱',
      id:2,
      code:'F'
    },{
      name:'H舱',
      id:3,
      code:'H'
    },],this.list)
  },
  methods:{
    poolColumns(columns, trends, data){ //columns 原有表头, trends 动态表头, data数据.
      //动态表头回来的数据是什么类型？                      
      //汇总增加动态表头
      for(let item of trends){
          columns.push({
              prop: item.id,
              label: item.name,
              type: 'string'
          })
      }
      return {
          columns,
          data
      }

  }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
