<template>
  <div class="forum-listing">
    <div class="forum-details">
        <router-link :to="{name: 'forum', params: {id: forum['.key']}}" class="forum-name">{{forum.name}}</router-link>

        <p class="forum-description ">{{forum.description}}</p>
    </div>

    <div class="threads-count">
        <p class="count text-lead">{{threadsCount}}</p>
        {{threadsCount === 1 ? 'thread' : 'threads'}}
    </div>

    <div class="last-thread">
      <!-- TODO: implement later -->
    </div>
  </div> 
</template>

<script>
export default {
  props: {
    forum: {
      required: true,
      type: Object
    }
  },

  computed: {
    threadsCount () {
      return this.forum.threads ? Object.values(this.forum.threads).length : 0
    }
  }
}
</script>