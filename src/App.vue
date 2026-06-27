<script setup>
  import Header from './components/Header.vue'
  import AOS from 'aos';
  import 'aos/dist/aos.css'
  import { onMounted } from 'vue';
  import MySelfSection from './components/MySelfSection.vue';
  // temporary comment
  // import Certificates from './components/Certificates.vue';
  import Experience from './components/Experience.vue';
  import Projects from './components/Projects.vue';
  import Contact from './components/Contact.vue';
  // import Footer from './components/Footer.vue';

  onMounted(() => {
    AOS.init({
      duration: 1000,
      once:false,
      offset:100
    })
  })

</script>

<template>
  <div class="bg-[#111827] min-h-screen">
    <Header />
    <MySelfSection />
    <Experience />  
    <!-- temporary comment -->
    <!-- <Certificates /> --> 
    <Projects />
    <Contact />
    <!-- <Footer /> -->
  
  </div>
</template>

