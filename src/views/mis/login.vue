<template>
	<div class="page">
		<div class="panel">
			<div class="left">
				<img src="../../assets/login/logo.png" class="logo" />
				<img src="../../assets/login/big.png" class="big" />
			</div>
			<div class="right">
				<div class="title-container">
					<h2>神州大健康体检系统</h2>
					<span>V1.0</span>
				</div>
				<div v-if="!qr.qrCodeVisible">
					<div class="row">
						<el-input v-model="loginForm.username" placeholder="用户名"
							prefix-icon="user" size="large" clearable />
					</div>
					<div class="row">
						<el-input type="password" v-model="loginForm.password"
							placeholder="密码" prefix-icon="Lock" size="large"
							clearable></el-input>
					</div>
					<div class="row">
						<el-button type="primary" class="btn" size="large"
							@click="login">
							登陆系统
						</el-button>
					</div>
					<div class="row"><a class="link">二维码登陆</a></div>
				</div>
				<div v-if="qr.qrCodeVisible">
					<div class="qrCode-container">
						<img :src="qr.qrCode" height="153" class="qrCode" />
						<img src="../../assets/login/phone.png" height="148" />
					</div>
					<div class="row"><a class="link">用户名密码登陆</a></div>
				</div>
			</div>
		</div>
	</div>
</template>

<script lang="ts" setup>
	import { getCurrentInstance, reactive, ref } from 'vue';
	import { useRouter } from 'vue-router';
	import { ElMessage } from 'element-plus';

	const { proxy } = getCurrentInstance();
	const router = useRouter();

	const loginForm = reactive({
		username: '',
		password: ''
	});

	const loading = ref(false);

	const login = async () => {
		loading.value = true;
		try {
			// 这里应该有一个实际的登录API调用
			// 为了演示，我们直接模拟登录成功
			await new Promise(resolve => setTimeout(resolve, 1000)); // 模拟API调用

			// 模拟存储token和权限
			localStorage.setItem('token', 'dummy_token');
			localStorage.setItem('permissions', 'USER,ADMIN');

			ElMessage.success('登录成功');
			router.push({ name: 'Main' }); // 跳转到 mis/main 页面
		} catch (error) {
			console.error('登录失败', error);
			ElMessage.error('登录失败，请检查用户名和密码');
		} finally {
			loading.value = false;
		}
	};

	//这部分内容将来给APP程序使用
	const qr = reactive({
		qrCodeVisible: false,
		qrCode: '',
		uuid: null,
		qrCodeTimer: null,
		loginTimer: null
	});

</script>

<style lang="less" scoped="scoped">
    @import url('login.less');
</style>