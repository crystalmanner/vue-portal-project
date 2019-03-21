<template>
  <div id="header" v-if="context.header" v-on:mouseleave="displayMenu = false">
    <div class="container">
      <nav class="navbar navbar-default top">
        <div class="container-fluid">
          <div class="navbar-header">
            <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#navbar1">
              <span class="sr-only">Toggle navigation</span>
              <span class="icon-bar"></span>
              <span class="icon-bar"></span>
              <span class="icon-bar"></span>
            </button>
            <a class="navbar-brand" href="#"><img class="logo" src="../assets/logo.png" alt="logo">
            </a>
            <div class="search">
              <input type="text" placeholder="Search">
            </div>
          </div>
          <div id="navbar1" class="navbar-collapse collapse">
            <ul class="nav navbar-nav">
              <li class="dropdown" v-for="(menus, index) in context.header.selectors">
                <a class="dropdown-toggle" data-toggle="dropdown" role="button" aria-expanded="false">{{ menus.title }} <span class="caret"></span></a>
                <ul class="dropdown-menu" role="menu">
                  <li v-for="link in context.header.selectors[index].links">
                    <router-link :to="link.page">{{ link.title }}</router-link>
                  </li>
                </ul>
              </li>
            </ul>
          </div><!--/.nav-collapse -->
        </div><!--/.container-fluid -->
        <div class="top-right">
          <div class="social">
            <a href="#"><img src="../assets/icons/facebook.png"></a>
            <a href="#"><img src="../assets/icons/twitter.png"></a>
            <a href="#"><img src="../assets/icons/profile.png"></a>
          </div>
        </div>
      </nav>
    </div>
    <!-- <div class="container">
      <div class="clearfix top">
        <i class="glyphicon glyphicon-menu-hamburger pull-left"></i>
        <router-link to="/">
          <img class="logo" src="../assets/logo.png">
        </router-link>
        <div class="search">
          <input type="text" placeholder="Search">
        </div>
        <div class="top-right">
          <div class="drop-down-menus">
            <ul v-for="(menus, index) in context.header.selectors">
              <li v-on:click="setActiveMenu(index)">{{ menus.title }} <i class="glyphicon glyphicon-menu-down"></i></li>
            </ul>
          </div>
          <div class="social">
            <a href="#"><img src="../assets/icons/facebook.png"></a>
            <a href="#"><img src="../assets/icons/twitter.png"></a>
            <a href="#"><img src="../assets/icons/profile.png"></a>
          </div>
        </div>
      </div>
    </div> -->
    <div class="bottom" :class="{active: displayMenu }">
      <div class="container" :class="{ 'container-wide': activeMenu === 0 }">
        <ul class="shows" v-if="activeMenu === 1">
          <li v-for="link in context.header.selectors[activeMenu].links">
            <router-link :to="link.page">{{ link.title }}</router-link>
          </li>
        </ul>
        <ul v-else>
          <li v-for="link in context.header.selectors[activeMenu].links">
            <router-link :to="link.page">{{ link.title }}</router-link>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'Header',
  props: [
    'context'
  ],
  data () {
    return {
      activeMenu: 0,
      displayMenu: false
    }
  },
  methods: {
    setActiveMenu (id) {
      // console.log('setting', id, 'active')
      this.activeMenu = id
      this.displayMenu = true

      // Disable hiding menu delay for now
      let _this = this
      setTimeout(function () {
        _this.displayMenu = false
      }, 15000)
    }
  }
}
</script>
<style scoped>
/*.container {
  width: 925px;
  padding: 0;
}*/
#header {
  background: #1446cb url('../assets/bg2.jpg') no-repeat;
  background-size: cover;
  position: fixed;
  width: 100%;
  z-index: 999;
}

#header .navbar {
  margin-bottom: 0;
}

#header .navbar-default {
  background-color: transparent;
  border-color: transparent;
}

#header .navbar-brand {
  padding: 0;
}

#header .navbar-default .navbar-nav>li>a {
  line-height: 30px;
}

.dropdown-menu {
  padding-top: 0;
}

.open>.dropdown-menu {
  background-color: #1446cb;
}

.dropdown-menu>li>a:focus, .dropdown-menu>li>a:hover,
#header .navbar-default .navbar-nav>li>a:hover {
  background-color: #0a2b84;
}

#header .navbar-default .navbar-nav>.active>a {
  background-color: #0a2b84;
}

#header .navbar-default .navbar-nav a {
  color: white;
}

