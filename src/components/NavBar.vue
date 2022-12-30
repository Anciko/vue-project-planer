<template>
    <nav>
        <router-link to="/" class="routerLink">Home</router-link>
        <router-link to="/add-project" class="routerLink">Add Project</router-link>
    </nav>
</template>

<script>
export default {

}
</script>

<style>
nav {
    display: flex;
    justify-content: center;
    gap: 10px;
    padding: 5px;
}

nav a {
    color: #333;
    padding: 10px;
    font-size: 17px;
    border-radius: 7px;
}

.routerLink:hover,
.routerLink:active {
    background: hsla(160, 100%, 37%, 1);
    text-decoration: none;
    color: #eef;
    transition: 0.4s;
}
</style>