<script setup>
    import proj1 from '../assets/pcm.jpg'
    import proj2 from '../assets/gp.jpg'
    import proj3 from '../assets/osi.png'

    const projects = [
        {
            id: 1,
            image: proj1,
            title: 'PC Management',
            desc: 'Monitoring installed Software',
            stack: ['Vue JS', 'Laravel', 'MS SQL'],
            repo: 'https://github.com/Dn0myaR/my-portfolio'
            
        },
            {
            id: 2,
            image: proj2,
            title: 'Material Gatepass',
            desc: 'tracking Incoming/Outcoming of Materials',
            stack: ['Vue JS', 'Laravel', 'MS SQL'],
            repo: 'https://github.com/Dn0myaR/my-portfolio'
        },
            {
            id: 3,
            image: proj3,
            title: 'Office Supplies Inventory',
            desc: 'automated cost tracking, and monthly usage analytics to streamline supply management',
            stack: ['Vue JS', 'Laravel', 'MS SQL'],
            repo: 'https://github.com/Dn0myaR/my-portfolio'
        }
    ]

    const stackColor = [
        { language: 'Vue JS', color: 'bg-green-600 text-white' },
        { language: 'JavaScript', color: 'bg-yellow-500 text-black' },
        { language: 'Laravel', color: 'bg-red-600 text-white' },
        { language: 'MS SQL', color: 'bg-blue-600 text-white' },
        { language: 'HTML', color: 'bg-orange-500 text-white' },
        { language: 'Tailwind', color: 'bg-cyan-500 text-white' },
        { language: 'PHP', color: 'bg-indigo-400 text-white' },
        { language: 'CSS', color: 'bg-blue-400 text-white' }
    ]

    const getColor = (stack) => {
        const found = stackColor.find(s => stack.includes(s.language))
        return found ? found.color : 'bg-gray-700 text-gray-300'
    }


</script>

<template>
    <!-- 1. MAIN SECTION: Ginawang light background (bg-slate-50) na may gumagalaw na grid lines -->
    <section class="relative py-16 bg-slate-400 overflow-hidden 
                    bg-[linear-gradient(to_right,#e2e8f0_1px,transparent_1px),linear-gradient(to_bottom,#e2e8f0_1px,transparent_1px)] 
                    bg-size-[4rem_4rem] animate-grid-move" id="project">
        
        <!-- TECH AMBIENT GLOWS (Mga kumikinang na background elements) -->
        <div class="absolute inset-0 z-0 pointer-events-none overflow-hidden">
            <!-- Unang Core Glow (Top Right) -->
            <div class="absolute top-1/4 -right-20 w-96 h-96 bg-primary/25 rounded-full blur-3xl animate-pulse-slow"></div>
            <!-- Ikalawang Core Glow (Bottom Left - Delayed) -->
            <div class="absolute bottom-1/4 -left-20 w-120 h-120 bg-blue-400/20 rounded-full blur-3xl animate-pulse-slow [animation-delay:2s]"></div>
        </div>

        <!-- MAIN CONTENT (z-10 para lumutang nang maayos sa grid) -->
        <div class="container mx-auto px-4 max-w-7xl lg:mb-50 relative z-10">
            <div class="text-center mb-10">
                <!-- Inayos ang text color sa gray-800 para malinaw sa puting background -->
                <h2 class="text-4xl md:text-5xl font-extrabold text-gray-800">
                    Projects.
                </h2>
                <div class="w-28 h-1 bg-primary mx-auto mt-2 rounded-2xl"></div>
            </div>  

            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-5">
                <!-- PROJECT CARDS -->
                <div v-for="project in projects" :key="project.id"
                    class="bg-gray-800/60 rounded-lg overflow-hidden shadow-md hover:shadow-2xl hover:scale-105 transition-all duration-300">
                    <img :src="project.image" :alt="project.title"
                        class="w-full h-44 object-cover hover:opacity-90 transition-opacity duration-300">
                    <div class="p-4">
                        <h3 class="text-lg font-semibold text-primary">
                            {{ project.title }}
                        </h3>
                        <p class="text-white text-sm mt-1">
                            {{ project.desc }}
                        </p>

                        <div class="flex flex-wrap justify-between gap-1.5 mt-3 items-center">
                            <div class="flex gap-2">
                                <span v-for="(stack, idx) in project.stack" :key="idx"
                                        :class="`text-xs px-2 py-0.5 rounded hover:opacity-90 cursor-pointer transition-colors duration-300 ${getColor(stack)}`">
                                    {{ stack }}
                                </span>
                            </div>
                            <a :href="project.repo" target="_blank"
                                class="text-xs px-3 py-1 bg-gray-700 text-gray-300 rounded hover:bg-primary hover:text-white transition-colors duration-300">
                                GitHub
                            </a>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

