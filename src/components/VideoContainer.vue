<template>
  <div class="video-container">
    <div class="video-thumbnail-container">
        testing
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
</template>

<script>
    export default {
        name: 'VideoContainer'
    }
</script>

<style>
.video-container {
       display: flex;
       margin: 0rem 7rem;
       margin-top: 1rem;
}
.video-thumbnail-container {
       outline: 1px solid orange;
       margin-right: 1rem;
}
.video-thumbnail{
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