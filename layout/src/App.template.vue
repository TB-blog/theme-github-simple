<style lang="stylus">
@import '../../source/style/App.styl';
</style>

<template>
  <div id="app">
    <header v-if="!this.$route.fullPath.match(/error/)" class="header">
      <a class="avatar"
        :href="user.html_url"
        target="_blank"
        rel="noopener">
        <img :src="user.avatar_url" alt="avatar">
      </a>
      <h1 class="username">{{ user.name }}</h1>
      <p class="bio">{{ user.bio }}</p>
      <div class="social">
        <router-link to="/blog">
          <i class="iconfont icon-blog"></i>
        </router-link>
        <router-link to="/repo">
          <i class="iconfont icon-github"></i>
        </router-link>
        <a v-if="user.blog"
          :href="user.blog"
          target="_blank"
          rel="noopener">
          <i class="iconfont icon-home"></i>
        </a>
        <a v-if="user.email"
          :href="`mailto:${user.email}`">
          <i class="iconfont icon-email"></i>
        </a>
      </div>
    </header>
    <transition name="fade" mode="out-in">
      <router-view class="view"></router-view>
    </transition>
  </div>
</template>

<script>
export default {
  data () {
    return {
      user: this.$store.state.user
            || this.$store.state.issues[0].user
            || this.$store.state.singleIssue.user
    };
  }
}
</script>
