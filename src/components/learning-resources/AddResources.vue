<template>
  <base-dialog v-if="inputIsInvalid" title="Invalid Input" @close="confirmError">
    <template #default>
      <p>Unfortunately, at least one of the input is invalid</p>
      <p>Please check all the inputs and try again</p>
    </template>
    <template #actions>
      <base-button @click="confirmError">Okay!!!</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label for="title">Title</label>
        <input type="text" name="title" id="title" ref="titleInput" />
      </div>
      <div class="form-control">
        <label for="title">Description</label>
        <textarea name="description" id="description" rows="3" ref="descInput" />
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input type="url" name="link" id="link" ref="linkInput" />
      </div>
      <div class="form-control">
        <base-button type="submit">Add Resource</base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
export default {
  data() {
    return {
      inputIsInvalid: false,
    }
  },
  inject: ['addResources'],
  methods: {
    submitData() {
      const enteredTitle = this.$refs.titleInput.value
      const enteredDescription = this.$refs.descInput.value
      const enteredLink = this.$refs.linkInput.value

      if (
        enteredTitle.trim() === '' ||
        enteredDescription.trim() === '' ||
        enteredLink.trim() === ''
      ) {
        this.inputIsInvalid = true
        return
      }

      this.addResources(enteredTitle, enteredDescription, enteredLink)
    },
    confirmError() {
      this.inputIsInvalid = false
    },
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
