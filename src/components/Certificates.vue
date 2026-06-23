<script setup>
    import { Award, ExternalLink } from 'lucide-vue-next';
    import { ShieldCheck } from 'lucide-vue-next';

   
    const certifications = [ 
        {  
            id: 1,
            title : "",
            issuer: "",
            date: "",
            link: "",
            desc: ""
        },
            {  
            id: 2,
            title : "",
            issuer: "",
            date: "",
            link: "",
            desc: ""
        },
        {  
            id: 3,
            title : "",
            issuer: "",
            date: "",
            link: "",
            desc: ""
        },
           
    ]
</script>

<template>
    <section class="text-white py-20 lg:mt-40 sm:mt-0" id="certificates">
        <div class="max-w-7xl px-6 lg:px-16">
            <div class="mb-16">
                <p class="text-primary text-sm uppercase mb-2
                tracking-widest font-semibold">
                    Achievements
                </p>
                <h2 class="text-4xl md:text-5xl font-extrabold">
                    Certifications.
                </h2>
            </div>
            <div class="grid grid-cols-1 md:grid-cols-2 
            lg:grid-cols-3 gap-6">
            <div v-for="cert in certifications" :key="cert.id"
            data-aos="zoom-in"
            class="group relative bg-[#111a3e] border 
            border-[#1f1641] p-6 rounded-2xl transition-all 
            duration-300 hover:border-primary/50
            hover:shadow-[0_0_20px_-5x_rgba(6, 162, 194, 0.2)]">
            <div class="absolute -top-4 -right-4 bg-primary
            p-3 rounded-xl shadow-lg transform group-hover:rotate-12 
            transition-transform">
                <Award class="text-white :size=24"/>
            </div>
            <div class="flex items-center gap-4 mb-4 text-shadow-xs
            text-gray-400">
                <span class="flex items-center gap-1">
                    <ShieldCheck :size="14" class="text-primary" />
                    {{ cert.issuer }}
                </span>
            </div>
            <h3 class="text-xl font-bold mb-3 group-hover:text-primary
            transition-colors">
                {{ cert.title }}
            </h3>
            <p class="text-gray-400 text-sm mb-6 line-clamp-2">
                {{ cert.desc }}
            </p>
            <a :href="cert.link"
            target="_blank"
            rel="noopener noreferrer"
            class="inline-flex items-center gap-2 text-sm
            font-medium text-primary hover:text-white transition-colors 
            border-b border-transparent hover:border-white pb-1"
            >
                View Certificate <ExternalLink :size="14"/>
            </a>
            </div>
            </div>
        </div>
    </section>
</template>
