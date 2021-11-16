<template>
  <div>
    <h2 class="m-b-15">Страница с постами</h2>
    <div>
      <input-default
        v-model="searchQuery"
        placeholder="Search..."
      />
    </div>
    <div class="app__buttons">
      <button-default @click="showModal">
        Открыть модальное окно
      </button-default>
      <select-default
        v-model="selectedSort"
        :options="sortOptions"
      />
    </div>
    <modal-default v-model:show="modalVisible">
      <post-form
        @create="createPost"
      />
    </modal-default>
    <post-form
      @create="createPost"
    />
    <post-list
      class="m-b-15"
      :posts="sortedAndSerchedPosts"
      @remove="removePost"
      v-if="!isPostsLoading"
    />
    <h4 v-else>Идёт загрузка постов...</h4>
    <div v-intersection class="observer"></div>
    <!-- <pagination-default :totalPages="totalPages" :currentPage="page" @update="changePage"/> -->
  </div>
</template>

<script>
  import PostForm from '@/components/PostForm.vue';
  import PostList from '@/components/PostList.vue';
  import axios from 'axios';

  export default {
    components: {
      PostForm,
      PostList,
    },
    data() {
      return {
        posts: [],
        modalVisible: false,
        isPostsLoading: false,
        searchQuery: '',
        selectedSort: '',
        sortOptions: [
          {value: 'title', name: 'По названию'},
          {value: 'body', name: 'По описанию'},
          {value: 'id', name: 'По идентификатору'}
        ],
        page: 1,
        limit: 10,
        totalPages: 0
      }
    },
    methods: {
      createPost(post) {
        this.posts.push(post);
        this.modalVisible = false;
      },
      removePost(post) {
        this.posts = this.posts.filter((p) => p.id !== post.id);
      },
      showModal() {
        this.modalVisible = true;
      },
      async fetchPosts() {
        try {
          this.isPostsLoading = true;
          const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
            params: {
              _page: this.page,
              _limit: this.limit
            }
          });
          this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit);
          this.posts = response.data;
        } catch (e) {
          console.log('Error');
        } finally {
          this.isPostsLoading = false;
        }
      },
      async loadMorePosts() {
        try {
          this.page += 1;
          const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
            params: {
              _page: this.page,
              _limit: this.limit
            }
          });
          this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit);
          this.posts = [...this.posts, ...response.data];
        } catch (e) {
          console.log('Error');
        }
      },
      // changePage(numberPage) {
      //   this.page = numberPage;
      // }
    },
    mounted() {
      this.fetchPosts();

      // let options = {
      //   rootMargin: '0px',
      //   threshold: 1.0
      // }

      // let callback = (entries, observer) => {
      //   if (entries[0].isIntersecting && this.page < this.totalPages) {
      //     this.loadMorePosts();
      //   }
      // }

      // let observer = new IntersectionObserver(callback, options);
      // observer.observe(this.$refs.observer);
    },
    computed: {
      sortedPosts() {
        return [...this.posts].sort((post1, post2) => {
          return String(post1[this.selectedSort])?.localeCompare(String(post2[this.selectedSort]))
        })
      },
      sortedAndSerchedPosts() {
        return this.sortedPosts.filter((post) => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
      }
    },
    watch: {
      // page() {
      //   this.fetchPosts();
      // }
    }
  }
</script>

<style>
  .m-b-15 {
    margin-bottom: 15px;
  }

  .app__buttons {
    display: flex;
    justify-content: space-between;
  }

  .observer {
    height: 30px;
    background: red;
  }
</style>