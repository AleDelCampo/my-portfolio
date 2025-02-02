<script>
import axios from 'axios';
import ProjectCards from '../components/ProjectCards.vue';

export default {
  name: 'SingleProject',

  components: {
    ProjectCards
  },

  data() {
    return {
      project: null,
      projectSlug: null,
      projects: [],
      "technologies": [
        {
          id: 1, name: "HTML", preview: "HTML.jpg"
        },
        {
          id: 2, name: "CSS", preview: "CSS.jpg"
        },
        {
          id: 3, name: "Bootstrap", preview: "Bootstrap.jpg"
        },
        {
          id: 4, name: "JavaScript", preview: "JS.png"
        },
        {
          id: 5, name: "Vue.Js", preview: "Vue.Js.png"
        },
        {
          id: 6, name: "Mamp",preview: "Mamp.webp"
        },
        {
          id: 7, name: "PHP", preview: "PHP.png"
        },
        {
          id: 8, name: "Laravel", preview: "Laravel.png"
        }
      ],
      types: [
        { id: 1, title: "Music Platform" },
        { id: 2, title: "Streaming Platform" },
        { id: 3, title: "Message Platform" },
        { id: 4, title: "Web App Comics Library" },
        { id: 5, title: "B&B Platform" },
        { id: 6, title: "Personal Blog, Work In Progress" }
      ]
    };
  },

  mounted() {
    this.projectSlug = this.$route.params.slug;
    this.loadProjects();
  },

  methods: {
    loadProjects() {
      // Carica i progetti dal file JSON
      axios.get('/projects.json')
        .then(res => {
          this.projects = res.data.results.data;
          this.project = this.projects.find(project => project.slug === this.projectSlug);
          if (!this.project) {
            this.$router.push({ name: 'error404' });  // Se il progetto non esiste, reindirizza alla pagina 404
          } else {
            // Mappa gli ID delle tecnologie ai dati completi
            this.project.technologies = this.project.technologies.map(id =>
              this.technologies.find(tech => tech.id === id)
            );

            // Mappa il tipo al dato completo
            this.project.type = this.types.find(type => type.id === this.project.type);
          }
        })
        .catch(err => {
          console.error('Errore nel caricamento dei progetti:', err);
        });
    }
  }
}
</script>

<template>
  <div v-if="project" class="my-cnt">
    <ProjectCards class="mb-5" :project="project"></ProjectCards>

    <div v-if="project.technologies.length" class="mb-5">
      <h3>Technologies Used:</h3>
      <ul class="d-flex">
        <li v-for="tech in project.technologies" :key="tech.id">
          <img class="img-cnt" :src="`../public/projects/${tech.preview}`" alt="" />
          <p class="me-4">{{ tech.name }}</p>
        </li>
      </ul>
    </div>

    <div v-if="project.type">
      <h3>Project Type: <span class="my-color">{{ project.type.title }}</span></h3>
    </div>
  </div>

  <div v-else>
    <div class="spinner-border" role="status">
      <span class="visually-hidden">Loading...</span>
    </div>
  </div>
</template>

<style lang="scss" scoped>

.img-cnt {
  width: 140px;
  height: 80px;
}

.my-cnt {
  padding: 40px;
}

.my-color {
  color: black;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}

img {
  width: 30px;
  height: 30px;
  margin-right: 10px;
}
</style>
