<template>
    <div class="conversation-info">
        <div class="password-form-container" v-if="tabtype < 3">
			<div class="menuflex">
				<div  :class="[tabtype==1?'menunva  active':'menunva']" @click="tabpytes(1)" >发起报修</div>
				<div  :class="[tabtype==2?'menunva  active':'menunva']" @click="tabpytes(2)">报修列表</div>
			</div>
			<div v-if="tabtype == 1" style="width: calc(100% - 20px);margin: 0 auto;">
				<div class="flex" >
					<div class=" item" placeholder="请输入" >
						<div class="itemlable">所属部门：</div>
                        <select class="text-input w21" v-model="formdata.dapart"  placeholder="请输入">
                            <option value="1">财务部</option>
                            <option value="2">销售部</option>
                        </select>
					</div>
					<div class="item" style="margin-left: 10px;">
						<div class="itemlable">联系人：</div>
						<input  class="text-input w21" type="text" v-model="formdata.phoneName" placeholder="请输入">
					</div>
				</div>
                <div class="flex" >
                	<div class="item" style="margin-left: 10px;">
                		<div class="itemlable">设备名称：</div>
                		<input  class="text-input w21" type="text" v-model="formdata.devicename" placeholder="请输入">
                	</div>
                	<div class="item" style="margin-left: 10px;">
                		<div class="itemlable">联系地址：</div>
                		<input  class="text-input w21" type="text" v-model="formdata.address" placeholder="请输入">
                	</div>
                </div>

				<div class="flex">
                    <div class="item">
                        <div class="itemlable">所属科室：</div>
                        <select class="text-input w21" v-model="formdata.departments"  placeholder="请输入">
                            <option value="1">产科</option>
                            <option value="2">妇科</option>
                            <option value="3">骨科</option>
                        </select>
                    </div>
					<div class="item" style="margin-left: 10px;">
						<div class="itemlable">手机号：</div>
						<input  class="text-input w21" v-model="formdata.phone" type="text" placeholder="请输入">
					</div>
				</div>
				<div class="flex">
					<div class="item">
						<div class="itemlable" >紧急级别：</div>
                        <select class="text-input w21" v-model="formdata.rank"  placeholder="请输入">
                            <option value="1">1级</option>
                            <option value="2">2级</option>
                            <option value="3">3级</option>
                        </select>
					</div>
					<div class="item" style="margin-left: 10px;">
						<div class="itemlable">故障类型：</div>
                        <select class="text-input w21" v-model="formdata.malfunction"  placeholder="请输入">
                            <option value="1">一般故障</option>
                            <option value="2">重大故障</option>
                        </select>
					</div>
				</div>
				<div class="flex">
					<div class="item">
						<div class="itemlable">期望到场日：</div>
						<input  class="text-input w21" v-model="formdata.arrival" type="text" placeholder="请输入">
					</div>
					<div class="item">
						<div class="itemlable">到场时间段：</div>
                        <select class="text-input w21" v-model="formdata.arrivalTime"  placeholder="请输入">
                            <option value="8:00">8:00</option>
                            <option value="9:00">9:00</option>
                            <option value="10:00">10:00</option>
                            <option value="11:00">11:00</option>
                            <option value="12:00">12:00</option>
                        </select>
					</div>
				</div>

				<div class="item">
					<div class="itemlable" style="width: 100px;">故障描述：</div>
					<textarea name=""  cols="30" style="height:100px;" v-model="formdata.desc" class="text-input" rows="10"></textarea>
				</div>
				<button class="confirm-button" @mousedown="sendbaox">确定</button>
			</div>
			<div v-if="tabtype == 2" style="width: 100%;">
				<div class="bupeead">
					<div class="ittqda">
                            <div class="itemlist" @click="godetail(item)"  v-for="item in datalist">
                            	<div class="lesd">
                            		<div class="tips" v-if="item.orderStatus == 0">已发布</div>
									<div class="tips2" v-if="item.orderStatus == 1">已接单</div>
									<div class="tips3" v-if="item.orderStatus == 2">维修中</div>
									<div class="tips3" v-if="item.orderStatus == 3">已签字</div>
									<div class="tips3" v-if="item.orderStatus == 4">已完成</div>
									<div class="tips3" v-if="item.orderStatus == 5">待评价</div>
                            	</div>
                            	<div class="rfv">
                            		<div class="ti1">
                            			<div>紧急级别：</div>
                            			<div>{{item.rank}}级</div>
                            		</div>
                            		<div class="ti1">
                            			<div>故障类型：</div>
                            			<div>{{item.malfunction}}</div>
                            		</div>
                            		<div class="ti1">
                            			<div>问题描述：</div>
                            			<div>{{item.desc}}</div>
                            		</div>
                            	</div>
                            </div>
					</div>
				</div>
			</div>
        </div>
		<div class="godetailcss" v-if="tabtype == 3">
			<div  style="width: calc(100% - 20px);margin: 0 auto;font-size: 14px;">
				<div class="flex" style="flex-direction: column;" >
					<div class=" item2" >
						<div class="itemlable2" style="width: 100px;">所属部门：</div>
						<div  class="text-input " style="line-height: 35px;" >{{detailinfo.dapart}}</div>
					</div>
					<div class="item2" >
						<div class="itemlable2" style="width: 100px;">联系人：</div>
						<div  class="text-input " style="line-height: 35px;"  >{{detailinfo.phoneName}}</div>
					</div>
					<div class="item2">
						<div class="itemlable2" style="width: 100px;">所属科室：</div>
						<div  class="text-input " style="line-height: 35px;"  >{{detailinfo.departments}}</div>
					</div>
					<div class="item2" >
						<div class="itemlable2" style="width: 100px;">手机号：</div>
						<div  class="text-input " style="line-height: 35px;"  >{{detailinfo.phone}}</div>
					</div>
					<div class="item2">
						<div class="itemlable2" style="width: 100px;">紧急级别：</div>
						<div  class="text-input " style="line-height: 35px;"  >{{detailinfo.rank}}级</div>
					</div>
					<div class="item2" >
						<div class="itemlable2" style="width: 100px;">故障类型：</div>
						<div  class="text-input " style="line-height: 35px;" >{{detailinfo.malfunction}}</div>
					</div>
					<div class="item2">
						<div class="itemlable2" style="width: 100px;">期望到场日：</div>
						<div  class="text-input " style="line-height: 35px;" >{{detailinfo.arrival}}</div>
					</div>
					<div class="item2">
						<div class="itemlable2" style="width: 100px;">到场时间段：</div>
						<div  class="text-input " style="line-height: 35px;"  >{{detailinfo.arrivalTime}}</div>
					</div>
                    <div class="item2">
                    	<div class="itemlable2" style="width: 100px;">当前状态：</div>
                        <div class="text-input " style="line-height: 35px;" v-if="detailinfo.orderStatus == 0">已发布</div>
                        <div class="text-input " style="line-height: 35px;" v-if="detailinfo.orderStatus == 1">已接单</div>
                        <div class="text-input " style="line-height: 35px;" v-if="detailinfo.orderStatus == 2">维修中</div>
                        <div class="text-input " style="line-height: 35px;" v-if="detailinfo.orderStatus == 3">已签字</div>
                        <div class="text-input " style="line-height: 35px;" v-if="detailinfo.orderStatus == 4">已完成</div>
                        <div class="text-input " style="line-height: 35px;" v-if="detailinfo.orderStatus == 5">待评价</div>
                    </div>
					<div class="item2">
						<div class="itemlable2" style="width: 100px;">故障描述：</div>
						<div  class="text-input " style="line-height: 35px;"  >{{detailinfo.malfunctionRemark}}</div>
					</div>
					<div class="ccaaa" @click="closetype"  >关闭</div>
				</div>
			</div>
		</div>
    </div>
