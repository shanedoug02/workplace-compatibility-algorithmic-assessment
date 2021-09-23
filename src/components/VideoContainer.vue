<template>
	<div>
		<div v-for="obj of jsonData" :key="obj.id" :id="obj.id" class="video-container">
			<div class="video-thumbnail-container">
				{{ obj.name }}
				<!-- :id="video.id.videoId" -->
				<!-- <object data='https://www.youtube.com/embed/${video.id.videoId}?autoplay=1'  height='202px'></object> -->
			</div>
			<div class="video-data-container">
				<div class="video-title">
					temp
					<!-- {{video.snippet.title}} -->
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: 'VideoContainer',
	data() {
		return {
			jsonData: {},
			categories: [],
		};
	},
	methods: {
		setJson(payload) {
			this.jsonData = payload;
		},
	},
	mounted() {
		fetch('https://jsonplaceholder.typicode.com/users')
			.then((response) => response.json())
			.then((json) => {
				console.log(json);
				this.setJson(json);
			});
	},
	computed: {},
	updated: function() {
		this.$nextTick(function() {
			this.categories.push(this.jsonData[0].email, this.jsonData[1].email);
			console.log(this.categories);
		});
	},
};
</script>

<style>
.video-container {
	display: flex;
	margin: 0rem 7rem;
	margin-top: 1rem;
	height: 200px;
}
.video-thumbnail-container {
	outline: 1px solid orange;
	margin-right: 1rem;
}
.video-thumbnail {
	height: 202px;
}

.video-data-container {
	width: 600px;
	height: auto;
	outline: 1px solid orange;
}
.video-title {
	font-size: 1.8rem;
}
</style>
