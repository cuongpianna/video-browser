<template>
    <div class="container">
        <search-bar @termChange="onTermChange"></search-bar>
        <video-detail></video-detail>
        <video-list @videoSelect="onVideoSelect" :videos="videos"></video-list>
    </div>
</template>

<script>
import axios from 'axios';
import SearchBar from './components/SearchBar';
import VideoList from './components/VideoList';
import VideoDetail from './components/VideoDetail';
const API_KEY = 'AIzaSyBq6RdDAcOjqXD1x7q0kb6R8XxknyvVTEM';

export default {
    name: 'App',
    components: {
        SearchBar, VideoList, VideoDetail
    },
    data() {
        return {
            videos: []
        };
    },
    methods: {
        onVideoSelect(video){
            console.log(video);
        },
        onTermChange (searchTerm){
            axios.get('https://www.googleapis.com/youtube/v3/search', {
                params: {
                    key : API_KEY,
                    type: 'video',
                    part: 'snippet',
                    q: searchTerm
                }
            }).then(response => {
                this.videos = response.data.items;
            });
        }
    }
};
</script>