</template>

<script>
import wfc from "../../../wfc/client/wfc";
import organizationServerApi from "../../../api/organizationServerApi.js";
export default {
    name: "Baoxiunew",
    props: {},
    data() {
        return {
         oldPassword: '',
         newPassword: '',
         confirmPassword: '',
         tabtype:1,
         datalist:[],
		 detailinfo:{},
		 formdata:{
             address:"",
             devicename:"",
			 malfunctionRemark:"",
             hospitalName:"",
			 arrival:"",
			 arrivalTime:"",
			 malfunction:"",
			 rank:"",
			 phone:"",
			 departments:"",
			 phoneName:"",
			 dapart:""
		 }
        }
    },

	created() {
		this.getlistall();
	},
    methods: {
		 tabpytes(type){
			this.tabtype=type
		 },
		 godetail(item){

			 if(item.dapart==1){
				item.dapart="财务部";
			 }else if(item.dapart==2){
				item.dapart="销售部";
			 }
			 if(item.departments==1){
			 	item.departments="产科";
			 }else if(item.departments==2){
			 	item.departments="妇科";
			 }else if(item.departments==3){
			 	item.departments="骨科";
			 }

			 if(item.malfunction==1){
			 	item.malfunction="一般故障";
			 }else if(item.malfunction==2){
			 	item.malfunction="重大故障";
			 }
			 this.detailinfo=item
			 this.tabtype=3
		 },
		 closetype(){
			this.tabtype=2
		 },
		 //获取报修列表
		 getlistall(){
			 let fdata={}
			 fdata.pageNo=1;
			 fdata.pageSize=100000000
			 organizationServerApi.getbaoxiudan(fdata).then(resp=>{
				 this.datalist=resp.result.records
				 this.datalist.map(p=>{
					 if(p.malfunction==1){
						 p.malfunction="一般故障";
					 }else if(p.malfunction==2){
						 p.malfunction="重大故障";
					 }
				 })
			 })
		 },
		 //发起维修报修
		 sendbaox(){
			let fdata={}
			fdata.address=this.formdata.address
			fdata.arrival=this.formdata.arrival
			fdata.arrivalTime=this.formdata.arrival+" "+this.formdata.arrivalTime
			fdata.dapart=this.formdata.dapart
			fdata.departments=this.formdata.departments
			fdata.devicename=this.formdata.devicename
			fdata.hospitalName=this.formdata.hospitalName
			fdata.malfunction=this.formdata.malfunction
			fdata.phone=this.formdata.phone
			fdata.phoneName=this.formdata.phoneName
			fdata.rank=this.formdata.rank
			fdata.malfunctionRemark=this.formdata.malfunctionRemark

			organizationServerApi.addbaoxiudan(fdata).then(resp=>{
				if(resp.success){
					this.tabtype=2
					this.$notify({
					    title: '温馨提示',
					    text: resp.message,
					    type: 'success'
					});
				}else{
					this.$notify({
					    title: '温馨提示',
					    text: "操作失败",
					    type: 'error'
					});
				}
			})
		 }
    },

	components: {},
    computed: { }
};
</script>

