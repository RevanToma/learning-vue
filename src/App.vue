<template>
  <section>
    <header>
      <h1>My Friends</h1>
    </header>
    <new-friend @add-contact="addContact"></new-friend>
    <ul>
      <friend-contact
        v-for="friend in friends"
        :id="friend.id"
        :key="friend.id"
        :name="friend.name"
        :phone-number="+friend.phone"
        :email-adress="friend.email"
        :is-favorite="friend.isFavorite"
        @toggle-favorite="toggleFavStatus"
        @deleteContact="deleteContact"
      ></friend-contact>
    </ul>
  </section>
  <div class="activeUs">
    <label class="activeUsersLabel">Active Users:</label>
    <button @click="displayUsers">
      {{ showUsers ? "Hide active users" : "Show active users" }}
    </button>
  </div>
  <section v-show="showUsers">
    <div class="activeUs">
      <active-user
        v-for="user in activeUser"
        :key="user.id"
        :id="user.id"
        :name="user.name"
        :age="user.age"
        @deleteUser="deleteUser"
      ></active-user>
    </div>
  </section>
  <user-data @add-user-data="addUserData"></user-data>
</template>

<script>
export default {
  data() {
    return {
      friends: [{}],
      activeUser: [{}],
      showUsers: true,
    };
  },
  methods: {
    displayUsers() {
      this.showUsers = !this.showUsers;
    },
    toggleFavStatus(friendId) {
      const idFriend = this.friends.find((friend) => friend.id === friendId);
      idFriend.isFavorite = !idFriend.isFavorite;
    },
    addContact(name, phone, email) {
      const newFriend = {
        id: new Date().toISOString(),
        name,
        phone,
        email,
        isFavorite: false,
      };
      if (newFriend.name && newFriend.phone && newFriend.email) {
        if (isNaN(phone)) {
          alert("Please provide a valid phone number");
          return;
        }
        this.friends.push(newFriend);
      }
      return;
    },
    deleteContact(friendId) {
      this.friends = this.friends.filter((friend) => friend.id !== friendId);
    },
    addUserData(name, age) {
      if (isNaN(age)) {
        alert("Please provide a valid age");
        return;
      }

      const newUser = {
        id: new Date().toISOString(),
        name,
        age,
      };
      this.activeUser.push(newUser);
    },
    deleteUser(id) {
      this.activeUser = this.activeUser.filter((user) => user.id !== id);
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Jost&display=swap");
* {
  box-sizing: border-box;
}

html {
  font-family: "Jost", sans-serif;
}

body {
  margin: 0;
}
#app .activeUsersLabel {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
}
header {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  margin: 3rem auto;
  border-radius: 10px;
  padding: 1rem;
  background-color: #58004d;
  color: white;
  text-align: center;
  width: 90%;
  max-width: 40rem;
}

#app ul {
  margin: 0;
  padding: 0;
  list-style: none;
}
.activeUs {
  display: flex;
  flex-direction: column;
  align-items: center;
}

#app li,
#app form {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  margin: 1rem auto;
  border-radius: 10px;
  padding: 1rem;
  text-align: center;
  width: 90%;
  max-width: 40rem;
}

#app h2 {
  font-size: 2rem;
  border-bottom: 4px solid #ccc;
  color: #58004d;
  margin: 0 0 1rem 0;
}

#app button {
  font: inherit;
  cursor: pointer;
  border: 1px solid #ff0077;
  background-color: #ff0077;
  color: white;
  padding: 0.05rem 1rem;
  box-shadow: 1px 1px 2px rgba(0, 0, 0, 0.26);
  margin: 0.5rem;
  border-radius: 5px;
}

#app button:hover,
#app button:active {
  background-color: #ec3169;
  border-color: #ec3169;
  box-shadow: 1px 1px 4px rgba(0, 0, 0, 0.26);
}
</style>
