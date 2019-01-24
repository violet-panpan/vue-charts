<template>
    <div id="result" :class="{maskBox:ismask}">
    	<div class="mask-box" style="position: relative;" @touchmove.prevent>
    	<div class="mask opacity" style="display:none;" >
    		<!--雷达图弹出框-->
    	<div class="lbox" style="display: none;">
    		<div class="y-top" @click="close">
    			<p class="y-title">社交风险视图说明</p>
    			<i class="close"></i>
    		</div>
    		<div class="z-content w90">
    			<div class="z-txt m8">图中所示风险，是指关联联系人中存在欺诈类、严重逾期类风险或本人于高风险号码频繁通话的风险情况。</div>
    			<div class="z-txt">“其他”指与法院通话、夜间通话、与虚拟号码通话的情况。</div>
    		</div>
    	</div>
    	<div class="fbox" style="display: none;">
    		<div class="y-top" @click="close">
    			<p class="y-title">负债趋势说明 </p>
    			<i class="close" ></i>
    		</div>
    		<div class="z-content w90" >
    			<div class="z-txt m8">反映近期负债金额、非近期负债金额占近一年负债金额的百分比。</div>
    			<div class="z-txt">近期负债指近一个月的负债，非近期负债指近一年中，除近一个月以外的负债。</div>
    		</div>
    	</div>
    	</div> 
    	</div>
    	<!--风险弹出框-->
    	<div class="ybox" style="display:none;">
    		<div class="y-top" @click="close">
    			<p class="y-title">说明</p>
    			<i class="close"></i>
    		</div>
    		<div class="y-content">
    			<div class="explain-box w90">
    				<div class="explain-content">
    					<div class="explain-item">
    						<p class="txt">评分区间</p>
    						<p class="txt1 m9">300分-850分(分数越低，风险越高)</p>
    					</div>
    					<div class="explain-item">
    						<p class="txt">风险等级</p>
    						<p class="txt1 m9">A:资质良好</p>
    						<p class="txt1 m5">B:资质尚可</p>
    						<p class="txt1 m5">C:资质一般</p>
    						<p class="txt1 m5">D:存在一定风险</p>
    						<p class="txt1 m5">E:资质较差</p>
    					</div>
    					<div class="explain-item">
    						<p class="txt1">评分未命中：数据资料中暂未找到匹配对象评分</p>
    					</div>
    					<div class="explain-item" style="margin-top: 0.35rem;">
    						<p class="txt1" style="font-size: 0.13rem;">查询结果仅供参考，仅限查询方内部使用，不得向信息主体等任何第三方透露。</p>
    					</div>
    				</div>
	    		</div>
    		</div>
    	</div>
    	<!--资质评估图谱弹出框-->
    	<div class="zbox" style="display: none;">
    		<div class="y-top" @click="close">
    			<p class="y-title">资质评估图谱说明</p>
    			<i class="close"></i>
    		</div>
    		<div class="z-content w90">
    			<p class="m8 f14">借款活跃度趋势：</p>
    			<div class="z-txt">注册次数、申请次数、放款次数3个指标均表示在各个借款平台的借贷行为。</div>
    			<p class="m8 f14">机构核准趋势：</p>
    			<div class="z-txt">反映近一年内不同阶段，被查询人对自己的需求程度和各信贷机构对其资质的综合评定。</div>
    			<p class="m8 f14">多头查询趋势：</p>
    			<div class="z-txt">反映近一年内不同阶段，被查询人多头查询趋势，有助于识别其多头借贷情况。</div>
    		</div>
    	</div>
    	
    	
    	<!--主题内容-->
    	<div class="content">
    		<!--评分为零-->
	    	<div class="top"  style="position: relative;" v-show="unresullt">
	    		<p class="un-txt">评分未命中</p>
	    		<p class="un-txt1">大数据评分未命中，可以尝试进件</p>
	    		<i class="ex-icon" @click="open" style="bottom: 0.2rem;right: 0.1rem;"></i>
	    	</div>
	    	<!--评分不为零-->
	    	<div class="top">
	    		<div v-show="!unresullt">
	    		<div class="item">
	    			<p class="top-title fl">姓&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;名</p>
	    			<p class="top-txt fl">{{userInfo.name}}</p>
	    		</div>
	    		<div class="item">
	    			<p class="top-title fl">身份证号</p>
	    			<p class="top-txt fl">{{userInfo.idNo}}</p>
	    		</div>
	    		<div class="item">
	    			<p class="top-title fl">报告编号</p>
	    			<p class="top-txt fl">{{userInfo.flowId}}</p>
	    		</div>
	    		<div class="media-box">
	    			<div class="flex-item" style="margin-right: 5%;">
	    				<p class="media-title fl">综合评分</p>
	    				<p class="media-txt fl blue">{{userInfo.compositeScore}}</p>
	    				<div class="media-bottom bg-bule"></div>
	    			</div>
	    			<div class="flex-item">
	    				<p class="media-title fl p25">风险等级</p>
	    				<p class="media-txt fl yellow">{{userInfo.grade}}</p>
	    				<div class="media-bottom bg-yellow"></div>
	    			</div>
	    			<i class="ex-icon" @click="open"></i>
	    		</div>
	    		<div class="sug">{{sugTxt}}</div>
	    		<div class="notice-txt" style="margin-top：0.05rem;display: none;">{{noTxt}}</div>
	    		</div>
	    	</div>
	    	<div class="explain" style="display: none;">
	    	    <div class="explain-box w90">
	    	    	<div class="title">
    					<div class="icon-left fl"></div>
    					<div class="fl">说明</div>
    					<div class="icon-right fl"></div>
	    	    	</div>
    				<div class="explain-content">
    					<div class="explain-item">
    						<p class="txt">评分区间</p>
    						<p class="txt1 m9">300分-850分(分数越低，风险越高)</p>
    					</div>
    					<div class="explain-item">
    						<p class="txt">风险等级</p>
    						<p class="txt1 m9">A:资质良好</p>
    						<p class="txt1 m5">B:资质尚可</p>
    						<p class="txt1 m5">C:资质一般</p>
    						<p class="txt1 m5">D:存在一定风险</p>
    						<p class="txt1 m5">E:资质较差</p>
    					</div>
    					<div class="explain-item">
    						<p class="txt1">评分未命中：数据资料中暂未找到匹配对象评分</p>
    					</div>
    					<div class="explain-item">
    						<p class="txt1" style="font-size: 0.13rem;">查询结果仅供参考，仅限查询方内部使用，不得向信息主体等任何第三方透露。</p>
    					</div>
    				</div>
	    	    </div>
	    	</div>
	    	<div class="bk"></div>
	    	<!--资质评估图谱-->
	    	<div class="chart-box">
	    		<div class="chart-top">
	    			<div class="chart-top-img fl"><img src="../assets/img/demand_icon_title1.png"></div>
	    			<div class="chart-top-txt fl">资质评估图谱</div>
	    			<div class="chart-top-img fl"><img src="../assets/img/demand_icon_title2.png"></div>
	    		    <i class="ex-icon po" @click="openZ"></i>
	    		</div>
	    		<!--折线图-->
	    		<div class="chart-list">
	    			<div class="list-top">
	    				<div class="flex-item list-top-txt" :class="{active:index==nowIndex}" v-for="(item,index) in list1" @click="changeList(index)">{{item}}</div>
	    			</div>
	    			<ve-line :data="loanVitalityChart" :legend='legend' v-if="nowIndex==0" v-show="chart1" :tooltip-visible="false"></ve-line>
	    			<ve-line :data="orgApprovalChart" :legend='legend' :settings="chartSettings" v-if="nowIndex==1" v-show="chart2" :tooltip-visible="false"></ve-line>
	    			<ve-line :data="multiLoanChart" :legend='legend' v-if="nowIndex==2"  v-show="chart3" :tooltip-visible="false"></ve-line>
	    			<div class="em-pic" v-show="chart1em">
	    				<img src="../assets/img/que.png"/>
	    			</div>
	    			<p class="em-txt" v-show="chart1em">此项暂无风险</p>
	    		</div>
	    		<!--负债趋势-->
	    		<div class="chart-list" style="height: 1.5rem;" v-show="showfu">
	    			<div class="list-top"><p class="list-top-txt1">负债趋势</p><i class="ex-icon lei-icon" @click="openF" style="display: block;"></i></div>
	    			<div class="list-box">
	    				<div class="list-box-top">
	    					<div class="list-box-txt fl">近期负债</div>
	    					<div class="list-box-txt fr">非近期负债</div>
	    				</div>
	    				<div class="list-box-item" >
	    					<div class="list-box-item-left fl" :style="{width:debtDistributionChart.shortTermDebtProportion}">{{debtDistributionChart.shortTermDebtProportion}}</div>
	    					<div class="list-box-item-right fl" :style="{width:debtDistributionChart.longTermDebtProportion}">{{debtDistributionChart.longTermDebtProportion}}</div>
	    				</div>
	    			</div>
	    		</div>
	    		<!--雷达图-->
	    		<div class="chart-list" id="lei" v-show="lei" style="position: relative;">
	    			<div class="list-top" style="position: relative;"><p class="list-top-txt1">社交风险视图</p><i class="ex-icon lei-icon" @click="openL" style="display: block;"></i></div>
	    			 <div style="padding-left: 0.1rem;"><ve-radar :data="socialRiskChart" :legend-visible="false" :radar='radar' :settings="chartSettings1" :extend="chartExtend"  width="3.1rem" :tooltip-visible="false"></ve-radar></div>
	    			 <p class="gao" v-show="lei"> 高</p>
	    			 <p class="zhong" v-show="lei">中</p>
	    			 <p class="di" v-show="lei">低</p>
	    		</div>
	    		<!--饼图-->
	    		<!--借款机构类型分布-->
	    		<div class="chart-list">
	    			<div class="list-top"><p class="list-top-txt1">借款机构类型分布</p></div>
	    			<div class="date" v-show="ring1">
	    				<div class="date-list flex-item" v-for="(item,index) in dateList1" :class="{activeD:index==nowIndex1}" @click="changeDate1(index,item)">{{item}}</div>
	    			</div>
	    			<div class="em-pic" v-show="emring1" style="top: 50%;">
	    				<img src="../assets/img/que.png"/>
	    			</div>
	    			<p class="em-txt" v-show="emring1">此项暂无风险</p>
	    			<!--机构类型-占比-申请机构数-->
	    			<div class="ring-box" v-show="ring1">
	    				<div class="ring-item">
	    					<ve-ring :data="selectLoan1" :settings="ringSettings" width="1.6rem" height='2rem'  :colors="colors" :legend-visible="false" :tooltip-visible="false" :hoverAnimation='false'> </ve-ring>	
	    				</div>
	    				<div class="ring-item" v-show="ring1">
	    					<p class="ting-txt" v-show="ring1">机构类型-占比-申请机构数</p>
                            <div class="ring-txt">
	    						<div class="ring-txt-left fl">
	    							<div class="clist1" :style="{background:item}" v-for='item in clist'></div>
	    						</div>
	    						<div class="ring-txt-right fr">
	    							<div class="ctxt" v-for="ss in tlist1">{{ss.机构类型}}_{{ss.申请机构数占比}}_{{ss.申请机构数}}</div>
	    						</div>
                            </div>
	    				</div>
	    			</div>
	    			<!--机构类型-占比-核准机构数-->
	    			<div class="ring-box" v-show="ring1">
	    				<div class="ring-item">
	    					<ve-ring :data="selectLoan1" :settings="ringSettings1" width="1.6rem" height='2rem'  :colors="colors" :legend-visible="false" :tooltip-visible="false" :hoverAnimation='false'> </ve-ring>	
	    				</div>
	    				<div class="ring-item" v-show="ring1">
	    					<p class="ting-txt" v-show="ring1">机构类型-占比-核准机构数</p>
                            <div class="ring-txt">
	    						<div class="ring-txt-left fl">
	    							<div class="clist1" :style="{background:item}" v-for='item in clist'></div>
	    						</div>
	    						<div class="ring-txt-right fr">
	    							<div class="ctxt" v-for="ss in tlist1">{{ss.机构类型}} _ {{ss.核准机构数占比}} _ {{ss.核准机构数}}</div>
	    						</div>
                            </div>
	    				</div>
	    			</div>
	    		</div>
	    		<!--多头查询机构类型分布-->
	    		<div class="chart-list">
	    			<div class="list-top"><p class="list-top-txt1">多头查询机构类型分布</p></div>
	    			<div class="date" v-show="ring">
	    				<div class="date-list flex-item" v-for="(item,index) in dateList" :class="{activeD:index==nowIndex2}" @click="changeDate(index,item)">{{item}}</div>
	    			</div>
	    			<div class="em-pic" v-show="emring" style="top: 50%;">
	    				<img src="../assets/img/que.png"/>
	    			</div>
	    			<p class="em-txt" v-show="emring">此项暂无风险</p>
	    			<!--机构类型-占比-申请机构数-->
	    			<div class="ring-box" v-show="ring">
	    				<div class="ring-item">
	    					<ve-ring :data="selectLoan" :settings="ringSettings" width="1.6rem" height='2rem'  :colors="colors" :legend-visible="false" :tooltip-visible="false" :hoverAnimation='false'> </ve-ring>	
	    				</div>
	    				<div class="ring-item">
	    					<p class="ting-txt" v-show="ring">机构类型-占比-申请机构数</p>
                            <div class="ring-txt">
	    						<div class="ring-txt-left fl">
	    							<div class="clist" :style="{background:item}" v-for='item in clist'></div>
	    						</div>
	    						<div class="ring-txt-right fr">
	    							<div class="ctxt" v-for="ss in tlist">{{ss.机构类型}} _ {{ss.申请机构数占比}} _ {{ss.申请机构数}}</div>
	    						</div> 
                            </div>
	    				</div>
	    			</div>
	    		</div>
	    		
	    	</div>
    	</div>
    </div>