<style lang="css" scoped>
.bupeead{
	width: 100%;
	height: 100%;
}
.godetailcss{
	margin:10px;

}
.ccaaa{
	background-color: #009688;
	color:#fff;
	width:100px;
	margin:0 auto;
	height:35px;
	line-height:35px;
	text-align: center;
	margin-top: 30px;
	border-radius:3px;
}
.ittqda{
	margin-top: 20px;
	height: calc(100% - 150px);
	width: 100%;
	overflow: auto;
    padding-bottom: 150px;
}
.item2{
	display: flex;
	width:100%;
	text-align: left;
	border-bottom: 1px solid #eee;
	height: 35px !important;
	list-height:35px !important;
}
.sbaodd{
	width: 54px;
	height: 35px;
	line-height: 35px;
	text-align: center;
	position: absolute;
	right: 10px;
}
.layui-btn{
	height: 38px;
	line-height: 38px;
	border: 1px solid transparent;
	padding: 0 18px;
	background-color: #009688;
	color: #fff;
	white-space: nowrap;
	text-align: center;
	font-size: 14px;
	border-radius: 2px;
	cursor: pointer;
}
.layui-btn-sm {
    height: 30px;
    line-height: 30px;
    padding: 0 10px;
    font-size: 12px;
}
.tipnaa{
	width: 100%;
	position: relative;
	height: 40px;
}
.lesd{
	width: 40%;
	background-color: #eee;
	height: 100px;
}
.itemlist{
	display: flex;
	padding: 10px;
	width: 100%;
	border-bottom: 1px solid #eee;
    cursor: pointer;
}
.rfv{padding-left: 10px;}
.ti1{
	display: flex;
	margin-bottom: 10px;font-size: 14px;
	margin-top: 10px;
}
.tips{
	font-size: 12px;
	background-color:#2F4056;
	color: #fff;
	width: 60px;
	text-align: center;
	padding: 3px 6px;
	border-radius: 2px;
}
.tips2{
	font-size: 12px;
	background-color:#FF5722;
	color: #fff;
	width: 60px;
	text-align: center;
	padding: 3px 6px;
	border-radius: 2px;
}
.tips3{
	font-size: 12px;
	background-color:#009688;
	color: #fff;
	width: 60px;
	text-align: center;
	padding: 3px 6px;
	border-radius: 2px;
}
.item{
	display: flex;
	width:50%;
	text-align: left;
	justify-content: space-between;
}
.bxlist{
	position: absolute;
	right: 10px;
}
.menunva{
	width: 50%;
	float: left;
	height: 35px;
	line-height: 35px;
	color: #000;
	text-align: center;
	background-color: #eee;
	cursor: pointer;
}
.menunva.active{
	background-color: #1976D2 !important;
	color: #fff;
}
.menuflex{
	width: 100%;
	height: 25px;
	line-height: 25px;
	display: flex;
	color: #000;
	border-bottom: 1px solid #eee;
}
.w21{
	width:80px !important;
}
.flex{
	display: flex;
	width: 100%;
}
.itemlable{
	width: 78px;
	line-height: 25px;
	color: #000;
}
.itemlable2{
	width: 78px;
	line-height: 35px;
	color: #000;
}
.password-form-container {
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
	margin-top:10px;
}

