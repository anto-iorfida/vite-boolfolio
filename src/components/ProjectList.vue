<script>
import axios from 'axios';
import SingleProject from './SingleProject.vue'

export default {
    name: "ProjectList",
    components:{
        SingleProject
    },
    data() {
        return {
            projects: []
        };
    },
    methods:{
        getProjects() {
            axios.get('http://127.0.0.1:8000/api/projects')
            .then((response) => {
                this.projects = response.data.result;
            });
        }
    },
    mounted () {
        this.getProjects();
    }
}
</script>

<template>
    <div class="container">
        <h2>All Projects</h2>

        <div class="row row-cols-4">
           <SingleProject v-for="project in projects" :key="project.id" :projectInfo="project" ></SingleProject>
        </div>
    </div>
</template>

<style lang="scss" scoped></style>