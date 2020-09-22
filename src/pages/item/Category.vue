<template>
  <v-card>
    <v-flex xs12 sm10>
      <v-tree url="/item/category/list"
              :isEdit="isEdit"
              @handleAdd="handleAdd"
              @handleEdit="handleEdit"
              @handleDelete="handleDelete"
              @handleClick="handleClick"
      />
    </v-flex>
  </v-card>
</template>

<script>
  import {treeData} from '../../mockDB'
  import axios from 'axios'
  export default {
    name: "category",
    data() {
      return {
        treeData: treeData,
        isEdit:true
      }
    },
    methods: {
      handleAdd(node) {
        console.log("add .... ");
        console.log(node);
        //发送ajax提交数据保存
        this.$http({
          method: "post",
          url:"item/category",
          data:node
        }).then(resp=>{
          this.$message.info("操作成功");
        }).catch(resp=>{
          this.$message.error("服务器异常");
        });
      },
      handleEdit(id, name) {
        console.log("edit... id: " + id + ", name: " + name);
        //发送ajax提交数据保存
        this.$http({
          method: "put",
          url:"item/category",
          params:{
            id,
            name
          }
        }).then(resp=>{
          this.$message.info("操作成功");
        }).catch(resp=>{
          this.$message.error("服务器异常");
        });
      },
      handleDelete(id) {
        console.log("delete ... " + id)
        this.$http({
          method: "delete",
          url:"item/category/"+id,
        }).then(resp=>{
          this.$message.info("操作成功");
        }).catch(resp=>{
          this.$message.error("服务器异常");
        });
      },
      handleClick(node) {
        console.log(node)
      }
    }
  };
</script>

<style scoped>

</style>
