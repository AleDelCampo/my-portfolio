<script>

import {store} from '../store.js';

export default {
    name: 'AppHeader',
    data() {
        return {
            store,
        };
    },
    methods: {
        filterProjects() {
            this.$emit('filter-projects', this.filterQuery);
        },

        applyFilter(filterQuery) {

            if (store.filterQuery.trim() === '') {
                store.filteredProjects = store.projects;
            } else {
                store.filteredProjects = store.projects.filter(project =>
                    project.title.toLowerCase().includes(store.filterQuery.toLowerCase())
                );
                console.log("sono nell'else")
            }
            console.log(store.filterQuery)
        }
    }
}
</script>


<template>

    <header class="bg-nav">
        <div class="container">
            <nav class="navbar">
                <div class="container-fluid d-flex justify-content-between h">

                    <a href="#">
                        <router-link :to="{ name: 'home' }"><img src="/public/MyLogo.png" class="logo"></router-link>
                    </a>

                    <div>
                        <input class="form-control" type="search" v-model="store.filterQuery" placeholder="Search Projects...." @keyup="applyFilter(store.filterQuery)">
                    </div>

                </div>
            </nav>
        </div>
    </header>

</template>

<style lang="scss">
    .bg-nav {
        background-color: #211951;
    }

    .logo {
        border-radius: 24px;
        width: 140px;
        height: 80px;
    }
</style>