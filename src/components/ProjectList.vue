<script>
import axios from 'axios';
import SingleProject from './SingleProject.vue'

export default {
    name: "ProjectList",
    components: {
        SingleProject
    },
    data() {
        return {
            currentPage: 1,
            prevPageUrl: null,
            nextPageUrl: null,
            projects: [],
        };
    },
    methods: {
        getProjects(pageNumber) {
            axios.get('http://127.0.0.1:8000/api/projects',{
                params:{
                    page : pageNumber
                }
            })

                .then((response) => {
                    this.projects = response.data.result.data;
                    this.currentPage = response.data.result.current_page;
                    this.prevPageUrl = response.data.result.prev_page_url;
                    this.nextPageUrl = response.data.result.next_page_url;
                });
        }

    },
    mounted() {
        this.getProjects(this.currentPage);
    }
}
</script>

<template>
    <div class="container">
        <h2>All Projects</h2>

        <div class="row row-cols-4 my-5">
            <SingleProject v-for="project in projects" :key="project.id" :projectInfo="project"></SingleProject>
        </div>
        <nav aria-label="Page navigation example">
            <ul class="pagination justify-content-center">
                <li v-if="prevPageUrl" class="page-item ">
                    <a class="page-link rounded-pill" @click="getProjects(currentPage - 1)">Previous</a>
                </li>
                <li class="page-item"><a class="page-link rounded-circle" >{{ currentPage - 1 }}</a></li>
                <li class="page-item "><a class="page-link rounded-circle large" >{{ currentPage }}</a></li>
                <li class="page-item"><a class="page-link rounded-circle" >{{ currentPage + 1 }}</a></li>
                <li v-if="nextPageUrl" class="page-item ">
                    <a class="page-link rounded-pill" @click="getProjects(currentPage + 1)">Next</a>
                </li>
            </ul>
        </nav>
    </div>
</template>

<style lang="scss" scoped></style>