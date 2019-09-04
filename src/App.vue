<template>
  <div id="app">
    <select
      v-model="lang"
      @change="createBtn">
      <option value="ja_JP">日本語</option>
      <option value="en_US">英語</option>
      <option value="de_DE">ドイツ語</option>
    </select>
    <div
      class="fb-like"
      data-href="https://developers.facebook.com/docs/plugins/"
      data-width=""
      data-layout="button"
      data-action="like"
      data-size="small"
      data-show-faces="false"
      data-share="false">
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      lang: 'ja_JP'
    }
  },
  methods: {
    createBtn: function () {
      window.FB = null
      const fbsdkElem = document.getElementById('fb-sdk')
      if (fbsdkElem) fbsdkElem.parentNode.removeChild(fbsdkElem)
      const fbrootElem = document.getElementById('fb-root')
      if (fbrootElem) fbrootElem.parentNode.removeChild(fbrootElem)
      let scriptElem = document.createElement('script')
      scriptElem.id = 'fb-sdk'
      scriptElem.crossorigin = 'anonymous'
      scriptElem.async = true
      scriptElem.src = 'https://connect.facebook.net/' + this.lang + '/sdk.js#xfbml=1&version=v4.0'
      document.body.appendChild(scriptElem)
      if (window.FB) {
        window.FB.XFBML.parse()
      }
    }
  },
  mounted () {
    this.createBtn()
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.fb-like {
  width: 100px;
  height: 50px;
}
</style>
