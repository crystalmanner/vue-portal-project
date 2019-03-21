<template>
  <div class="container">
    <div v-if="banner" class="backdrop-single">
      <img class="img-responsive" :src="banner"/>
    </div>
    <div class="site-header"
      :style="{ 'background-image': 'url(' + media[0] + ')' }"
      >
      <div class="row">
        <div class="thumb">
          <img :src="icon" width="100" height="100">
        </div>
        <ul>
          <li v-for="item in menu">
            <router-link :to="item.link" :class="{active: item.link === $route.path}">{{ item.title }}</router-link>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'SiteHeader',
  props: [
    'context',
    'buttons',
    'icon',
    'media',
    'menu',
    'banner'
  ],
  mounted () {
    console.log(this)
  }
}
</script>
<style scoped>
.container {
  position: relative;
  padding: 0;
}

.backdrop-single img {
  width: 100%;
}

.site-header {
  position: relative;
  margin-bottom: 80px;
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center center;
}

.row {
  background: white;
  position: absolute;
  bottom: -40px;
  width: 100%;
  margin: 0;
  height: 40px;
}

.thumb {
  float: left;
  position: relative;
  border: 3px solid white;
  left: 80px;
  top: -25px;
  margin-right: 100px;
}

ul {
  padding-top: 5px;
}

li {
  display: inline-block;
  font-size: 16px;
  margin-right: 25px;
  font-weight: 300;
  padding-top: 3px;
}

li a {
  color: #434343;
}

li a.active {
  color: black;
  font-weight: 500;
  text-transform: uppercase;
}

li.highlight {
  background: #1f55ff;
  color: white;
  padding: 3px 10px;
  text-transform: uppercase;
  font-weight: 400;
  margin-right: 0;
}
</style>
