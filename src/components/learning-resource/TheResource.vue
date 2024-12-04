<template>



  <base-card>
    <base-button @click="seletedTab = 'stored-resource'" :mode="storedResourceMode"
      >Stored Resources</base-button
    >
    &nbsp;
    <base-button @click="seletedTab = 'add-resource'" :mode="AddResourceMode"
      >Add Resource</base-button
    >
  </base-card>
  <keep-alive>
    <component :is="seletedTab"></component>
  </keep-alive>
</template>


<script>
import StoredResource from './StoredResource.vue'
import AddResource from './AddResource.vue'

export default {
  components: {
    StoredResource,
    AddResource,
  },
  data() {
    return {
      seletedTab: 'stored-resource',

      storedResources: [
        {
          id: 1,
          title: 'Learn Vue',
          description: 'Learn Vue js is a JavaScript framework for building user interfaces.',
          link: 'https://vuejs.org',
        },
        {
          id: 2,
          title: 'Learn React',
          description: 'Learn React is a JavaScript framework for building user interfaces.',
          link: 'https://reactjs.org',
        },

        {
          id: 3,
          title: 'Learn Angular',
          description: 'Learn Angular is a JavaScript framework for building user interfaces.',
          link: 'https://angular.io',
        },
      ],

      // addResourceData: this.addResourceData,
    }
  },

  provide() {
    return {
      resources: this.storedResources,
      addResourceData: this.addResourceData,
      deleteResource: this.deleteResource
    }
  },

  computed: {
    storedResourceMode() {
      return this.seletedTab === 'stored-resource' ? null : 'flat'
    },
    AddResourceMode() {
      return this.seletedTab === 'add-resource' ? null : 'flat'
    },
  },

  methods: {
    setSelectedTab(tab) {
      this.seletedTab = tab
    },

    addResourceData(title, description, url) {
      const newResource = {
        id: new Date().toISOString(),
        title: title,
        description: description,
        link: url,
      }
      this.storedResources.unshift(newResource)
      this.seletedTab = 'stored-resource'
    },
    deleteResource(resId) {
      const resIndex = this.storedResources.findIndex((res)=> res.id === resId);
      this.storedResources.splice(resIndex, 1)
    }
  },
}
</script>
