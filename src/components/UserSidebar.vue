<template>
  <div class="dropdown">
    <button
      class="btn btn-secondary dropdown-toggle"
      type="button"
      id="dropdownMenuButton"
      data-bs-toggle="dropdown"
      aria-expanded="false"
    >
      Select User
    </button>
    <ul class="dropdown-menu" aria-labelledby="dropdownMenuButton">
      <li v-for="user in users" :key="user.id">
        <a class="dropdown-item" href="#" @click.prevent="selectUser(user)">
          {{ user.name }}
        </a>
      </li>
    </ul>
  </div>
</template>

<script>
import 'bootstrap/dist/css/bootstrap.css'
export default {
  name: 'UserSidebar',
  props: {
    users: {
      type: Array,
      required: true
    }
  },
  mounted() {
    console.log('Users in Dropdown:', this.users); // Log users for debugging
  },
  methods: {
    selectUser(user) {
      this.$emit('user-selected', user);
    }
  }
};
</script>

<style>
.dropdown {
  display: inline-block;
  width: fit-content;
}
</style>
