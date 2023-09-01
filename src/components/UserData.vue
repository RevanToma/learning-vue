<template>
  <form @submit.prevent="addUserData">
    <div>
      <label for="name">Name: </label>
      <input type="text" v-model="enteredName" />
    </div>
    <div>
      <label for="age">Age</label>
      <input type="text" v-model="enteredAge" />
    </div>
    <div>
      <button>Add User Data</button>
    </div>
  </form>
</template>

<script>
export default {
  emits: ["add-user-data"],
  data() {
    return {
      enteredName: "",
      enteredAge: "",
    };
  },
  methods: {
    addUserData() {
      if (this.enteredName && this.enteredAge) {
        this.$emit("add-user-data", this.enteredName, this.enteredAge);
      }
      return;
    },
  },
};
</script>
