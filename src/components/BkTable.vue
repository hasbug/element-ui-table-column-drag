<template>
    <el-table
    :data="tableData"
    style="width: 100%"
    :row-class-name="tableRowClassName">
    <template v-for="(col,index) in columns">
        <slot v-if="col.slot" :name="col.slot"></slot>
        <bk-column :col="col" :key="col.id? col.id: index" :columnKey="col.id? col.id.toString(): index.toString()"></bk-column>
    </template>
  </el-table>
</template>
<script>
    import BkColumn from './BkColumn';
    export default {
        data () {
            return{
                tableRowClassName:''
            }
        },
        components:{
            BkColumn
        },
        props:{
            tableData:{ //传入的表格list数据
                type: Array,
                default: ()=>{
                    return []
                },

            },
            columns:{ //表头配置
                type: Array,
                default: ()=>{
                    return []
                },
            }
        },
        methods:{
            //点击编辑
            handleEdit () {},
            //取消编辑
            handelCancel () {}
        }
    }

    /**
        columns 每一项配置
        {
            label:'显示名称',
            prop:'对应tableData中的key'
            width: '宽度',
            type:'数据类型,方便编辑使用对应form组件'，若为空默认未字符串. string boolean array 
            render: Function //设置自定义内容
            slot: '插槽名称' //使用插槽
        }
     */
</script>
