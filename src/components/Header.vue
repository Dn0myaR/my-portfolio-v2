<script setup>
import { ref } from 'vue';
import { Menu } from 'lucide-vue-next';
import { X } from 'lucide-vue-next';
import { onMounted, onUnmounted } from 'vue'

const isScrolled = ref(false)

const handleScroll = () => {
  isScrolled.value = window.scrollY > 0 // kahit konting galaw
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})

const isMenuOpen = ref(false)

const menuItems = [
    {name: 'About', href: '#about'},
    {name: 'Skills', href: '#skills'},
    {name: 'Project', href: '#project'},
    // {name: 'Certification', href: '#certificates'},
]

const scrollToSection = (href) => {
    isMenuOpen.value = false
    const element = document.querySelector(href)
    if(element){
        element.scrollIntoView({ behavior: 'smooth'})
    }
}
</script>

<template>
    <!-- <header class="fixed top-0 left-0 w-full z-50 px-6 py-7 transition-colors
     duration-300 bg-transparent" id="mainHeader"> -->
     <header 
        :class="[
            'fixed top-0 left-0 w-full z-50 px-1 py-1 transition-colors duration-300',
            isScrolled ? 'bg-[#031744]' : 'bg-transparent'
        ]">
        <div class="max-w-7xl mx-auto flex justify-between items-center" >
            <div class="text-white text-3xl font-black cursor-pointer">
                <!-- PORTFOLIO<span class="text-primary">.</span> -->
            </div>
            <!-- navigation -->
            <nav class="hidden md:flex items-center mt-5 gap-10">
                <ul class="flex gap-8"> 
                    <li v-for="item in menuItems" :key="item.name">
                        <button
                        @click="scrollToSection(item.href)"
                        class="text-gray-300 hover:text-white
                        text-base font-medium transition-colors">
                            {{ item.name }}
                        </button>
                    </li>
                </ul>
                <button @click="scrollToSection('#contact')"
                class="bg-primary hover:bg-primary/90 text-white
                 px-6 py-2.5 rounded-lg text-base font-semibold transition-all"
                >Contact Me</button>
            </nav>
            <!-- Menu Button -->
            <button class="md:hidden text-white"
            @click="isMenuOpen= !isMenuOpen">
            <Menu v-if="!isMenuOpen" :size="32"/>
            <X v-else :size="32"/>
            </button>
        </div>
        <div v-if="isMenuOpen"
        class="fixed inset-0 bg-black/60 backdrop-blur-sm md:hidden"
        @click="isMenuOpen = false">
        </div>
        <div class="fixed top-0 right-0 h-full w-80 bg-[#112723] p-4
        z-50 transform transition-transform duration-300 md:hidden"
        :class="isMenuOpen ? 'translate-x-0' : 'translate-x-full'">
        <button class="self-end text-white mb-10"
        @click="isMenuOpen=false">
            <X :size="32"/>
        </button>
        <ul class="flex flex-col gap-8">
            <li v-for="item in menuItems" :key="item.name">
                <button @click="scrollToSection(item.href)"
                class=text-white text-xl font-semibold hover:text-primary
                transition-colors>
                    {{ item.name }}
                </button>
            </li>
            <li class="pt-6">
                <button @click="scrollToSection('#section')"
                class="w-full bg-primary text-white py-4
                rounded-xl text-lg font-bold">
                   Contact Me
                </button>

            </li>
        </ul>
        </div>
    </header>
</template>
