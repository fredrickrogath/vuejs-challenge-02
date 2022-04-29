<template>
  <base-dialog v-if="inputIsInvalid" title="Invalid Input">
    <template #default>
      <p>One or more inputs is/are invalid, Make sure all inputs are filled</p>
    </template>

    <template #actions>
      <base-button @click="confirmError">Got it</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label for="title">Title</label>
        <input type="text" name="title" id="title" v-model="titleInput" />
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea
          name="description"
          id="description"
          rows="3"
          v-model="descInput"
        ></textarea>
      </div>
      <div class="form-control">
        <label for="link">Title</label>
        <input type="url" name="link" id="link" v-model="linkInput" />
      </div>

      <div>
        <base-button type="submit" @click.prevent="submitData"
          >Add Resource</base-button
        >
      </div>
    </form>
  </base-card>
</template>

<script>
export default {
  inject: ["addResource"],
  data() {
    return {
      titleInput: "",
      descInput: "",
      linkInput: "",
      inputIsInvalid: false,
    };
  },
  methods: {
    submitData() {
      if (
        this.titleInput.trim() === "" ||
        this.descInput.trim() === "" ||
        this.linkInput.trim() === ""
      ) {
        this.inputIsInvalid = true;
        return;
      }
      this.addResource(this.titleInput, this.descInput, this.linkInput);
    },
    confirmError() {
        this.inputIsInvalid = false;
    }
  },
};
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