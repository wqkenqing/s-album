<template>
	<div class="gallery" :style="{ columnCount: galleryColumnCount }">
		<el-image v-for="(image, index) in images" :key="index" :src="image.src"
			:style="{ height: getAdjustedHeight(image.width, image.height) + 'px' }" fit="cover"
			class="gallery-image" :preview-src-list="[image.src]"
			@click="openDialog(image.src, index)"></el-image>

		<el-dialog :visible.sync="dialogVisible" width="80%" :before-close="closeDialog">
			<template #default>
				<img :src="currentImage.src" alt="Original Image" class="dialog-image" />
			</template>
			<template #footer>
				<div class="dialog-buttons">
					<el-button @click="changeImage('prev')" :disabled="false"
						class="dialog-button">上一张</el-button>
					<el-button @click="changeImage('next')" :disabled="false"
						class="dialog-button">下一张</el-button>
				</div>
			</template>
		</el-dialog>

	</div>
</template>

<script>
import { onMounted, onBeforeUnmount, ref, computed } from 'vue';

import 'element-plus/dist/index.css';

export default {
	name: "Gallery",
	data() {
		return {
			images: [
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
			console.log(this.currentIndex)
			this.dialogVisible = true;
		},
		closeDialog() {
			this.dialogVisible = false;
			this.currentImage = '';
			this.currentIndex = -1;
		},
		changeImage(direction) {
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
	},
	mounted() {
		window.addEventListener('resize', this.updateWindowWidth);
	},
	beforeUnmount() {
		window.removeEventListener('resize', this.updateWindowWidth);
	}
};
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
}

.dialog-image {
	width: 100%;
	max-height: 80vh;
	object-fit: cover;
}

.dialog-buttons {
	display: flex;
	justify-content: space-between;
	margin-top: 10px;
	padding: 10px;
	background-color: #f9f9f9;
	/* 背景颜色 */
	border-top: 1px solid #e0e0e0;
	/* 上边框 */
}

.dialog-button {
	padding: 10px 20px;
	background-color: #409EFF;
	color: white;
	border: none;
	cursor: pointer;
}


.el-button {
	display: inline-block;
	/* 确保按钮显示为块级元素 */
	visibility: visible;
	/* 确保按钮不可见时是显示状态 */
}
</style>
