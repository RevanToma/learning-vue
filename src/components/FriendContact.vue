<template>
  <li v-if="id">
    <h2>{{ name }} {{ isFavorite ? "(Favorite)" : "" }}</h2>
    <button @click="toggleDetails">
      {{ detailsVisible ? "Hide" : "Show" }} Details
    </button>
    <button @click="toggleIsFavorite">Toggle Favorite</button>
    <ul v-if="detailsVisible">
      <li><strong>Phone:</strong> {{ phoneNumber }}</li>
      <li><strong>Email:</strong> {{ emailAdress }}</li>
    </ul>
    <button @click="$emit('deleteContact', this.id)">Delete Contact</button>
  </li>
</template>

<script>
export default {
  // props: ["name", "phoneNumber", "emailAdress", "isFavorite"],
  props: {
    id: {
      type: String,
      required: true,
    },
    name: String,
    emailAdress: String,
    phoneNumber: {
      type: Number,
      required: true,
    },
    isFavorite: {
      type: Boolean,
      required: false,
      default: false,
    },
  },
  emits: ["toggle-favorite", "deleteContact"],
  // emits: {
  //   "toggle-favorite": (id) => {
  //     if (id) {
  //       return true;
  //     } else {
  //       console.warn("id is missing");
  //       return true;
  //     }
  //   },
  // },
  data() {
    return {
      detailsVisible: false,
    };
  },
  methods: {
    toggleDetails() {
      this.detailsVisible = !this.detailsVisible;
    },
    toggleIsFavorite() {
      this.$emit("toggle-favorite", this.id);
    },
  },
};
</script>
