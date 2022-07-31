<template>
  <div>
    <el-button type="text" @click="outerVisible = true">点击打开外层 Dialog</el-button>

    <el-dialog title="外层 Dialog" :visible.sync="outerVisible">

      <el-dialog
        width="50%"
        title="内层 Dialog"
        :visible.sync="innerVisible"
        append-to-body>
        <AmapView></AmapView>
        <div slot="footer" class="dialog-footer">
        <el-button @click="innerVisible = false">取 消</el-button>
        <el-button type="primary" @click="innerVisible = true">确定</el-button>
      </div>
      </el-dialog>
      <div slot="footer" class="dialog-footer">
        <el-button @click="outerVisible = false">取 消</el-button>
        <el-button type="primary" @click="innerVisible = true">打开内层 Dialog</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
import AmapView from './Amap.vue'
export default {
  data () {
    return {
      outerVisible: false,
      innerVisible: false
    }
  },
  components: {
    AmapView
  }
}
</script>

<style>

</style>
