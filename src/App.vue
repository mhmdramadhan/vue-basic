<template>
  <div id="app">
    <router-view/>
    <Footer/>
  </div>
</template>
<script>
// untuk import file
import Footer from "@/components/Footer.vue";

export default {
 name:"App",
  components: {
    Footer,
  },
}
</script>