</template>

<script>
	import axios from "axios"
	import { Toast } from 'mint-ui';
	import 'echarts/lib/component/markArea'
	import 'v-charts/lib/style.css'
    export default {
        name:"result",
        data() {
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
        	}
        	this.chartSettings = {
		        axisSite: { right: ['核准机构占比'] },
		        yAxisType: ['normal', 'percent'],
		        yAxisName: ['数值', '比率']
            }
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
        	this.chartSettings1={
        		dimension: [],
                metrics: ["一阶联系人", "二阶联系人", "主叫联系人","同行联系人","其他联系人"],
          		area:true,
        	}
        	this.chartExtend={
        	series:{
        		type: 'radar',
        		itemStyle: {normal: {areaStyle: {type: 'default'}}},  
        	}	
        	}
        	this.itemStyle={
        		normal: {areaStyle: {type: 'default'}}
        	},
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
            return {
            	showfu:false,//负载
            	leiPos:7,//雷达图的位置
            	loanPos:'',//负债趋势图
            	ismask:false,//遮罩层样式
            	showBig:false,//老旧版本展示
            	showem:false,//雷达图缺省页展示
            	emring:true,//饼1缺省图展示
            	emring1:true,//饼2图缺省展示
            	chart1em:false,//折线图缺省页展示
            	chartem:false,
            	chart1:true,//折1
            	chart2:true,//折2
            	chart3:true,//折3
            	lei:true,
            	ring:false,//饼一展示
            	ring1:false,//饼二展示
                unresullt:false,
                userInfo:{
                },
                selectLoan1:{
                	columns:[],
                	row:[],
                },
                type:0,
                token:'',
                sugTxt:'',
                noTxt:'',
                nowIndex:0,
                nowIndex1:0,
                nowIndex2:0,
                texts:[{"机构类型": "平台门户", "申请机构数": 1},{"机构类型": "平台", "申请机构数": 3}],
                clist:[],
                clist1:[],
                colors:['#19D4AE','#5AB1EF','#FA6E86','#FFB980','#0067A6','#D7C6FA','#2f4554', '#61a0a8', '#d48265', '#91c7ae','#749f83', '#ca8622', '#bda29a','#6e7074', '#546570', '#c4ccd3'],
                tlist:[],
                tlist1:[],
                debtDistributionChart:{},
                dateList:['近1个月','近3个月','近6个月','近12个月'],
                dateList1:['近1个月','近3个月','近6个月','近12个月'],
                chartData:{
                	columns: ["一阶联系人", "二阶联系人", "主叫联系人","同行联系人","其他联系人",],
                	rows:[
                		 { '一阶联系人': 1, '二阶联系人': 3, '主叫联系人': 3, '同行联系人': 3, '其他联系人': 2, },
                	]
                },
                list1:['借款活跃度趋势','机构核准趋势','多头查询趋势'],
                loanVitalityChart:{},//借款活跃度趋势表
                orgApprovalChart:{},//机构核准趋势表
                multiLoanChart:{},//多头查询趋势表
                socialRiskChart:{},//社交风险视图
                loanOrgTypeChart:{},//借款机构类型分布
                multiLoanOrgTypeChart:{},//多头查询机构类型分布
                selectLoan:{
                	columns:[],
                	row:[],
                },
                loanOrgTypeChart1: {
                	columns: ["机构类型","申请机构数","核准机构数"],
                	rows:[
                	{"机构类型":'典当',"申请机构数":1,"核准机构数":3},
                	{"机构类型":'不是典当',"申请机构数":3,"核准机构数":4},
                	{"机构类型":'呼呼',"申请机构数":5,"核准机构数":6},
                	{"机构类型":'网址',"申请机构数":10,"核准机构数":90},
                	],
                },
                
            }
        },
        methods:{
        stop(){
        var mo=function(e){e.preventDefault();};
        document.body.style.overflow='hidden';
        document.addEventListener("touchmove",mo,false);//禁止页面滑动
      },
      move(){
        var mo=function(e){e.preventDefault();};
        document.body.style.overflow='';//出现滚动条
        document.removeEventListener("touchmove",mo,false);
      },
        	
			 getCookie(cname) {
				var name = cname + "=";
				var ca = document.cookie.split(';');
				for(var i = 0; i < ca.length; i++) {
					var c = ca[i].trim();
					if(c.indexOf(name) == 0) return c.substring(name.length, c.length);
				}
				return "";
		    },
		    getValueByKey(data, field){
			    for (let key in data) {
			        if (key === field) {
			            return data[key];
			        }
			    }
			},
		    open(){
		    	$('.mask').show();
		    	$('.ybox').show();
		    	this.ismask=true;
		    },
		    openZ(){
		    	$('.mask').show();
		    	$('.zbox').show();
		    	this.ismask=true;
		    },
		    openL(){
				$('.mask').show();
		    	$('.lbox').show();
		    
		    },
		     openF(){
				$('.mask').show();
		    	$('.fbox').show();
		    	
		    },
		    close(){
		    	$('.mask').hide();
		    	$('.ybox').hide();
		    	$('.zbox').hide();
		    	$('.lbox').hide();
		    	$('.fbox').hide();
		    	this.ismask=false;
		    	
		    },
		    changeList(index){
		    	var that=this;
		    	that.nowIndex=index; 
		    	that.rfreshData();
		    	if(index==1){
		    		if(that.orgApprovalChart!=null){
		    			that.chart1em=false;
			    		that.chart2=true;
				    }else{
				    	that.chart2=false;
				    	that.chart1em=true;
				    }
		    	}else if(index==2){
		    	if(that.multiLoanChart!= null){
			    	that.chart3=true;
			    	that.chart1em=false;
			    }else{
			    	that.chart3=false;
			    	that.chart1em=true;
			    }
		    	}else if(index==0){
		    		if(that.loanVitalityChart!= null){
		    	    that.chart1em=false;
			    	that.chart1=true;
			    }else{
			    	that.chart1=false;
			    	that.chart1em=true;
			    }
		    	}
		    	
			   
		    },
		    changeDate(index,item){
		    	var that=this;
		    	that.nowIndex2=index; 
		    	var test1=that.multiLoanOrgTypeChart.rows;
		    	if(index==0){
		    		that.tlist=that.getValueByKey(test1,"oneMonthsDetail");
		    	}else if(index==1){
		    		that.tlist=that.getValueByKey(test1,"threeMonthsDetail");
		    	}else if(index==2){
		    		that.tlist=that.getValueByKey(test1,"sixMonthsDetail");
		    	}else if(index==3){
		    		that.tlist=that.getValueByKey(test1,"twelveMonthsDetail");
		    	}
		    	that.clist=that.colors.slice(0,that.tlist.length);
		    	that.selectLoan.columns=that.multiLoanOrgTypeChart.columns;
		    	that.selectLoan.rows=this.tlist;
		    },
		     changeDate1(index,item){
		    	var that=this;
		    	that.nowIndex1=index; 
		    	var test1=that.loanOrgTypeChart.rows;
		    	if(index==0){
		    		that.tlist1=that.getValueByKey(test1,"oneMonthsDetail");
		    	}else if(index==1){
		    		that.tlist1=that.getValueByKey(test1,"threeMonthsDetail");
		    	}else if(index==2){
		    		that.tlist1=that.getValueByKey(test1,"sixMonthsDetail");
		    	}else if(index==3){
		    		that.tlist1=that.getValueByKey(test1,"twelveMonthsDetail");
		    	}
		    	that.clist1=that.colors.slice(0,that.tlist1.length);
		    	this.selectLoan1.columns=that.loanOrgTypeChart.columns;
		    	this.selectLoan1.rows=this.tlist;
		    },
		    getQueryString(name) {
				var reg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)", "i");
				var r =window.location.href.split('?')[1].match(reg);
				if(r != null)
				return decodeURI(r[2]);
				return null;
			},
			//刷新数据
			rfreshData(){
				var that=this;
				axios({
			      method: "get",
			      url: "/api/riskScore/getFindInfo/v2",
			      params:{id:that.userInfo.id},
//			      params:{id:13},
			  }).then(function(d){
			  	if(d.data.success){
			  		$('.chart-box').show();
		    	    $('.bk').show();
			    	that.loanVitalityChart=d.data.data.loanVitalityChart;
			    	that.orgApprovalChart=d.data.data.orgApprovalChart;
			    	that.multiLoanChart=d.data.data.multiLoanChart;    	
			  	}else{
			  		
			  	}
			    	
			    })
			},
			//获取数据
			getData(){
				var that=this;
				axios({
			      method: "get",
			      url: "/api/riskScore/getFindInfo/v2",
			      params:{id:that.userInfo.id},
//			      params:{id:111},
			  }).then(function(d){
			  	if(d.data.success){
			  		$('.chart-box').show();
		    	    $('.bk').show();
		    	    if(that.noTxt.length>0){
		    	    	that.noTxt="风险提示 ： "+d.data.data.riskPromptingsDecide;
		    	    }
			    	that.loanVitalityChart=d.data.data.loanVitalityChart;
			    	that.orgApprovalChart=d.data.data.orgApprovalChart;
			    	that.multiLoanChart=d.data.data.multiLoanChart;
			    	that.socialRiskChart=d.data.data.socialRiskChart;
			    	that.loanOrgTypeChart=d.data.data.loanOrgTypeChar;
			    	that.multiLoanOrgTypeChart=d.data.data.multiLoanOrgTypeChart;
			    	if(d.data.data.debtDistributionChart!= null){
			    		that.debtDistributionChart=d.data.data.debtDistributionChart;
			    		that.showfu=true;
			    	}else{
			    		that.erroMsg='暂无任何信息！'
			    		that.showfu=false;
			    	}
				    	if(that.loanVitalityChart!= null){
				    	  that.chart1=true;
				    	}else{
				    		that.chart1em=true;
				    		that.chart1=false;
				    	}
			    	if(that.socialRiskChart!= null){
			    		that.lei=true;
			    	}else{
			    		that.lei=false;
			    		that.showem=true;
			    	}
			    	if(that.loanOrgTypeChart!= null){
			    		that.ring1=true;
			    		that.emring1=false;
			    		localStorage.setItem('sr',JSON.stringify(that.loanOrgTypeChart));
			    	}else{
			    		that.ring1=false;
			    		that.emring1=true;
			    	}
			    	if(that.multiLoanOrgTypeChart!= null){
			    		that.ring=true;
			    		that.emring=false;
			    		localStorage.setItem('se',JSON.stringify(that.multiLoanOrgTypeChart));
			    	}else{
			    		that.ring=false;
			    		that.emring=true;
			    	}
			  	}else{
			  		$('.chart-box').hide();
			  		$('.notice-txt').hide();
		    	    $('.bk').hide();
		    	    $('.ex-icon').hide();
		    	    $('.explain').show();
			  	}
			    	
			    })
			},
        },
        mounted(){
        	var that=this;
        	//that.getData();
          	var ss=that.getQueryString('userInfo');
	    	that.userInfo=JSON.parse(unescape(ss));
	    	if(that.userInfo.id==null||that.userInfo.id==''){
	    		 Toast({
                        message: '请升级APP至最新版本，查看新版大数据  ',
                        position: 'bottom',
                        duration: 3000
                    });
	    	}
	    	if(that.userInfo.version==null||that.userInfo.version==''){
		    	$('.chart-box').hide();
				$('.notice-txt').hide();
			    $('.bk').hide();
			    $('.ex-icon').hide();
			    $('.explain').show(); 
			    that.getData();
	    	}else{
	    		if(that.userInfo.version==1){
	    		$('.chart-box').hide();
	    		$('.notice-txt').hide();
		    	$('.bk').hide();
		    	$('.ex-icon').hide();
		    	$('.explain').show();
	    	}else if(that.userInfo.version==2){
	    		$('.chart-box').show();
	    		$('.notice-txt').show();
		    	$('.bk').show();
		    	$('.ex-icon').show();
		    	$('.explain').hide();
		    	that.getData();
	    	}
	    	}
	    	
	    	if(localStorage.getItem('se')!=null){
	    		console.log(2222);
	        	var seobj=JSON.parse(localStorage.getItem('se'));
	        	that.selectLoan.columns=seobj.columns;
	        	that.selectLoan.rows=that.getValueByKey(seobj.rows,"oneMonthsDetail");
	        	that.clist=that.colors.slice(0,that.selectLoan.rows.length);
	        	that.tlist=that.selectLoan.rows;
        	}
        	if(localStorage.getItem('sr')!=null){
         		var seobj1=JSON.parse(localStorage.getItem('sr'));
         		that.selectLoan1.columns=seobj1.columns;
	        	that.selectLoan1.rows=that.getValueByKey(seobj.rows,"oneMonthsDetail");
	        	that.clist1=that.colors.slice(0,that.selectLoan1.rows.length);
	        	that.tlist1=that.selectLoan1.rows;
        	}
	     if(that.userInfo.compositeScore==null){
	    		that.unresullt=true;
	      }else{
	      	that.unresullt=false;
	      	if(that.userInfo.grade=="A"){
	      	that.sugTxt='意见参考：放心进件，若被拒，可复议';
	        }else if(that.userInfo.grade=="B"){
	        	that.sugTxt='意见参考：放心进件，若被拒，可复议';
	        }else if(that.userInfo.grade=="C"){
	        	that.sugTxt='意见参考：可进件，碰运气，其他方面需要注意';
	        }else if(that.userInfo.grade=="D"){
	        	that.sugTxt='意见参考：好单位或者有资产的才可能通过';
	        }else{
	        	that.sugTxt='意见参考：基本没戏，不建议进件';
	        }
	      }
	      
        }
        
    }
