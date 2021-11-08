<template>
  <v-app>
    <Navbar/>
    <v-content class="ma-4">
      <router-view> </router-view>
    </v-content>
    <Footer/>

  </v-app>
</template>

<script>
import Navbar from '@/components/Navbar' // Navbar 폴더에 있는것으로부터 Navbar 를 불러온다. component 에 있는 파일 다 불러옴.
import Footer from '@/components/Footer'
export default {
  name: 'App',
  components: {
    Navbar,
    Footer
  }

}
</script>
