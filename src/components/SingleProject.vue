<template>

    <div class="card shadow-sm p-3 m-2" :class="{ complete: project.completed }">
        <div class="d-flex justify-content-between">
            <h4 @click="handleDetails()">{{ project.name }}</h4>
            <div>
                <span class="material-icons mi-done" :class="{ 'mi-done-complete': project.completed }"
                    @click="completeProject(project.id)">
                    done
                </span>
                <router-link :to="{ name: 'edit-project', params: { id: project.id } }">
                    <span class="material-icons mi-edit">edit</span>
                </router-link>
                <span class="material-icons mi-delete" @click="deleteProject(project.id)">delete</span>
            </div>
        </div>

        <p v-if="showDetails">{{ project.description }}</p>
    </div>

</template>

<script>
export default {
    props: ['project'],
    data() {
        return {
            showDetails: false,
            uri: 'http://localhost:3000/projects/',
            complete: true
        }
    },
    methods: {
        handleDetails() {
            this.showDetails = !this.showDetails
        },
        deleteProject(id) {
            fetch(this.uri + id, { method: "DELETE" })
                .then(_ => this.$emit('delete', this.project.id))
                .catch(err => console.log(err))
        },
        completeProject(id) {
            fetch(this.uri + id, {
                method: "PATCH",
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ completed: !this.project.completed })
            })
                .then(_ => this.$emit('complete', this.project.id))
                .catch(err => console.log(err))
        }
    }
}
</script>

<style scoped>
h3 {
    cursor: pointer;
}

.card {
    border-left: 3px solid crimson;
    border-radius: 4px;
}

.complete {
    border-left: 3px solid rgb(10, 147, 92);
}

.mi-edit,
.mi-delete,
.mi-done {
    opacity: 0.5;
    cursor: pointer;
    margin: 0 5px;
}

.mi-done-complete {
    color: rgb(9, 186, 9);
}

.mi-edit:hover {
    color: rgb(248, 181, 56);
}

.mi-delete:hover {
    color: crimson;
}

.mi-done:hover {
    color: rgb(9, 186, 9);
}
</style>