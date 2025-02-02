<script>
import { store } from '../store.js';
import ProjectCards from '../components/ProjectCards.vue';
import AppHeader from '../components/AppHeader.vue';
import AppJumbo from '../components/AppJumbo.vue';
import axios from 'axios';

export default {
    name: 'HomePage',
    components: {
        AppHeader,
        AppJumbo,
        ProjectCards
    },
    data() {
        return {
            store,
            projects: [],
            paginatedProjects: [],
            currentPage: 1,
            perPage: 2,
            totalPages: 0
        };
    },
    mounted() {
        this.loadProjects();
    },
    watch: {
        'store.filterQuery': 'applyFilter', // Aggiorna il filtro ogni volta che cambia store.filterQuery
    },
    computed: {
        filteredProjects() {
            return store.filteredProjects;
        }
    },
    methods: {
        loadProjects() {
            axios.get('/projects.json')
                .then(res => {
                    this.projects = res.data.results.data;
                    store.projects = this.projects;
                    this.totalPages = Math.ceil(this.projects.length / this.perPage);
                    this.updatePaginatedProjects();
                })
                .catch(err => {
                    console.error('Errore nel caricamento dei progetti:', err);
                });
        },

        updatePaginatedProjects() {
            // Filtra i progetti in base alla query di ricerca
            const filteredProjects = store.filteredProjects.length ? store.filteredProjects : this.projects;

            const start = (this.currentPage - 1) * this.perPage;
            const end = start + this.perPage;
            this.paginatedProjects = filteredProjects.slice(start, end);
        },

        changePage(pageNumber) {
            if (pageNumber > 0 && pageNumber <= this.totalPages) {
                this.currentPage = pageNumber;
                this.updatePaginatedProjects();
            }
        },

        applyFilter() {
            if (store.filterQuery.trim() === '') {
                store.filteredProjects = store.projects; // Se la query è vuota, mostriamo tutti i progetti
            } else {
                store.filteredProjects = store.projects.filter(project =>
                    project.title.toLowerCase().includes(store.filterQuery.toLowerCase())
                );
            }

            // Resetta la pagina corrente alla prima pagina dopo il filtro
            this.currentPage = 1;
            this.totalPages = Math.ceil(store.filteredProjects.length / this.perPage);
            this.updatePaginatedProjects();
        }
    }
};
</script>

<template>
    

    <div class="container w-75">
        <h1 class="mb-5">My Projects:</h1>

        <div v-if="paginatedProjects.length">
            <ul>
                <li v-for="project in paginatedProjects" :key="project.slug" class="mb-2 text ">
                    {{ project.title }} 
                    <router-link  class="btn my-btn" :to="{ name: 'single-project', params: { slug: project.slug } }">
                        Mostra
                    </router-link>
                </li>
            </ul>

            <nav>
                <ul class="d-flex gap-2">
                    <li v-if="currentPage > 1">
                        <button class="btn my-btn" @click="changePage(currentPage - 1)">Previous</button>
                    </li>

                    <li v-for="page in totalPages" :key="page">
                        <button class="btn my-btn" @click="changePage(page)" :class="{ active: page === currentPage }">
                            {{ page }}
                        </button>
                    </li>

                    <li v-if="currentPage < totalPages">
                        <button class="btn my-btn" @click="changePage(currentPage + 1)">Next</button>
                    </li>
                </ul>
            </nav>
        </div>

        <div v-else>
            <div class="spinner-border" role="status">
                <span class="visually-hidden">Loading...</span>
            </div>
        </div>
    </div>
    <AppJumbo></AppJumbo>
</template>

<style lang="scss" scoped>
nav {
  margin-bottom: 80px;
  padding-top: 20px;
  border-top: solid 1px gray;

  ul {
    list-style-type: none;

    button, li {
      text-decoration: none;
      color: black;
      background-color: #fd2bfd;
      transition: all .3s ease;
      cursor: pointer;
      border-radius: 5px;

      &:hover {
      background-color: transparent;
      color: white;
      }
    }
  }
}

.text {
  font-size: 24px;
}

.my-btn {
  border: 1px solid #fd2bfd;
  background-color: #fd2bfd;
  color: black;

  &:hover {
    background-color: transparent;
    color: white;
  }
}
</style>
