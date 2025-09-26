<template>
  <base-card>
    <base-button @click="setSelectedTab('stored-resources')" :mode="storedResButton"
      >Stored Resources</base-button
    >
    <base-button @click="setSelectedTab('add-resources')" :mode="addResButton"
      >Add Resources</base-button
    >
  </base-card>
  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
</template>

<script>
import StoredResources from './StoredResources.vue'
import AddResources from './AddResources.vue'

export default {
  components: {
    StoredResources,
    AddResources,
  },
  data() {
    return {
      selectedTab: 'stored-resources',
      storedResources: [
        {
          id: 'official-guide',
          title: 'Official Guide',
          description: 'The official Vue.js documentation.',
          link: 'https://vuejs.org',
        },
        {
          id: 'google',
          title: 'Google',
          description: 'Learn to Google.',
          link: 'https://google.com',
        },
      ],
    }
  },
  provide() {
    return {
      resources: this.storedResources,
      addResources: this.addResources,
      removeResources: this.removeResources,
    }
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab
    },
    addResources(title, description, url) {
      const newResource = {
        id: new Date().toISOString(),
        title: title,
        description: description,
        link: url,
      }
      this.storedResources.unshift(newResource)
      this.selectedTab = 'stored-resources'
    },
    removeResources(resID) {
      const resIndex = this.storedResources.findIndex((res) => res.id === resID)
      this.storedResources.splice(resIndex, 1)
    },
  },
  computed: {
    storedResButton() {
      return this.selectedTab === 'stored-resources' ? '' : 'flat'
    },
    addResButton() {
      return this.selectedTab === 'add-resources' ? '' : 'flat'
    },
  },
}
</script>
