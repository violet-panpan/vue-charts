# vue-charts
#基于echarts的图表组件的使用，其中有折线图，饼图和雷达图
<h2>安装</h2>
```javaScript
npm i v-charts echarts -S
```
<h2>main.js</h2>
```javaScript
  import VCharts from 'v-charts'
  Vue.use(VCharts);
```
<h2>demo.vue图表重绘</h2>
data(){
 //折线图公用legend
        	this.legend={
        		top:'5',
		        textStyle:{
		        	color:'#707070',
		        	fontSize:'0.13rem',
		        	lineHeight:'0.18rem',
		        	height:'0.18rem'
		        	
		        },
		        padding:[0,0,20,0],
        	},
          //雷达图
        	this.radar={
		        indicator: [
		           { name: '一阶联系人', max: 3},
		           { name: '二阶', max:3},
		           { name: '主叫联系人', max: 3},
		           { name: '同行联系人', max: 3},
		           { name: '其他', max: 3},
		        ],
		        splitNumber: 2,
        	}
          //饼图
        	this.colors =['#19D4AE','#5AB1EF','#FA6E86','#FFB980','#0067A6','#D7C6FA','#2f4554', '#61a0a8', '#d48265', '#91c7ae','#749f83',  '#ca8622', '#bda29a','#6e7074', '#546570', '#c4ccd3'],
        	this.ringSettings={
        		metrics: ['申请机构数'],
                dimension: ['机构类型'],
        		center : ['0%', '100%'],
        		radius: [15,68],
                offsetY: 90,
                label: {
                normal: {
                    show: false,
                }, 
               }, 
        	}
        	this.ringSettings1={
        		metrics: ['核准机构数'],
                dimension: ['机构类型'],
        		center : ['0%', '100%'],
        		radius: [15,68],
                offsetY: 90,
                label: {
                normal: {
                    show: false,
                }, 
               }, 
        	}
}


#结果展示折线图
<img src="https://github.com/violet-panpan/vue-charts/blob/master/3.png"/>
#结果展示雷达图
<img src="https://github.com/violet-panpan/vue-charts/blob/master/1.png"/>
#结果展示饼图
<img src="https://github.com/violet-panpan/vue-charts/blob/master/2.png"/>

#最终效果
<img src="https://github.com/violet-panpan/vue-charts/blob/master/大数据评分查询结果.jpg"/>
