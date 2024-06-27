<template>
  <div>
    <h2>Posts</h2>
    <ul>
      <li v-for="post in filteredPosts" :key="post.id" @click="selectPost(post)" data-bs-toggle="modal" data-bs-target="#postModal">
        <strong>{{ post.title }}</strong>
      </li>
    </ul>

    <!-- Modal -->
    <div class="modal fade" id="postModal" tabindex="-1" aria-labelledby="postModalLabel" aria-hidden="true">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="postModalLabel">{{ selectedPost?.title }}</h5>
            <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
          </div>
          <div class="modal-body">
            <p>{{ selectedPost?.body }}</p>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PostList',
  props: {
    posts: Array,
    selectedUser: Object
  },
  data() {
    return {
      selectedPost: null
    };
  },
  computed: {
    filteredPosts() {
      if (this.selectedUser) {
        return this.posts.filter(post => post.userId === this.selectedUser.id);
      }
      return this.posts;
    }
  },
  methods: {
    selectPost(post) {
      this.selectedPost = post;
    }
  }
};
</script>


<style>
.main {
  display: block; 
  flex-direction: row;
  width: 100%;
  height: 10;
}

h2{
  text-align: center;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  padding: 10px;
  cursor: pointer;
  border-bottom: 1px solid #bdc3c7;
  transition: background-color 0.3s;
}

li:hover {
  background-color: #bdc3c7;
}

li strong {
  color: #2980b9;
}

.post-details {
  margin-top: 20px;
  padding: 20px;
  background: #fff;
  border: 1px solid #bdc3c7;
  border-radius: 4px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}
</style>
