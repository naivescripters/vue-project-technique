<template>
  <div>
    <div class="user-info">
      <a href="#" class="user-name">{{ user.name }}</a>

      <a href="#">
        <img
          class="avatar-large"
          :src="user.avatar"
          alt=""
        />
      </a>

      <p class="desktop-only text-small">{{userPostCount}} posts</p>
    </div>

    <div class="post-content">
      <template v-if="!editing"> 
        <div>
          {{ post.text }}
        </div>
        <a @click="editing = true" href="#" style="margin-left: auto;" class="link-unstyled" title="Make a change"><i class="fa fa-pencil"></i>edit</a>
      </template>
      
      <div v-else>
        <PostEditor 
          :post="post" 
          @save="editing = false" 
          @cancel="editing = false"
        />
      </div>

    </div>
 
    <div class="post-date text-faded">
      <div v-if="post.edited" class="edition-info">edited</div>
      <AppDate :timestamp="post.publishedAt" />
    </div>
  </div>
</template>

<script>
import {countObjectProperties} from '@/utils'
import PostEditor from './PostEditor.vue'

export default {
  props: {
    post: {
      required: true,
      type: Object
    }
  },
  components: {
    PostEditor
  },
  data () {
    return {
      editing: false
    }
  },
  computed: {
    user () {
      return this.$store.state.users[this.post.userId]
    },
    userPostCount () {
      return countObjectProperties(this.user.posts)
    }
  }
}
</script>

<style>
</style>