</script>

<style scoped>
	.gao{
		position: absolute;
		font-size: 0.14rem;
		color: #707070;
		top: 34%;
		left: 32%;
	}
	.zhong{
		position: absolute;
		font-size: 0.14rem;
		color: #707070;
		top: 42%;
		left: 35%;
	}
	.di{
		position: absolute;
		font-size: 0.14rem;
		color: #707070;
		top: 50%;
		left: 39%;
	}
	#result{
		width: 100%;
		overflow: hidden;
	}
	/*新增样式*/
	/*借款机构分布图*/
	.maskClass{
		/*height: 100vh;*/
		overflow: hidden;
	}
	.lei-icon{
		background-image: url(../assets/img/demand_icon_explainy.png) !important;
		top: 0.1rem;
		left: 1.25rem;
	}
	.ring-txt-left{
		width: 12%;
	}
	.ring-txt-right{
		width: 88%;
	}
	.ctxt{
		height:0.18rem;
		font-size:0.13rem;
		font-family:PingFangSC-Regular;
		font-weight:400;
		color:rgba(112,112,112,1);
		line-height:0.18rem;
		margin-top: 0.058rem;
		margin-left: 0.02rem;
	}
	.txt3{
		font-size: 0.13rem;
		padding-top: 0.1rem;
	}
	.em-pic{
		width: 2.14rem;
		height: 0.54rem;
		position: absolute;
		top: 50%;
		left: 17%;
	}
	.em-txt{
		position: absolute;
		height:0.22rem;
		font-size:0.12rem;
		font-family:PingFangSC-Regular;
		font-weight:400;
		color:rgba(151,151,151,1);
		line-height:0.22rem;
		bottom:5%;
		left: 36%;
	}
	.em-pic img{
		width: 100%;
		height: 100%;
		display: block;
	}
	.ting-txt{
		height:0.18rem;
		font-size:0.13rem;
		font-family:PingFangSC-Regular;
		color:rgba(31,31,31,1);
		margin-bottom: 0.05rem;
		margin-top: 0.1rem;
	}
	.activeD{
		color: #0098FF !important;
		border: 0.01rem solid #0098FF !important;
		z-index: 10;
	}
	.date{
		width:92%;
		height: 0.26rem;
		display: flex;
		border: 0.01rem solid #f4f4f4;
		margin: 0 auto;
		margin-top: 0.3rem;
		
	}
	.date-list{
		width: 25%;
		font-size:0.12rem;
		font-family:PingFangSC-Regular;
		font-weight:400;
		color:rgba(151,151,151,1);
		line-height: 0.26rem;
		text-align: center;
		border-right: 0.01rem solid #F4F4F4;
	}
	.ring-box{
		width: 100%;
		margin-top: 0.2rem;
		display: flex;
	}
	.ring-item{
		width: 50%;
	}
	.clist{
		width:0.13rem;
		height:0.13rem;
		background:rgba(25,212,174,1);
		border-radius:0.02rem;
		margin-top: 0.1rem;
	}
	/*遮罩层*/
	.mask{
		height:100%; 
		width:100%; 
		position:fixed;
		_position:absolute; 
		top:0;
		z-index:100;
		background:rgb(0,0,0,0.6);
		} 
    /*说明盒子*/
   .ybox{
   		width: 78%;
   		height: 4rem;
   		background: #ffffff;
   		z-index: 9000;
   		position: absolute;
   		left: 11%;
   		top:1.34rem;
   		
    }
    .zbox{
    	width: 78%;
   		background: #ffffff;
   		z-index: 9000;
   		position: absolute;
   		left: 11%;
   		top:1.34rem;
   		padding-bottom:0.3rem;
    }
    .lbox,.fbox{
    	width: 78%;
   		background: #ffffff;
   		z-index: 900;
   		position: absolute;
   		left: 11%;
   		top:1.34rem;
   		padding-bottom:0.3rem;
   		opacity: 1 !important;
   		height: 2.1rem !important;
    }
    .z-top{
    	height: 0.5rem;
    	width: 100%;
    	border-bottom: 0.01rem solid #F4F4F4;
    	position: relative;
    }
    .y-top{
    	height: 0.5rem;
    	width: 100%;
    	border-bottom: 0.01rem solid #F4F4F4;
    	position: relative;
    }
    .y-title{
    	height:0.22rem;
		font-size:0.16rem;
		font-family:PingFangSC-Regular;
		font-weight:400;
		color:rgba(31,31,31,1);
		line-height:0.5rem;
		text-align: center;
    }
    .y-content-title{
    	height:0.2rem;
		font-size:0.16rem;
		font-weight: bold;
		color:rgba(31,31,31,1);
		line-height:0.2rem;
    }
    .close{
    	position: absolute;
    	width: 0.1rem;
    	height: 0.1rem;
    	display: block;
    	background: url(../assets/img/popup_delete_icon@2x.png);
    	right: 0.2rem;
    	top: 0.21rem;
    	background-size: cover;
    	background-size: 100% auto;
    }
    .y-content{
    	width: 90%;
    	margin: 0 auto;
    	padding-top: 0.08rem;
    	
    }
    .y-item{
    	margin-top: 0.15rem;
    }
    .y-content-txt{
		font-size:0.14rem;
		font-family:PingFangSC-Regular;
		color:rgba(112,112,112,1);
		line-height:0.2rem;
    }
	.ex-icon{
		display: block;
		width: 0.2rem;
		height: 0.2rem;
		position: absolute;
		right: -0.08rem;
		background-image: url(../assets/img/demand_icon_explain.png);
		background-size: cover;
	    background-size: 100% auto;
	    bottom: 0.02rem;
	}
	/*资质评估*/
	.po{
		right: -0.65rem;
	}
	.chart-top{
		height: 0.25rem;
		width: 2.2rem;
		margin: 0 auto;
		position: relative;
	}
	.chart-top-img{
		width: 0.5rem;
		height: 0.1rem;
		margin-top: 0.075rem;
	}
	.chart-top-img img{
		display: block;
		width: 100%;
		height: 100%;
	}
	.chart-top-txt{
		width: 1.2rem;
		height: 0.25rem;
		text-align: center;
		font-size:0.18rem;
		font-family:PingFangSC-Regular;
		color:rgba(31,31,31,1);
		line-height: 0.25rem;
	}
	/*图表样式*/
	.chart-list{
		width:90%;
		margin: 0 auto;
		background:rgba(255,255,255,1);
		box-shadow:0 0.02rem 0.04rem 0px rgba(0,0,0,0.06);
		border-radius:0.04rem;
		padding-top: 0.2rem;
		margin-top:0.2rem !important;
		position: relative;
		min-height: 2rem;
	}
	.list-top{
		width: 100%;
		height: 0.39rem;
		display: flex;
		border-bottom: 0.01rem solid #F4F4F4;
		position: relative;
	}
	.list-top-txt{
		height:0.18rem;
		font-size:0.13rem;
		font-family:PingFangSC-Medium;
		font-weight:500;
		color:#979797;
		width: 33%;
		text-align: center;
		border-right: 0.01rem solid #F4F4F4;
	}
	.list-top-txt1{
		height:0.4rem;
		font-size:0.16rem;
		font-family:PingFangSC-Medium;
		font-weight:bold;
		color:rgba(31,31,31,1);
		line-height:0.4rem;
		padding-left: 0.2rem;
	}
	.list-top-txt:last-child{
		border: none;
	}
	.active{
		color: #1F1F1F;
		font-weight: bold;
	}
	.list-box{
		padding-left: 0.2rem;
		padding-right: 0.2rem;
	}
	.list-box-top{
		width: 100%;
		height: 0.18rem;
		margin-top: 0.19rem;
		margin-bottom: 0.12rem;
	}
	.list-box-txt{
		height:18px;
		font-size:0.13rem;
		font-family:PingFangSC-Regular;
		color:rgba(112,112,112,1);
		line-height:0.18rem;
	}
	.list-box-item{
		width: 100%;
		height: 0.25rem;
	}
	.list-box-item-left{
		background:#22D5B1;
		font-size:0.13rem;
		font-family:PingFangSC-Regular;
		font-weight:400;
		color:rgba(255,255,255,1);
		line-height:0.25rem;
		text-align: center;
	}
	.list-box-item-right{
		background:#66B6F0;
		font-size:0.13rem;
		font-family:PingFangSC-Regular;
		font-weight:400;
		color:rgba(255,255,255,1);
		line-height:0.25rem;
		text-align: center;
	}
	.sug{
		width: 100%;
		margin-top: 0.15rem;
		height:0.18rem;
		font-size:0.13rem;
		font-family:PingFangSC-Regular;
		font-weight:400;
		color:rgba(112,112,112,1);
		line-height:0.18rem;
	}
	.content{
		/*padding: 0.2rem;*/
		width: 100%;
	}
	.p25{
		padding-left: 0.28rem !important;
	}
	.un-txt{
		margin-top: 0.27rem;
		text-align: center;
		height:0.22rem;
		font-size:0.16rem;
		font-family:PingFangSC-Regular;
		font-weight:400;
		color:rgba(31,31,31,1);
		line-height:0.22rem;
	}
	.un-txt1{
		margin-top: 0.14rem;
		text-align: center;
		height:0.2rem;
		font-size:0.14rem;
		font-family:PingFangSC-Regular;
		font-weight:400;
		color:rgba(112,112,112,1);
		line-height:0.2rem;
	}
	.fl{
		float: left;
	}
	.fr{
		float: right;
	}
	.item{
		height:0.2rem;
		width: 100%;
		margin-top: 0.1rem;
	}
	.top-title{
		font-size:0.14rem;
		font-family:PingFangSC-Regular;
		font-weight:400;
		color:rgba(112,112,112,1);
		line-height:0.2rem;
		margin-right: 0.22rem;
	}
	.top-txt{
		height:0.2rem;
		font-size:0.14rem;
		font-family:PingFangSC-Regular;
		font-weight:400;
		color:rgba(31,31,31,1);
		line-height:0.2rem;
	}
	.media-box{
		width: 100%;
		margin-top: 0.3rem;
		display: flex;
		height: 0.25rem;
		position: relative;
	}
	.flex-item{
		width: 45%;
		position: relative;
	}
	.media-title{
		padding-left: 0.2rem;
		height:0.25rem;
		font-size:0.18rem;
		font-family:PingFangSC-Medium;
		font-weight: bold;
		color:rgba(31,31,31,1);
		line-height:0.25rem;
		margin-right: 0.12rem;
		z-index: 100;
	}
	.media-txt{
		height:0.33rem;
		font-size:0.24rem;
		font-family:PingFangSC-Medium;
		font-weight: bold;
		line-height:0.33rem;
		margin-top: -0.05rem;
		z-index: 100;
	}
	.blue{
		color: #0098FF;
	}
	.yellow{
		color: #FCCF08;
	}
	.media-bottom{
		position: absolute;
		width: 100%;
		height: 0.14rem;
		bottom: 0.04rem;
		z-index: -2;
	}
	.bg-bule{
		background-color:#E6F5FF;
	}
	.bg-yellow{
		background-color:#FCF8E3;
	}
	.explain-box{
		width: 100%;
		margin: 0 auto;
		height: 3.3rem;
		
	}
	.explain{
		width: 89%;
		height:3.8rem;
		background:rgba(255,255,255,1);
		box-shadow:0rem 0.02rem 0.04rem 0.02rem rgba(0,0,0,0.08);
		border-radius:0.04rem;
		margin: 0 auto;
		margin-top: 0.25rem;
	}
	.w90{
		width: 90%;
		margin: 0 auto;
	}
	.title{
        width: 0.9rem;
        margin: 0 auto;
		height: 0.25rem;
		line-height: 0.25rem;
		font-size:0.18rem;
		font-family:PingFangSC-Regular;
		font-weight:500;
		color:rgba(31,31,31,1);
		margin-bottom: 0.1rem;
		padding-top: 0.25rem;
	}
	.icon-left{
		margin-top: 0.05rem;
		display: block;
		width: 0.14rem;
		height: 0.14rem;
		background-size: contain;
	    background-repeat: no-repeat;
	    background-image: url(../assets/img/data_icon_left1.png);
	    margin-right: 0.08rem;
	}
	.icon-right{
		margin-top: 0.05rem;
		display: block;
		width: 0.14rem;
		height: 0.14rem;
		background-size: contain;
	    background-repeat: no-repeat;
	    background-image: url(../assets/img/data_icon1_right.png);
	    margin-left: 0.08rem;
	}
	.explain-content{
		width: 100%;
	}
	.txt{
		height:0.22rem;
		font-size:0.16rem;
		font-family:PingFangSC-Regular;
		font-weight:520;
		color:rgba(31,31,31,1);
		line-height:0.22rem;
	}
	.txt1{
		height:0.2rem;
		font-size:0.14rem;
		font-family:PingFangSC-Regular;
		font-weight:400;
		color:rgba(112,112,112,1);
		line-height:0.2rem;
	}
	.m9{
		margin-top: 0.07rem;
	}
	.m5{
		margin-top: 0.04rem;
	}
	.explain-item{
		margin-top: 0.09rem;
	}
	.notice-txt{
		height:0.18rem;
		font-size:0.13rem;
		font-family:PingFangSC-Regular;
		font-weight:400;
		color:rgba(255,80,64,1);
		line-height:0.18rem;
	}
	.bk{
		width: 100%;
		height: 0.1rem;
		background-color: #F7F7F7;
	}
	.top{
		padding: 0.2rem;
	}
	.chart-box{
		width: 100%;
		padding-top: 0.25rem;
		padding-bottom: 0.4rem;
		border: 0.01rem solid #f4f4f4;
	}
	.z-content{
		width: 90%;
		margin: 0 auto;
	}
	.z-txt{
		font-size:0.14rem;
		font-family:PingFangSC-Regular;
		font-weight:400;
		color:rgba(112,112,112,1);
		line-height:0.2rem;
		margin-top: 0.15rem;
	}
	.m8{
		margin-top: 0.23rem !important;
	}
	.maskBox{
		width: 100%;
		height: 100vh;
		overflow: hidden;
	}
</style>