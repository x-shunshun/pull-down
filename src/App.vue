<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style lang="scss">
$list: (768, 720, 640, 540, 480, 414, 412, 400, 393, 375, 360, 345, 320);

@each $screen in $list {
  @media only screen and (max-width: $screen + px) {
    html {
      font-size: ($screen / 7.5) + px;
    }
  }
}

html {
  font-size: 100 / 7.5 + vw;
  -webkit-text-size-adjust: none;
}

body {
  margin: 0;
  font-size: 16px;
  font-family: sans-serif
}
html, body { word-wrap: break-word; }
html, body, h1, h2, h3, h4, h5, h6, p, ul, ol, li, dl, dt, form, th, td, hr { margin: 0; padding: 0; }
body { min-width: 320px; background: #F5F5F5; color: #404040; font: 14px/1.3 sans-serif; outline: 0; -webkit-tap-highlight-color: rgba(0, 0, 0, 0); -webkit-text-size-adjust: none; -webkit-overflow-scrolling: touch; }
h1, h2, h3, h4, h5, h6, p, input, button, select, textarea { font-size: 14px; -webkit-tap-highlight-color: rgba(0, 0, 0, 0); outline: 0; }
ul, li { list-style: none; }
table { border-collapse: collapse; border-spacing: 0; width: 100%; }
caption, cite, em, strong, th { font-style: normal; font-weight: 400; }
caption, th { text-align: left; }
a, a:visited { color: #333; text-decoration: none; }
hr { margin: 13px -15px; border-top: 1px solid #ddd; border-bottom: none; }
    hr.style2 { border-top-style: dotted; }
p { margin: .5em 0; }
img { max-width: 100%; border: 0; }
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
