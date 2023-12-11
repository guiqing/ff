<template>
    <div class="password-form-container">
        <!-- <div class="title">
			<span>发起报修</span>
			<span class="bxlist">报修列表</span>
		</div> -->
		<div class="menuflex">
			<div  :class="[tabtype==1?'menunva  active':'menunva']" @click="tabpytes(1)" >发起报修</div>
			<div  :class="[tabtype==2?'menunva  active':'menunva']" @click="tabpytes(2)">报修列表</div>
		</div>
		<div v-if="tabtype==1">
			<div class="flex" >
				<div class=" item" >
					<div class="itemlable">所属部门：</div>
					<input  class="text-input w21" v-model="form." type="text"  placeholder="请输入所属部门" />
				</div>

				<div class="item" style="margin-left: 10px;">
					<div class="itemlable">联系人：</div>
					<input  class="text-input w21" type="text" placeholder="请输入联系人">
				</div>
			</div>
			<div class="flex">
				<div class="item">
					<div class="itemlable">所属科室：</div>
					<input class="text-input w21" type="text" placeholder="请再次输入所属科室">
				</div>
				<div class="item" style="margin-left: 10px;">
					<div class="itemlable">手机号：</div>
					<input  class="text-input w21" type="text" placeholder="请再次输入手机号">
				</div>
			</div>
			<div class="flex">
				<div class="item">
					<div class="itemlable">紧急级别：</div>
					<input  class="text-input w21" type="text" placeholder="请再次输入紧急级别">
				</div>
				<div class="item" style="margin-left: 10px;">
					<div class="itemlable">故障类型：</div>
					<input  class="text-input w21" type="text" placeholder="请再次输入故障类型">
				</div>
			</div>
			<div class="flex">
				<div class="item">
					<div class="itemlable">期望到场日：</div>
					<input  class="text-input w21" type="text" placeholder="请输入期望到场日">
				</div>
				<div class="item">
					<div class="itemlable">到场时间段：</div>
					<input  class="text-input w21" type="text" placeholder="请输入到场时间段">
				</div>
			</div>

			<div class="item">
				<div class="itemlable" style="width: 100px;">故障描述：</div>
				<textarea name=""  cols="30" class="text-input" rows="10"></textarea>
			</div>

			<button class="confirm-button" :disabled="oldPassword.trim() === '' || newPassword.trim() === '' || confirmPassword.trim() === ''" @click="changePassword">确定</button>
		</div>
		<div v-if="tabtype == 2" style="width: 100%;">
			<div class="bupeead">
				<div class="ittqda">
						<div class="itemlist">
							<div class="lesd">
								<div class="tips">已派单</div>
							</div>
							<div class="rfv">
								<div class="ti1">
									<div>紧急级别：</div>
									<div>类别名称</div>
								</div>
								<div class="ti1">
									<div>故障类型：</div>
									<div>东西损坏</div>
								</div>
								<div class="ti1">
									<div>问题描述：</div>
									<div>xx</div>
								</div>
							</div>
						</div>
						<div class="itemlist">
							<div class="lesd">
								<div class="tips2">正在维修</div>
							</div>
							<div class="rfv">
								<div class="ti1">
									<div>紧急级别：</div>
									<div>类别名称</div>
								</div>
								<div class="ti1">
									<div>故障类型：</div>
									<div>东西损坏</div>
								</div>
								<div class="ti1">
									<div>问题描述：</div>
									<div>xx</div>
								</div>
							</div>
						</div>
						<div class="itemlist">
							<div class="lesd">
								<div class="tips3">已完成</div>
							</div>
							<div class="rfv">
								<div class="ti1">
									<div>紧急级别：</div>
									<div>类别名称</div>
								</div>
								<div class="ti1">
									<div>上报时间：</div>
									<div>东西损坏</div>
								</div>
								<div class="ti1">
									<div>问题描述：</div>
									<div>xx</div>
								</div>
							</div>
						</div>
				</div>
			</div>
		</div>
    </div>
</template>

<script>

import appServerApi from "../../../api/appServerApi";

export default {
    name: "CreateConferenceView",
    data() {
        return {
            oldPassword: '',
            newPassword: '',
            confirmPassword: '',
			tabtype:1
        }
    },

    methods: {
		tabpytes(type){
			this.tabtype=type
		},
        async changePassword() {
            this.$modal.hide('change-password-modal')
            appServerApi.changePassword(this.oldPassword, this.newPassword)
                .then(response => {
                    console.log(response.message)
                    this.$notify({
                        text: '发起报修成功',
                        type: 'info'
                    });
                })
                .catch(err => {
                    this.$notify({
                        title: '发起报修失败',
                        text: err.message,
                        type: 'error'
                    });
                })
        },
    },
}
</script>

<style scoped lang="css">
.bupeead{
	width: 100%;
	height: 100%;
}
.ittqda{
	margin-top: 20px;
	height: 100%;
	width: 100%;
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

}
.menunva.active{
	background-color: #1976D2 !important;
	color: #fff;
}
.menuflex{
	width: 100%;
	height: 35px;
	line-height: 35px;
	display: flex;
	color: #000;
	border-bottom: 1px solid #eee;
	margin-top: 20px;
}
.w21{
	width:120px !important;
}
.flex{
	display: flex;
	width: 100%;
}
.itemlable{
	width: 90px;
	line-height: 35px;
	color: #000;
}
.password-form-container {
    width: 100%;
    padding: 0 20px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
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
    height: 40px;
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

</style>
