<template>
  <div id="app">
    <div class="sidebar">
      <UserSidebar :users="users" @user-selected="handleUserSelected" />
    </div>
    <div class="content">
      <PostList :posts="posts" :selectedUser="selectedUser" />
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import UserSidebar from './components/UserSidebar.vue';
import PostList from './components/PostList.vue';

export default {
  name: 'App',
  components: {
    UserSidebar,
    PostList
  },
  data() {
    return {
      users: [],
      posts: [],
      selectedUser: null
    };
  },
  created() {
    this.fetchData();
  },
  methods: {
    async fetchData() {
      try {
        const usersResponse = await axios.get('https://jsonplaceholder.typicode.com/users');
        const postsResponse = await axios.get('https://jsonplaceholder.typicode.com/posts');
        this.users = usersResponse.data;
        this.posts = postsResponse.data;
        console.log('Users:', this.users);
        console.log('Posts:', this.posts); 
      } catch (error) {
        console.error('Error fetching data', error);
      }
    },
    handleUserSelected(user) {
      this.selectedUser = user;
    }
  }
};
</script>

<style>
#app {
  display: flex;
  width: 100%;
  height: 100vh;
  font-family: Arial, sans-serif;
}

.sidebar {
  min-width: 200px;
  padding: 20px;
  background: #2c3e50;
  color: #ecf0f1;
  border-right: 1px solid #34495e;
  overflow-y: auto;
}


.content {
  /* min-width: 700px; */
  flex: 1;
  padding: 20px;
  background: #ecf0f1;
  overflow-y: auto;
}

h2 {
  margin-top: 0;
}
</style>
