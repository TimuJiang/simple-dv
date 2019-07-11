<template>
	<div class="about">
		<el-upload
			class="avatar-uploader"
			multiple
			action="https://jsonplaceholder.typicode.com/posts/"
			:show-file-list="false"
			:http-request="uploadFileMethod">
			<i class="el-icon-plus avatar-uploader-icon"></i>
		</el-upload>
	</div>
</template>

<script>
	import axios from 'axios'
	export default {
		name: 'about',
		methods: {
			uploadFileMethod (param) {
				let fileObject = param.file
				let formData = new FormData()
				formData.append('file', fileObject)
				this.upload('/geely-dataview/dataSource/upload', formData, {id: 111111})
			},
			upload (url, data, params) {
				let instance = axios.create({
					baseURL: '/',
					timeout: 90000,
					headers: {
						'Content-Type': 'multipart/form-data',
					}
				})
				let config = {
					params: {...params}
				}
				return new Promise((resolve, reject) => {
					instance
						.post(url, data, config)
						.then(res => {
							reject(res.data.data)
						})
						.catch(error => {
							reject(error)
						})
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.about {

	}
</style>
