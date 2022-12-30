<template>
    <div class="col-md-5 mx-auto">
        <div class="card p-4">
            <form @submit.prevent="handleSubmit">
                <div class="mb-2">
                    <label for="name">Name</label>
                    <input type="text" class="form-control" id="name" v-model="name">
                </div>
                <div class="mb-3">
                    <label for="desc">Description</label>
                    <textarea class="form-control" id="desc" cols="30" rows="5" v-model="description"></textarea>
                </div>
                <div class="d-flex justify-content-between gap-3">
                    <button type="reset" class="w-100 btn btn-secondary">Cancel</button>
                    <button type="submit" class="w-100 btn btn-info">Update</button>
                </div>
            </form>
        </div>
    </div>
</template>

<script>
export default {
    props: ['id'],
    data() {
        return {
            name: "",
            description: ""
        }
    },
    mounted() {
        fetch('http://localhost:3000/projects/' + this.id)
            .then(res => res.json())
            .then(data => {
                this.name = data.name;
                this.description = data.description;
            })
            .catch(err => console.log(err));
    },
    methods: {
        handleSubmit() {
            let project = {
                name: this.name,
                description: this.description
            }
            fetch('http://localhost:3000/projects/' + this.id, {
                method: "PATCH",
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify(project)
            })
                .then(_ => {
                    this.$router.push('/');
                })
                .catch(err => {
                    console.log(err)
                })
        }
    }
}
</script>

<style>

</style>