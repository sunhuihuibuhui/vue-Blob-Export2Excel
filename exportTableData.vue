<template>
	<div>
		<el-button class='right' type="success" icon="el-icon-circle-plus-outline" @click="exportExcel">导出</el-button>
		<div class="listOuter">
			<el-table :data="logList" border>
				<el-table-column label="车牌号">
					<template slot-scope='scope'>
						<span class="pointer" @click='toDetail(scope.row.ID)'>{{scope.row.CARNUMBER}}</span>
					</template>
				</el-table-column>
				<el-table-column prop="DRIVER" label="司机" ></el-table-column>
				<el-table-column prop="CARTYPE" label="运载类型"></el-table-column>
				<el-table-column prop="SQUARE" label="方量"></el-table-column>
				<el-table-column prop="INOUTFLAG" label="进/出"></el-table-column>
				<el-table-column prop="DEPARTMENT" label="单位"></el-table-column>
				<el-table-column prop="INOUTTIME" label="时间"></el-table-column>
			</el-table>
		</div>
	</div>
</template>
<script>
import $ from 'jquery'
import FileSaver from 'file-saver'
import XLSX from 'xlsx'
export default {
	data(){
		return {
			
		}
	},
	created(){
		
	},
	methods:{
		exportExcel () {
			var wb = XLSX.utils.table_to_book(document.querySelector('.listOuter'))
			var wbout = XLSX.write(wb, { bookType: 'xlsx', bookSST: true, type: 'array' })
			try {
				FileSaver.saveAs(new Blob([wbout], { type: 'application/octet-stream' }), 'sheetjs.xlsx')
			} catch (e) { if (typeof console !== 'undefined') console.log(e, wbout) }
			return wbout
		},
	}
}
</script>