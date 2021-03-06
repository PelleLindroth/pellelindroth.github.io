<template>
  <div>
    <div
      class="projects-view-wrapper"
      :style="{ gridTemplateRows: calculateRows }"
    >
      <ImageModal
        v-if="showModal"
        @closeModal="closeModal"
        :showModal="showModal"
        :images="modalImages"
        :imageIndex="modalIndex"
      />
      <div class="page-description">
        <em v-html="$t('projects.page-description')"> </em>
      </div>
      <ProjectDescription
        v-for="project of this.projects"
        :key="project.id"
        :project="project"
      />
      <ProjectImageContainer
        v-for="project of this.projects"
        :key="'image ' + project.id"
        :project="project"
        @openModal="openModal"
      />
    </div>
  </div>
</template>

<script>
import ProjectDescription from '../components/ProjectDescription'
import ProjectImageContainer from '../components/ProjectImageContainer'
import ImageModal from '../components/ImageModal'
import projects from '../data/projects'

export default {
  components: {
    ImageModal,
    ProjectDescription,
    ProjectImageContainer,
  },
  computed: {
    calculateRows() {
      let multiplier = this.$root.isMobile ? 6 : 7
      return `repeat(${this.projects.length * multiplier}, 64px)`
    },
    title() {
      return this.$root.$i18n.locale == 'sv'
        ? 'Pelle Lindroth | Projekt'
        : 'Pelle Lindroth | Projects'
    },
  },
  updated() {
    document.title = this.title
  },
  data() {
    return {
      modalImages: [],
      modalIndex: 0,
      projects,
      showModal: false,
    }
  },
  created() {
    document.title = this.title
  },
  methods: {
    closeModal() {
      this.showModal = false
      document.body.style.overflow = 'scroll'
    },
    openModal(images, index) {
      this.modalImages = images
      this.modalIndex = index
      this.showModal = true
      document.body.style.overflow = 'hidden'
    },
  },
}
</script>

<style lang="scss" scoped>
$mobile-cutoff: 750px;

.projects-view-wrapper {
  display: grid;
  gap: 1rem;
  grid-template-columns: repeat(12, 1fr);
  margin: 4rem auto 0;
  max-width: 120rem;

  @media screen and (max-width: $mobile-cutoff) {
    gap: 1rem;
    grid-template-columns: repeat(8, 1fr);
    margin: auto;
    padding: 0 1rem;
    width: 100vw;
    min-height: 100vh;
  }

  .page-description {
    color: #ececec;
    font-size: 2rem;
    font-weight: 300;
    grid-column: 1 / span 6;
    grid-row: 1 / span 2;

    @media screen and (max-width: $mobile-cutoff) {
      font-size: 1.4rem;
      grid-column: 1 / span 8;
      grid-row: 1 / span 3;
      margin-top: 3rem;
    }
  }
}
</style>
