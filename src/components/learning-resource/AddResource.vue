<template>
  <base-dialog v-if="inputIsInvalid" title="Invalid Input" @close="confirmError">

    <template #default>
      <p>Unfortunately, at least one input is invalid</p>
      <p>Please Check all inputs and make sure you enter at least a few characters into each input field</p>
    </template>
    <template #actions>
      <base-button @click="confirmError">Close</base-button>
    </template>

  </base-dialog>



  <base-card>
    <h1>Add Resource</h1>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label for="title">Title</label>
        <input type="text" id="title" name="title" ref="title" />
      </div>

      <div class="form-control">
        <label for="description">Description</label>
        <textarea id="description" name="description" rows="3" ref="description"></textarea>
      </div>

      <div class="form-control">
        <label for="link">Link</label>
        <input type="url" id="link" name="link" ref="link" />
      </div>

      <div>
        <base-button type="submit">Add Resource</base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
export default {

  inject: ['addResourceData'],

  data() {
    return {
      inputIsInvalid: false
    }
  },

  methods: {
    submitData() {

      const enteredTitle = this.$refs.title.value;
      const enteredDescription = this.$refs.description.value;
      const enteredLink = this.$refs.link.value;

      if(enteredTitle.trim() === '' || enteredDescription.trim() === '' || enteredLink.trim() === '') {
        this.inputIsInvalid = true
        return
      }
      this.addResourceData(enteredTitle, enteredDescription, enteredLink);

      this.$refs.title.value = '';
      this.$refs.description.value = '';
      this.$refs.link.value = '';

    },
    confirmError() {
      this.inputIsInvalid = false
    }
  },
}
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>
