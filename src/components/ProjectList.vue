<script>
import axios from 'axios';

export default {
    name: "ProjectList",
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
            <div v-for="project in projects" :key="project.id" class="col">
                <div class="card my-3"  style="width: 18rem;">
                    <div class="card-body">
                        <h4 class="card-title">{{project.name}}</h4>
                        <h6 class="card-subtitle my-3 text-body-secondary">{{project.client_name}}</h6>
                        <p class="card-text">{{ project.summary }}</p>
                        <!-- <a href="#" class="card-link">Card link</a>
                        <a href="#" class="card-link">Another link</a> -->
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style lang="scss" scoped></style>