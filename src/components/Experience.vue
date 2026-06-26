<script setup>
    import { Briefcase } from 'lucide-vue-next';
    import { Building2 } from 'lucide-vue-next';
    import { Calendar } from 'lucide-vue-next';
    import sql from '../assets/sql-file.png'
    import html from '../assets/html.png'
    import css from '../assets/css-3.png'
    import js from '../assets/js.png'
    import vue from '../assets/vue.png'
    import laravel from '../assets/Laravel.png'
    import tailwind from '../assets/Tailwind_CSS.png'
    import php from '../assets/php.png'

    const skills = [
        {
            id: 1,
            name: "SQL",
            width: "70%",
            image : sql
        },
        {
            id: 2,
            name: "HTML",
            width: "75%",
            image : html
        },
        {
            id: 3,
            name: "CSS",
            width: "75%",
            image : css
        },
        {
            id: 4,
            name: "JavaScript",
            width: "75%",
            image : js
        },
        {
            id: 5,
            name: "Vue Js",
            width: "70%",
            image : vue
        },
        {
            id: 6,
            name: "Laravel",
            width: "65%",
            image : laravel
        },
        {
            id: 7,
            name: "Tailwind",
            width: "65%",
            image : tailwind
        },
        {
            id: 8,
            name: "PHP",
            width: "65%",
            image : php
        },
    ]

    const experiences = [
        {
            id: 1,
            role: "Software Developer",
            company: "HRD Singapore Pte., Ltd.",
            date: "August 2022 - Present"
        }
    ]
</script>


<template>
    <section class="text-white py-20 relative overflow-hidden bg-slate-700"
    id="skills">
        <div class="max-w-7xl mx-auto px-6 lg:px-16 relative z-10">
            <div class="grid md:grid-cols-2 gap-16 items-start">
                <div data-aos="fade-right">
                    <h2 class="text-4xl md:text-5xl font 
                    font-extrabold mb-12">Tech 
                    <span class="text-primary">Stack</span>
                    </h2>
                    <div class="space-y-8">
                        <div v-for="skill in skills" :key="skill.id"
                        class="group">
                            <div class="flex items-center justify-between mb-2"> 
                                <div class="flex items-center gap-3" >
                                    <div class="p-2 bg-slate-700 rounded-lg 
                                        group-hover:bg-primary transition-colors
                                        duration-300">
                                        <!-- <component :is="skill.icons"
                                        :size="20" class="text-primary
                                        group-hover:text-white" /> -->
                                        <img :src="skill.image" :alt="skill.name" 
                                        class="w-7 h-7 text-primary 
                                        group-hover:text-white">
                                    </div>  
                                    <span class="font-medium tracking-wide">
                                        {{ skill.name }}
                                    </span>
                                </div>
                                <span class="text-primary font-bold">
                                    {{ skill.width }}
                                </span>
                            </div>
                            <div class="h-2 w-full bg-[#131d30] rounded-full
                            p-0.5">
                                <div class="h-full rounded-full bg-linear-to-r
                                from-primary to-green-400 shadow-[0_0_10px_#06a2c2]"
                                :style="{width: skill.width}">
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div data-aos="fade-left">
                    <h2 class="text-4xl md:text-5xl font-extrabold mb-12">
                        Work <span class="text-primary">Experience</span>
                    </h2>
                    <div class="space-y-6">
                        <div v-for="exp in experiences" :key="exp.id"
                        class="group relative p-6 rounded-2xl bg-[#111a3e]
                        border border-[#1f1641] hover:border-primary/50 
                        transition-all duration-300">
                            <div class="flex gap-4">
                                <div class="shrink-0 mt-1">
                                    <div class="p-3 bg-[#050816] rounded-xl 
                                    border bordr-gray-800 group-hover:border-primary
                                    transition-colors">
                                        <Briefcase class="text-priamry" :size="24"/>
                                    </div>
                                </div>
                                <div class="grow">
                                    <h3 class="text-xl font-bold text-white 
                                    group-hover:text-primary transition-colors">
                                        {{ exp.role }}
                                    </h3>
                                    <div class="flex flex-col sm:flex-row sm:items-center
                                    gap-2 sm:gap-4 text-sm text-gray-400">
                                    <span class="flex items-center gap-1.5">
                                        <Building2 :size="14" class="text-primary" />
                                        {{ exp.company }}
                                    </span>
                                    <span class="flex items-center gap-1.5">
                                        <Calendar :size="14" class="text-primary" />
                                        {{ exp.date }}
                                    </span>
                                    </div>
                                </div>
                            </div>

                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>
