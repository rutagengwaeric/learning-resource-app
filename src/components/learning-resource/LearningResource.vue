<template>
  <li>
    <base-card>
      <header>
        <h3>{{ title }}</h3>
        <base-button mode="flat" @click="deleteResource(id)">Delete</base-button>
      </header>

      <p>{{ description }}</p>
      <nav>
        <a :href="link">View Resource</a>
      </nav>
    </base-card>
  </li>
</template>

<script>
export default {
  inject : ['deleteResource'],
  props: ['id','title', 'description', 'link'],

  data() {
    return {}
  },
}
</script >

<style scoped>
li {
  list-style: none;
  margin-bottom: 20px;
  padding: 10px;
  border-radius: 5px;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
}

h3 {
  margin: 0;
}

a {
  color: #2196f3;
  text-decoration: none;
}

a:hover {
  text-decoration: underline;
}
</style>