.password-form-container .title {
    padding-top: 20px;
    font-size: 18px;
}

.password-form-container .tip {
    align-self: flex-start;
    font-size: 12px;
    color: #4168e0;
    margin-top: 10px;
}

.password-form-container .item {
    width: 100%;
    font-size: 13px;
    margin-top: 20px;
    position: relative;
}

.password-form-container .text-input {
    height: 25px;
    width: 100%;
    border: 1px solid #e5e5e5;
    border-radius: 3px;
    outline: none;
    padding: 0 5px;
    -moz-appearance: textfield;
}

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
    -webkit-appearance: none;
    margin: 0;
}

.password-form-container .text-input:active {
    border: 1px solid #4168e0;
}

.password-form-container .text-input:focus {
    border: 1px solid #4168e0;
}

.password-form-container .confirm-button {
    height: 40px;
    width: 100%;
    margin-top: 20px;
    border: 1px solid #e5e5e5;
    border-radius: 3px;
}

.password-form-container .confirm-button:active {
    border: 1px solid #4168e0;
}

.password-form-container .confirm-auth-code-button {
    position: absolute;
    font-size: 12px;
    top: 50%;
    right: 0;
    transform: translateY(-50%);
    margin: 0 5px;
}



.conversation-info {
    display: flex;
    flex-direction: column;
    position: relative;
    justify-content: flex-start;
    height: 100%;
    overflow: hidden;
	right: 0px;
	background-color: #fff;

}

.action-item {
    height: 50px;
    display: flex;
    padding-left: 20px;
    align-items: center;
}

.action-item .icon {
    width: 40px;
    height: 40px;
    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: 3px;
    border: 1px dashed #d6d6d6;
}

.action-item img {
    width: 40px;
    height: 40px;
}

.action-item p {
    margin-left: 10px;
    font-size: 13px;
}

.action-item:active {
    background-color: #d6d6d6;
}

.conversation-action-item {
    display: flex;
    color: red;
    align-items: center;
    font-size: 12px;
    justify-content: center;
    height: 42px;
    max-height: 42px;
    border-top: 1px solid #ececec;
}

.conversation-action-item:active {
    background: #d6d6d6;
}

</style>
