<template>
  <div class="hello">
    <button @click="exportExcel">导出表格</button>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      showWindow:false,
      totalList:[
        {
          CARNUMBER: "ceshi ",
          CARTYPE: "渣土车",
          DEPARTMENT: "测试单位",
          DRIVER: "张三",
          ID: "02c37347-fdea-11e8-8c24-00163e32a1d5",
          INOUTFLAG: "出",
          INOUTTIME: "2018-12-12 16:43:35",
          OPERATIONTYPE: "手动操作平台起杆",
          SQUARE: "111"
        },{
          CARNUMBER: "123 ",
          CARTYPE: "测试车",
          DEPARTMENT: "测试单位",
          DRIVER: "李四",
          ID: "02c37347-fdea-11e8-8c24-00163e32a1d5",
          INOUTFLAG: "出",
          INOUTTIME: "2018-12-12 16:43:35",
          OPERATIONTYPE: "手动操作平台起杆",
          SQUARE: "111"
        }]

    }
  },
  methods:{
    exportExcel(){
      require.ensure([], () => {
        const { export_json_to_excel } = require('../vendor/Export2Excel'); //这里必须使用绝对路径
        const tHeader = ['车牌号', '司机', '运载类型', '方量', '进出', '单位', '时间']//表头信息
        const filterVal = ['CARNUMBER', 'DRIVER', 'CARTYPE', 'SQUARE','INOUTFLAG','DEPARTMENT','INOUTTIME']//对应表头的字段名
        const list = this.totalList;
        const data = this.formatJson(filterVal, list);
        export_json_to_excel(tHeader, data, '进出管理列表');// 导出的表格名称，根据需要自己命名
      })
     },	
     formatJson(filterVal, jsonData){
     	return jsonData.map(v =>{
    	  return filterVal.map(j => v[j])
        })
     },
  }

}
</script>
