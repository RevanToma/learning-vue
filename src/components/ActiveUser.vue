<template>
  <section>
    <div class="active-users" :key="name" v-if="id">
      <h2>Name: {{ name }}</h2>
      <h3>Age: {{ age }}</h3>
      <button v-if="name" @click="$emit('deleteUser', this.id)">
        Delete User
      </button>
    </div>
  </section>
</template>

<script>
export default {
  emits: ["deleteUser"],
  props: {
    name: { type: String, required: true },
    id: {
      type: String,
    },
    age: {
      type: String,
      required: true,
    },
  },
  data() {
    return {};
  },
};
</script>

<style>
#app .active-users {
  padding: 1rem;
  min-width: 20rem;
  margin: 1rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  box-shadow: 0px 0px 5px gray;
}
.active-users button {
  margin: 1rem;
}
</style>
