<template>
    <div class="container">
        <SearchBar @onInputChange="onInputChange"></SearchBar>
        <div class="row">
            <VideoDetail :video="selectedVideo" />
            <VideoList @videoSelect="onVideoSelect" :videos="videos"></VideoList>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import SearchBar from './components/SearchBar';
import VideoList from './components/VideoList';
import VideoDetail from './components/VideoDetail';

const API_KEY = 'AIzaSyDRg8ZKgqRDZMZhqKPRM-huUoVG2_XzzUw';

export default {
    name: 'App',
    components: {
        SearchBar,
        VideoList,
        VideoDetail
    },
    data () {   //default selectedVideo to null
        return { videos: [], selectedVideo: null }; 
    },
    methods: {
        onVideoSelect(video) {
            this.selectedVideo = video;
        },
        onInputChange(searchTerm) { //Network request to YouTube API
            axios.get('https://www.googleapis.com/youtube/v3/search', {
                params: {
                    key: API_KEY,
                    type: 'video',
                    part: 'snippet',
                    q: searchTerm //query
                }
            })
            .then(response => {
                this.videos = response.data.items;
            });
        }
    }
}
</script>