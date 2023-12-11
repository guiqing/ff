<template>
	<div>
		<div  style="width: calc(100% - 20px);margin: 0 auto;">
			<div class="flex" >
				<div class=" item" >
					<div class="itemlable">所属部门：</div>
					<input  class="text-input w21" type="text"  placeholder="请输入所属部门" />
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
				<textarea name=""  cols="30" style="height:100px;" class="text-input" rows="10"></textarea>
			</div>
			<button class="confirm-button" >确定</button>
		</div>
	</div>
</template>

<script>
</script>

<style>
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
</style>