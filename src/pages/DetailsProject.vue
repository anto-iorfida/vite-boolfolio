<script>
import axios from 'axios';

export default {
    name: 'DetailsProject',
    data() {
        return {
            project: null
        };
    },
    methods: {
        getProjectDetails() {
            axios.get(`http://127.0.0.1:8000/api/projects/${this.$route.params.slug}`)
                .then((response) => {
                    this.project = response.data.project;
                    console.log(this.project);
                });
        }
    },
    mounted() {
        this.getProjectDetails();
    }
}
</script>

<template>
    <div class="container">
        <div v-if="project">
            <div class="card">
                <div class="card-header">
                    <h3>{{ project.name }}</h3>
                </div>
                <div class="card-body">
                    <blockquote class="blockquote mb-0">
                        <p class="blockquote-footer">{{ project.client_name }}</p>
                        <p v-if="project.summary">
                            {{ project.summary }}
                        </p>
                    </blockquote>
                    <div v-if="project.cover_image">
                        <img :src="`http://127.0.0.1:8000/storage/${project.cover_image}`" :alt="project.title">
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
