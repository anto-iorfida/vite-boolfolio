<script>
export default {
    name: "SingleProject",
    props: {
        projectInfo: Object
    },
    data() {
        return {

        }
    },
    methods: {
        troncateText(text) {

            if (text.length > 100) {
                return text.substr(0, 99) + '...';
            }
        }
    }
}
</script>

<template>
    <div class="col">
        <div class="card my-3" style="width: 18rem;">
            <div class="card-body">
                <h4 class="card-title">{{ projectInfo.name }}</h4>
                <h6 class="card-subtitle my-3 text-body-secondary">{{ projectInfo.client_name }}</h6>
                <h6 v-if="projectInfo.type" class="card-subtitle my-3 text-body-secondary"><strong>Typo: </strong>{{
                    projectInfo.type.name}}</h6>
                <div class="text-body-secondary">
                    <strong>Technologies: </strong> <span v-for="technology in projectInfo.technologies"
                        :key="technology.id">{{ technology.name }} &nbsp;</span>
                </div>
                <p v-if="projectInfo.summary" class="card-text">{{ troncateText(projectInfo.summary) }}</p>

                <router-link :to="{ name: 'details-post', params: { slug: projectInfo.slug } }"
                    class="btn btn-primary">Info</router-link>
            </div>
        </div>
    </div>
</template>

<style lang="scss" scoped></style>