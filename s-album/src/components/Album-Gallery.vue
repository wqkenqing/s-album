<template>
	<div class="gallery" :style="{ columnCount: galleryColumnCount }">
		<el-image v-for="(image, index) in images" :key="index" :src="image.src"
			:style="{ height: getAdjustedHeight(image.width, image.height) + 'px' }" fit="cover"
			class="gallery-image" @click="openDialog(image.src, index)">
		</el-image>
	</div>
	<el-dialog v-model="dialogVisible" width="80%" :before-close="closeDialog">
		<img :src="currentImage.src" alt="Original Image" class="dialog-image" />
		<div class="dialog-buttons">
			<el-button @click="changeImage('prev')" :disabled="currentIndex === 0">上一张</el-button>
			<el-button @click="changeImage('next')"
				:disabled="currentIndex === images.length - 1">下一张</el-button>
		</div>
	</el-dialog>

</template>

<script>
import { ref, computed } from 'vue';
import 'element-plus/dist/index.css';

export default {
	name: "Gallery",
	data() {
		return {
			images:
				[
					{
						src: "http://gips3.baidu.com/it/u=1821127123,1149655687&fm=3028&app=3028&f=JPEG&fmt=auto?w=720&h=1280",
						width: 720,
						height: 1280,
					},
					{
						src: "http://gips2.baidu.com/it/u=195724436,3554684702&fm=3028&app=3028&f=JPEG&fmt=auto?w=1280&h=960",
						width: 1280,
						height: 960,
					},
					{
						src: "https://gips2.baidu.com/it/u=1651586290,17201034&fm=3028&app=3028&f=JPEG&fmt=auto&q=100&size=f600_800",
						width: 600,
						height: 800,
					},
					{
						src: "https://gips3.baidu.com/it/u=3732737575,1337431568&fm=3028&app=3028&f=JPEG&fmt=auto&q=100&size=f1440_2560",
						width: 1440,
						height: 2560,
					}, {
						src: "https://gips3.baidu.com/it/u=3732737575,1337431568&fm=3028&app=3028&f=JPEG&fmt=auto&q=100&size=f1440_2560",
						width: 1440,
						height: 2560,
					},
					{
						src: "https://gips3.baidu.com/it/u=3732737575,1337431568&fm=3028&app=3028&f=JPEG&fmt=auto&q=100&size=f1440_2560",
						width: 1440,
						height: 2560,
					},
					{
						src: "https://gips3.baidu.com/it/u=3732737575,1337431568&fm=3028&app=3028&f=JPEG&fmt=auto&q=100&size=f1440_2560",
						width: 1440,
						height: 2560,
					},
					{
						src: "https://gips3.baidu.com/it/u=3732737575,1337431568&fm=3028&app=3028&f=JPEG&fmt=auto&q=100&size=f1440_2560",
						width: 1440,
						height: 2560,
					},
					{
						src: "https://gips3.baidu.com/it/u=3732737575,1337431568&fm=3028&app=3028&f=JPEG&fmt=auto&q=100&size=f1440_2560",
						width: 1440,
						height: 2560,
					},
					{
						src: "https://gips3.baidu.com/it/u=3732737575,1337431568&fm=3028&app=3028&f=JPEG&fmt=auto&q=100&size=f1440_2560",
						width: 1440,
						height: 2560,
					},
				],
			dialogVisible: false,
			currentImage: '',
			currentIndex: -1,
			windowWidth: window.innerWidth
		};
	},
	computed: {
		galleryColumnCount() {
			return this.windowWidth < 1024 ? 1 : 4;
		}
	},
	methods: {
		getAdjustedHeight(imageWidth, imageHeight) {
			const colWidth = this.windowWidth / this.galleryColumnCount;
			return Math.floor((imageHeight / imageWidth) * colWidth);
		},
		openDialog(imageSrc, index) {
			this.currentImage = this.images[index];
			this.currentIndex = index;
			this.dialogVisible = true;
		},
		closeDialog() {
			this.dialogVisible = false;
			this.currentImage = '';
			this.currentIndex = -1;
		},
		changeImage(direction) {
			console.log(this.currentIndex)
			if (direction === 'prev' && this.currentIndex > 0) {
				this.currentIndex--;
			} else if (direction === 'next' && this.currentIndex < this.images.length - 1) {
				this.currentIndex++;
			}
			this.currentImage = this.images[this.currentIndex];
		},
		updateWindowWidth() {
			this.windowWidth = window.innerWidth;
		}
	}
}
</script>

<style scoped>
.gallery {
	column-gap: 20px;
}

.gallery-image {
	width: 100%;
	margin-bottom: 20px;
	border-radius: 8px;
	object-fit: cover;
	cursor: pointer;
	box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
	transition: transform 0.3s, box-shadow 0.3s;
}

.gallery-image:hover {
	transform: scale(1.05);
	box-shadow: 0 6px 12px rgba(0, 0, 0, 0.3);
}

.el-dialog__wrapper {
	background: rgba(0, 0, 0, 0.6);
	backdrop-filter: blur(5px);
}

.el-dialog {
	border-radius: 12px;
	overflow: hidden;
	box-shadow: 0 8px 16px rgba(0, 0, 0, 0.3);
	padding: 0;
}

.dialog-image {
	width: 100%;
	max-height: 70vh;
	object-fit: contain;
	display: block;
	margin: 0 auto;
	padding: 20px;
	background-color: #fff;
}

.dialog-buttons {
	display: flex;
	justify-content: space-between;
	align-items: center;
	padding: 10px 20px;
	background-color: #f3f3f3;
	border-top: 1px solid #e0e0e0;
}

.el-button {
	font-size: 14px;
	padding: 5px 15px;
	color: #333;
	background-color: #ffffff;
	border: 1px solid #ddd;
	border-radius: 4px;
	transition: all 0.3s;
}

.el-button:hover {
	background-color: #f2f2f2;
	border-color: #ccc;
}

.el-button:disabled {
	color: #bbb;
	border-color: #e0e0e0;
	cursor: not-allowed;
	background-color: #f9f9f9;
}
</style>
