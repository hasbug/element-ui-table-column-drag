<template>    
    <el-table-column
    :column-key="columnKey"
    :label="col.label"
    :width="col.width">
        <template v-if="col.children && col.children.length>0">
            <bk-column v-for="(item,subIndex) in col.children" :col="item" :key="item.id? item.id: subIndex" :columnKey="item.id? item.id.toString(): subIndex.toString()"></bk-column>
        </template>
        <template slot-scope="scope">
        <span v-if="col.render">
            {{col.render(scope.row)}}
        </span>
        <span v-else>{{scope.row[col.prop]}}</span>
        </template>
    </el-table-column>
</template>
<script>
    export default {
        name:'BkColumn',
        data (){
            return {

            }
        },
        props:{
            col: {
                type: Object,
                default () {
                    return {}
                }
            },
            columnKey:{
                type:String
            }
        }
    }
</script>