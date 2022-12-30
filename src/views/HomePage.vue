<template>
    <div class="col-md-5 mx-auto">
        <FilterNav @filter="current = $event" :current="current" />

        <div v-if="projects">
            <div v-for="project in filterProjects" :key="project.id">
                <SingleProject :project="project" @delete="handleDelete" @complete="handleComplete" />
            </div>
        </div>
    </div>
</template>

<script>
import SingleProject from '../components/SingleProject.vue';
import FilterNav from '../components/FilterNav.vue';


export default {
    components: { SingleProject, FilterNav },
    data() {
        return {
            projects: [],
            current: "all"
        }
    },
    mounted() {
        fetch('http://localhost:3000/projects')
            .then(res => res.json())
            .then(data => this.projects = data)
            .catch(err => console.log(err))
    },
    methods: {
        handleDelete(id) {
            this.projects = this.projects.filter(project => project.id != id);
        },
        handleComplete(id) {
            let p = this.projects.find(project => project.id == id);
            p.completed = !p.completed;
        }
    },
    computed: {
        filterProjects() {
            if (this.current == 'completed') {
                return this.projects.filter(project => project.completed);
            }
            if (this.current == 'ongoing') {
                return this.projects.filter(project => !project.completed);
            }
            return this.projects;
        }
    }
}
</script>

<style>

</style>