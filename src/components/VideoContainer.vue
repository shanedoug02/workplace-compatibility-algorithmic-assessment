<template>
	<div>
		<div v-for="video of slicedVideosArr" :key="video" class="video-container">
			<div class="video-thumbnail-container">
				<img :src="video.snippet.thumbnails.high.url" alt="" />

				<!-- <object data="https://www.youtube.com/embed/q6sHNLmYbAM?autoplay=1" height="202px"></object> -->
			</div>
			<div class="video-data-container">
				<div class="video-title">
					{{ video.snippet.title }}
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
			allVideosArrData: [], // Searching for a topic on Youtube returns related videos/data. BUT the video's category id's are not included.  You need to plug in a specific video id to get that video's categoryId number.
			slicedVideosArr: [],
			videoCategoryArr: [],
			mostCommonIdCategory: '',
		};
	},

	methods: {
		requestIdCategory(arr) {
			//This is the second API request (first API request is @ mounted()). It sends each video ID to get back each video CATEGORY ID
			arr.forEach((element) => {
				fetch(`https://youtube.googleapis.com/youtube/v3/videos?part=snippet&id=${element.id.videoId}&key=AIzaSyAP_2CK1-y8YPJCJ61Vf0iJXfZCg1ppxHY`)
					.then((response) => response.json())
					.then((rawDataFromEachVideoId) => {
						this.videoCategoryArr.push(rawDataFromEachVideoId.items[0].snippet.categoryId);
						this.createObjFromArray(this.videoCategoryArr);
					});
			});
		},
		createObjFromArray(arr) {
			//Intended to easily group the most common category ID's as KEYS
			const idCounter = {};
			for (let item of arr) {
				if (idCounter[item]) {
					idCounter[item]++;
				} else {
					idCounter[item] = 1;
				}
			}
			this.findMostCommonIdCategory(idCounter);
		},
		findMostCommonIdCategory(counter) {
			let highestRepeatedKey = Math.max.apply(null, Object.values(counter)); // tells us how many TIMES an objects most popular key was utilized
			this.mostCommonIdCategory = Object.keys(counter).find((key) => counter[key] === highestRepeatedKey); // returns the most common KEY (i.e. video category)
			console.log('this.mostCommonIdCategory', this.mostCommonIdCategory);
			return this.mostCommonIdCategory;
		},

		//need to plug in a seamless object tag????????
		createSeamlessUrl() {
			for (let video of this.slicedVideosArr) {
				console.log(video);
			}
		},
	},
	mounted() {
		//This first API request fetchs 50 YouTube videos and renders 5 to the DOM
		fetch('https://www.googleapis.com/youtube/v3/search?part=snippet&q=lakers&maxResults=50&key=AIzaSyAP_2CK1-y8YPJCJ61Vf0iJXfZCg1ppxHY')
			.then((response) => response.json())
			.then((rawJson) => {
				this.allVideosArrData = rawJson.items;
				console.log('this is Allllllllllllll the raw JSON', this.allVideosArrData, this.allVideosArrData.length);
				this.slicedVideosArr = rawJson.items.slice(0, 5);
				console.log('this is the jsonData sliced', this.slicedVideosArr);
			});
	},
	computed: {},
	updated() {
		this.requestIdCategory(this.allVideosArrData);
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
