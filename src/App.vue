<template>
  <div>
    <span class="wrapper">
      <nav-bar>
        <li class="side-nav-title side-nav-item">Menu</li>
        <menu-link goto="/" title="Início" icon="home" />
        <menu-link goto="/boards" title="Quadros" icon="developer-board" />
      </nav-bar>

      <main class="content-page">
        <div class="content">
          <header-vue/>
          <div class="container-fluid">
            <router-view></router-view>
          </div>
        </div>
      </main>
    </span>

    <right-bar></right-bar>
  </div>
</template>

<script>
import NavBar from '@/components/layouts/NavBar'
import RightBar from '@/components/layouts/RightBar'
import HeaderVue from '@/components/layouts/HeaderVue'
import MenuLink from '@/components/layouts/MenuLink'

export default {
  name: 'app',
  components: {
    NavBar,
    RightBar,
    HeaderVue,
    MenuLink,
  },
}

String.prototype.URLToAnchors = function() {
  // var regexp = /(?:www\.|(?!www))[^\s\.]+\.[^\s]{2,}|www\.[^\s]+\.[^\s]{2,}/gi
  // var matches_array = this.match(regexp)
  // for (var i = 0; i < matches_array.length; i++){
  //     $("#result").append('<a href="http://'+matches_array[i]+'" title="'+matches_array[i]+'">'+matches_array[i]+'</a>')
  // }
  // return this.replace(/((?:http(s)?:\/\/)?(?:www(\d)?\.)?([\w\-]+\.\w{2,})\/?((?:\?(?:[\w\-]+(?:=[\w\-]+)?)?(?:&[\w\-]+(?:=[\w\-]+)?)?))?(#(?:[^\s]+)?)?)/gi, '<a href="http$2://www$3.$4$5/$6">$1</a>')
  return this.replace(/((\[([^)]+)\])?(\(([^)]+)\)))|(?:http(s)?:\/\/)?(?:www(\d)?\.)?([\w\-]+\.\w{2,})\/?(?:\/(?:[\w\-]+(?:=[\w\-]+)?)?)+/gi, `<a href="$5" target="_blank">$3</a>`)
}
</script>
