<template>
	<div class="main">
		<div class="header">
			<img src="./assets/youtubeLogo.png" width="90" height="20" alt="Youtube Logo" />
			<div class="form-container">
				<form action="">
					<input type="text" placeholder="Search" class="search-box" />
				</form>
			</div>
		</div>
		<div class="videos-container">
			<div class="divider"></div>
			<VideoContainer />
		</div>
	</div>
</template>

<script>
import VideoContainer from './components/VideoContainer.vue';

export default {
	name: 'App',
	components: {
		VideoContainer,
	},
};
</script>

<style>
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
}
body {
	background: #f9f9f9;
	padding: 2rem 4rem;
}

.main {
	background: #fff;
	margin: 0 auto;
	padding-bottom: 3rem;
	box-shadow: 0 24px 38px 3px rgba(0, 0, 0, 0.14);
	border-radius: 4px;
}
.header {
	padding: 2rem;
	display: flex;
}
.form-container {
	width: 600px;
	margin: 0 auto;
}
.search-box {
	align-items: center;
	border: 1px solid #ccc;
	border-radius: 2px 0 0 2px;
	box-shadow: inset 0 1px 2px #eee;
	padding: 2px 6px;
	width: 550px;
	height: 30px;
}
.videos-container {
	background: #f9f9f9;
	margin: 0rem 7rem;
	padding: 1rem 1rem 4rem 1rem;
}
.divider {
	background: #ccc;
	height: 1px;
	margin: 2.5rem 7rem 1.5rem 7rem;
}
</style>
