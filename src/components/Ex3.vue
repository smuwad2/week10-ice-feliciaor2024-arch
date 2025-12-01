<script>
import blogPost from './subcomponents/BlogPost2.vue'
import axios from 'axios'
    export default {
        data() {
            return {
                posts: [] // array of post objects
            }  
        },
        computed: {
            baseUrl() {
                if (window.location.hostname == 'localhost')
                    return 'http://localhost:3000'
                else {
                    const codespace_host = window.location.hostname.replace('5173', '3000')
                    return `https://${codespace_host}`;
                }
            }
        },
        created() { // created is a hook that executes as soon as Vue instance is created
            axios.get(`${this.baseUrl}/posts`)
            .then(response => {
                // this gets the data, which is an array
                this.posts = response.data
                console.log(response.data)
            })
            .catch(error => {
                this.posts = [{ entry: 'There was an error: ' + error.message }]
            })
        },
        methods: {
            deletePost(id) {
                // Send delete request then remove the post from local array.
                axios.get(`${this.baseUrl}/deletePost`, {
                    params: { id: id }
                }).then(response => {
                    console.log(response.data)
                    // Normalize to numbers to avoid string/number mismatches
                    const idNum = Number(id);
                    this.posts = this.posts.filter(p => Number(p.id) !== idNum);
                }).catch(error => {
                    this.posts = [{ entry: 'There was an error: ' + error.message }]
                })
            }
        },
        components: {
            blogPost
        }
    }
</script>

<template>
   <!-- TODO: make use of the 'blog-post' component to display the blog posts -->
    <blogPost v-for="post in posts" :subject="post.subject" :entry="post.entry" :mood="post.mood" :key="post.id">
        <button class="btn btn-primary" @click="deletePost(post.id)">Delete</button>
    </blogPost>
</template>