#header .navbar-default .navbar-nav>.open>a {
  background-color: #0a2b84;
}

.container-fluid>.navbar-collapse, .container-fluid>.navbar-header, .container>.navbar-collapse, .container>.navbar-header {
  position: relative;
  z-index: 9999999;
  margin-right: -30px;
  margin-left: -30px;
}

#header .navbar-default .navbar-toggle,
#header .navbar-default .navbar-collapse, .navbar-default .navbar-form {
  border-color: transparent;
}

.navbar-default .navbar-toggle {
  float: left;
  margin-top: 12px;
}

.navbar-default .navbar-toggle .icon-bar {
  background-color: white;
}

.navbar-default .navbar-toggle:focus, .navbar-default .navbar-toggle:hover {
  background-color: transparent;
}

.logo {
  margin: 16px 20px 16px 0;
}

.glyphicon-menu-hamburger {
  font-size: 20px;
  margin: 20px;
}

.top {
  height: 60px;
}

.bottom {
  clear: both;
  background: rgba(0,0,0,0.5);
  display: none;
}

.bottom.active {
  display: block;
}

.bottom .container-wide {
  width: 1024px;
  position: relative;
  left: -5px;
  height: 66px;
}

.bottom p {
  margin: 0;
  padding: 0;
}

.bottom ul {
  margin: 0;
  padding: 0;
}

.bottom li {
  list-style-type: none;
  display: inline-block;
  margin: 0;
  height: 66px;
}

.bottom li a {
  display: inline-block;
  padding: 20px 52px;
  margin: 0;
  font-size: 18px;
}

.bottom li:hover {
  background: #f22061;
}

li.channel-pro-tv:hover {
  background: #2556fd;
}

li.channel-pro-2:hover {
  background: #f12160;
}

li.channel-pro-x:hover {
  background: #000000;
}

li.channel-pro-gold:hover {
  background: #cba635;
}

li.channel-pro-cinema:hover {
  background: #7d287d;
}

.bottom .shows {
  margin-bottom: 10px;
  margin-left: -20px;
  padding-top: 10px;
}

.bottom .shows li {
  height: 40px;
  padding: 2px 0;
}
.bottom .shows li a {
  display: inline-block;
  width: 230px;
  padding: 5px 15px;
  font-weight: 300;
}

.bottom .shows li:hover {
  background: none;
}

.bottom li a:hover {
  text-decoration: underline;
  font-weight: bold;
}

.search {
  position: initial;
  display: inline-block;
  margin-top: 15px;
  z-index: 1;
}

.search input {
  min-width: 320px;
  height: 28px;
  padding-left: 40px;
  background-image: url('../assets/icons/search.png');
  background-repeat: no-repeat;
  background-position: 15px center;
  color: black;
}

.search input::placeholder {
  font-style: italic;
}

.main-menu {
  background: #092061;
  text-transform: uppercase;
  font-weight: 800;
  font-size: 20px;
}
.main-menu li {
  display: inline-block;
}

.top-right {
  position: absolute;
  top: 0;
  right: 0;
  height: 60px;
}

.drop-down-menus {
  display: inline-block;
  line-height: 60px;
}

.drop-down-menus ul {
  display: inline-block;
  padding: 0;
}

.drop-down-menus ul > li {
  list-style-type: none;
  padding: 0 15px;
}

.drop-down-menus ul > li i {
  font-size: 8px;
}

.drop-down-menus ul ul {
  display: none;
}

.drop-down-menus ul > li {
  font-size: 15px;
}

.drop-down-menus ul > li:hover {
  background: rgba(0,0,0,0.5);
  cursor: pointer;
}

.drop-down-menus ul:hover ul {
  display: inline-block;
}

a {
  color: white;
}

.social {
  display: inline-block;
  margin-right: 15px;
  line-height: 60px;
}

.social a {
  margin: 0 10px;
}

@media (min-width: 768px) {
  .navbar-nav {
    float: right;
    margin-right: 150px;
  }
}

@media (max-width: 969px) {
  .top-right {
    float: none;
  }
}

@media (max-width: 767px) {
  #header .navbar-default .navbar-collapse {
    margin-top: 5px;
    background-color: #1446cb;
  }

  .search {
    position: absolute;
    top: 44px;
    left: 0;
    width: 100%;
    height: 50px;
    padding: 10px 0;
    display: block;
    background-color: #1446cb;
    text-align: center;
  }
}
</style>
