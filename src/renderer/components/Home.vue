<template>
  <div>
    <div
      v-if="loading"
      class="loading"
    >
      <span>Loading...</span>
    </div>
    <webview
      ref="webview"
      class="webview"
      :src="url"
    />
  </div>
</template>

<script>
export default {

  data () {
    return {
      url: 'https://app.zeplin.io/projects',
      loading: true
    }
  },

  mounted () {
    this.$refs.webview
      .addEventListener('did-stop-loading', this.handleLoadingStop)
  },

  destroyed () {
    this.$refs.webview
      .removeEventListener('did-stop-loading', this.handleLoadingStop)
  },

  methods: {
    handleLoadingStop () {
      this.loading = false
    }
  }
}
</script>

<style lang="scss" scoped>
.loading {
  position: fixed;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}

.webview {
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
}
</style>
