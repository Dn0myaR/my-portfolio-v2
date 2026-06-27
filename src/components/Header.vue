<script setup>
import { ref } from 'vue';
import { Menu } from 'lucide-vue-next';
import { X } from 'lucide-vue-next';
import { onMounted, onUnmounted } from 'vue'

const isScrolled = ref(false);
let scrollTimeout = null;

const handleScroll = () => {
    // 1. Kapag ginalaw ang page, automatic na magkakaroon ng background
    isScrolled.value = window.scrollY > 0

    // 2. Burahin ang naunang timer para hindi mag-flicker habang tuloy-tuloy ang scroll
    if (scrollTimeout) {
        clearTimeout(scrollTimeout)
    }

    // 3. Mag-antay ng 1.5 seconds (1500ms) pagkatapos tumigil mag-scroll bago alisin ang bg
    scrollTimeout = setTimeout(() => {
        isScrolled.value = false
    }, 1500) // Pwede mong palitan ang 1500 kung gusto mo mas mabilis o mas mabagal mawala
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
  if (scrollTimeout) clearTimeout(scrollTimeout) // Linisin ang timer pagka-unmount
})

const isMenuOpen = ref(false)

const menuItems = [
    {name: 'About', href: '#about'},
    {name: 'Skills', href: '#skills'},
    {name: 'Project', href: '#project'},
    // {name: 'Certification', href: '#certificates'}, //tempo comment
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
     <header 
        :class="[
            'fixed top-0 left-0 w-full z-50 px-1 py-1 transition-colors duration-300',
            isScrolled ? 'bg-[#1a2b3d] opacity-80' : 'bg-transparent'
        ]">
        <div class="max-w-7xl mx-auto flex justify-between items-center" >
            <div class="text-white text-3xl font-black cursor-pointer">
                <!-- can input message -->
            </div>
            <!-- navigation -->
            <nav class="hidden md:flex items-center mt-5 gap-10">
                <ul class="flex gap-8"> 
                    <li v-for="item in menuItems" :key="item.name">
                        <button
                        @click="scrollToSection(item.href)"
                        class="text-white hover:border-primary/80 
                        hover:shadow-[0_0_20px_rgba(15,225,240,0.3)]
                        transition-all duration-300 cursor-pointer hover:scale-105
                        text-base font-medium rounded-2xl hover:text-primary">
                            {{ item.name }}
                        </button>
                    </li>
                </ul>
                <button @click="scrollToSection('#contact')"
                class="bg-primary hover:bg-primary/90 text-white duration-300 ease-in-out hover:scale-105
                 px-6 py-2.5 rounded-lg text-base font-semibold transition-all "
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
        class="fixed inset-0 bg-white/60 backdrop-blur-sm md:hidden"
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
                class="text-white text-xl font-semibold hover:text-primary
                transition-colors hover:border-primary/80 hover:shadow-[0_0_20px_rgba(15,225,240,0.3)]
                duration-300 cursor-pointer hover:scale-105 rounded-2xl">
                    {{ item.name }}
                </button>
            </li>
            <li class="pt-6">
                <button @click="scrollToSection('#section')"
                class="w-full bg-primary text-white py-4
                rounded-xl text-lg font-bold transition-all duration-300 ease-in-out hover:scale-105">
                   Contact Me
                </button>
            </li>
        </ul>
        </div>
    </header>
</template>
