XLSX-and-FileSaver
使用XLSX和filesaver导出表格数据,
本方法针对页面中已经渲染出来的数据，如果需要导出数据库数据，请参考另外两种方法

首先安装两个依赖
npm i --save xlsx file-saver

在使用的组件中引入
import FileSaver from 'file-saver'
import XLSX from 'xlsx'

