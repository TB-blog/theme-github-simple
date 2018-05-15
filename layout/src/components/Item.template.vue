<style lang="stylus">
@import '../../../source/style/Item.styl';
</style>

<template>
  <li class="blogs-item" :class="{ 'list-item-left': type === 'blog' }">
    <div class="post" @click="goToItem(type, item)">
      <span class="score">{{ item.stargazers_count }}</span>
      <span class="title">
        <template v-if="type === 'blog'">
          <a rel="noopener">{{ item.title }}</a>
        </template>
        <template v-else>
          {{ item.name }}
        </template>
      </span>
      <br>
      <span class="meta">
        <template v-if="type === 'blog'">
          <span class="time">
            {{ item.created_at | timeFormat }}
          </span>
          <span v-if="item.labels"
            class="labels"
            v-for="label in item.labels.slice(0, 2)"
            :key="label.id">
            #{{ label.name }}
          </span>
        </template>
        <template v-else>
          <span class="time">
            {{ item.description }}
          </span><br>
          <span v-if="item.license" class="time">
            {{ item.license.name }}
          </span>
        </template>
      </span>
    </div>
  </li>
</template>

<script>
export default {
  methods: {
    goToItem (type, item) {
      if (type === 'blog') {
        this.$router.push(`/item/${item.number}`);
      }
      if (type === 'repo') {
        window.location = `https://github.com/${this.$_config.user}/${item.name}`;
      }
    }
  }
}
</script>
