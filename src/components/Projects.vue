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
    <section class="py-16 bg-gray-900" id="project">
        <div class="container mx-auto px-4 max-w-7xl lg:mb-50">
            <div class="text-center mb-10">
                <h2 class="text-4xl md:text-5xl font-extrabold text-white">
                Projects.
                </h2>
                <div class="w-28 h-1 bg-primary mx-auto mt-2 rounded-2xl"></div>
            </div>  

        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-5">
            <div v-for="project in projects" :key="project.id"
                class="bg-gray-800 rounded-lg overflow-hidden shadow-sm
                hover:shadow-lg hover:scale-105 transition-all duration-300">
                <img :src="project.image" :alt="project.title"
                    class="w-full h-44 object-cover hover:opacity-90 transition-opacity duration-300">
                <div class="p-4">
                    <h3 class="text-lg font-semibold text-white group-hover:primary transition-colors">
                    {{ project.title }}
                    </h3>
                    <p class="text-gray-400 text-sm mt-1">
                    {{ project.desc }}
                    </p>

                    <div class="flex flex-wrap justify-between gap-1.5 mt-3 items-center">
                        <div class="flex gap-2">
                            <!-- <span v-for="(stack, idx) in project.stack" :key="idx"
                                class="text-xs px-2 py-0.5 bg-gray-700 text-gray-300 rounded
                                    hover:bg-primary hover:text-white transition-colors duration-300 ">
                            {{ stack }}
                            </span>  -->
                            <span v-for="(stack, idx) in project.stack" :key="idx"
                                    :class="`text-xs px-2 py-0.5 rounded hover:opacity-90 cursor-pointer transition-colors duration-300 ${getColor(stack)}`">
                                {{ stack }}
                            </span>
                        </div>
                        <a :href="project.repo" target="_blank"
                            class="text-xs px-3 py-1 bg-gray-700 text-gray-300 rounded
                                    hover:bg-primary hover:text-white transition-colors duration-300 text-primary">
                            GitHub
                        </a>
                    </div>
                </div>
            </div>
      </div>
    </div>
  </section>
</template>

