<template>
  <base-card>
    <base-button
      :mode="storedResSelected"
      @click="setSelectedTab('stored-resourses')"
      >Stored resources</base-button
    >
    <base-button :mode="addResSelected" @click="setSelectedTab('add-resource')"
      >Add Resource</base-button
    >
  </base-card>

  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
</template>

<script>
import StoredResourses from "./StoredResourses.vue";
import AddResource from "./AddResource.vue";
export default {
  components: {
    StoredResourses,
    AddResource,
  },
  data() {
    return {
      selectedTab: "stored-resourses",
      storedResources: [
        {
          id: "official-guide",
          title: "Official Guide",
          description: "The official Vuejs documentation",
          link: "https://vuejs.org",
        },
        {
          id: "google",
          title: "Google",
          description: "Learn to google...",
          link: "https://google.com",
        },
      ],
    };
  },
  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
    };
  },
  computed: {
    storedResSelected() {
      return this.selectedTab !== "stored-resourses" ? "flat" : null;
    },
    addResSelected() {
      return this.selectedTab !== "add-resource" ? "flat" : null;
    },
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    addResource(title, description, url) {
      const newResource = {
        id: new Date().toISOString(),
        title: title,
        description: description,
        link: url,
      };

      this.storedResources.unshift(newResource);
      this.selectedTab = "stored-resourses";
    },
  },
};
</script>