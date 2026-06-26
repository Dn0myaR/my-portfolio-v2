<script setup>
import { Download } from 'lucide-vue-next';
import mypic from '../assets/mypics2.png';
import { ref, onMounted, onUnmounted } from 'vue'; 
import resumePdf from '@/assets/RaymondCV.pdf';
import sql from '../assets/sql-file.png'
import html from '../assets/html.png'
import css from '../assets/css-3.png'
import js from '../assets/js.png'
import vue from '../assets/vue.png'
import laravel from '../assets/Laravel.png'
import tailwind from '../assets/Tailwind_CSS.png'
import php from '../assets/php.png'

// --- EFFECT na nag tatype ---
const typedText = ref('');
const textToType = "Raymond";
let charIndex = 0;
let isDeleting = false; 

function type() {
    const currentText = textToType;
    
    if (!isDeleting) {
        typedText.value = currentText.substring(0, charIndex + 1);
        charIndex++;

        if (charIndex === currentText.length) {
            setTimeout(() => {
                isDeleting = true;
                type();
            }, 1500);
            return;
        }
        setTimeout(type, 150);
    } else {
        typedText.value = currentText.substring(0, charIndex - 1);
        charIndex--;

        if (charIndex === 0) {
            isDeleting = false; 
            setTimeout(type, 500);
            return;
        }
        setTimeout(type, 75);
    }
}

// --- magnet button effect---
const isHoveringBtn = ref(false); 
const mousePos = { x: null, y: null }; 

const updateMouse = (e) => {
    mousePos.x = e.clientX;
    mousePos.y = e.clientY;
};

const canvasRef = ref(null);
let animationFrameId;

const initParticles = () => {
    const canvas = canvasRef.value;
    if (!canvas) return;
  
    const ctx = canvas.getContext('2d');
  
    const setSize = () => {
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
    };
    setSize();
    window.addEventListener('resize', setSize);
    window.addEventListener('mousemove', updateMouse); // Subaybayan ang mouse moves globally

    const logoUrls = [sql, html,  css, js, vue, laravel, tailwind, php];
    
    const loadedLogos = [];
    logoUrls.forEach(url => {
        const img = new Image();
        img.src = url;
        loadedLogos.push(img);
    });

    const particlesArray = [];
    const numberOfParticles = 30; 

    class Particle {
        constructor() {
            this.x = Math.random() * canvas.width;
            this.y = Math.random() * canvas.height;
            this.vx = (Math.random() - 0.5) * 1.5; 
            this.vy = (Math.random() - 0.5) * 1.5; 
            this.size = Math.random() * 10 + 15; 
            this.logo = loadedLogos[Math.floor(Math.random() * loadedLogos.length)];
        }
        update() {
            const dxMouse = mousePos.x - this.x;
            const dyMouse = mousePos.y - this.y;
            const distanceToMouse = Math.sqrt(dxMouse * dxMouse + dyMouse * dyMouse);
            const isHoveringLogo = distanceToMouse < this.size;

            if (isHoveringLogo) {
                // --- CONTROL EFFECT ---
                // Hahabulin ng logo ang cursor mo nang "smooth"
                this.x += dxMouse * 0.1; 
                this.y += dyMouse * 0.1;
            } else if (isHoveringBtn.value && mousePos.x !== null) {
                // --- MAGNETIC BUTTON EFFECT ---
                const dx = mousePos.x - this.x;
                const dy = mousePos.y - this.y;
                const distance = Math.sqrt(dx * dx + dy * dy);
                if (distance < 300) {
                    this.x += dx * 0.03;
                    this.y += dy * 0.03;
                } else {
                    this.x += this.vx;
                    this.y += this.vy;
                }
            } else {
                // --- NORMAL MOVEMENT ---
                this.x += this.vx;
                this.y += this.vy;
            }

            // Bounce logic
            if (this.x < 0 || this.x > canvas.width) this.vx = -this.vx;
            if (this.y < 0 || this.y > canvas.height) this.vy = -this.vy;
        }
        // update() {
        //     //   Mouse Hover check
        //     const dxMouse = mousePos.x - this.x;
        //     const dyMouse = mousePos.y - this.y;
        //     const distanceToMouse = Math.sqrt(dxMouse * dxMouse + dyMouse * dyMouse);
        
        //     // Check kung tinapatan ang logo (kung ang distansya ay mas maliit sa size ng logo)
        //     const isHoveringLogo = distanceToMouse < this.size;

        //     if (isHoveringLogo) {
        //         // PAUSE movement pag naka-hover
        //         // (Walang gagawin sa x at y, kaya titigil siya)
        //     } else if (isHoveringBtn.value && mousePos.x !== null) {
        //         // MAGNETIC EFFECT (kung hindi naka-hover sa logo pero naka-hover sa button)
        //         const dx = mousePos.x - this.x;
        //         const dy = mousePos.y - this.y;
        //         const distance = Math.sqrt(dx * dx + dy * dy);
        //         if (distance < 300) {
        //             this.x += dx * 0.03;
        //             this.y += dy * 0.03;
        //         } else {
        //             this.x += this.vx;
        //             this.y += this.vy;
        //         }
        //     } else {
        //         this.x += this.vx;
        //         this.y += this.vy;
        //     }
        
        //     // Bounce logic sa pader
        //     if (this.x < 0 || this.x > canvas.width) this.vx = -this.vx;
        //     if (this.y < 0 || this.y > canvas.height) this.vy = -this.vy;
        // }

        draw() {
            if (this.logo.complete) {
                // CHECK HOVER para sa visual effect
                const dx = mousePos.x - this.x;
                const dy = mousePos.y - this.y;
                const isHovering = Math.sqrt(dx * dx + dy * dy) < this.size;

                if (isHovering) {
                    // GLOW EFFECT (Shadow)
                    ctx.shadowBlur = 20;
                    ctx.shadowColor = '#41e2ee'; // Primary color
                    // Enlarge logo (scaling)
                    ctx.drawImage(this.logo, this.x - (this.size * 1.5) / 2, this.y - (this.size * 1.5) / 2, this.size * 1.5, this.size * 1.5);
                    ctx.shadowBlur = 0; // Reset
                } else {
                    ctx.drawImage(this.logo, this.x - this.size / 2, this.y - this.size / 2, this.size, this.size);
                }
            }
        }
    }

    for (let i = 0; i < numberOfParticles; i++) {
        particlesArray.push(new Particle());
    }

    const animate = () => {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        
        for (let i = 0; i < particlesArray.length; i++) {
            particlesArray[i].update();
            particlesArray[i].draw();

            for (let j = i; j < particlesArray.length; j++) {
                const dx = particlesArray[i].x - particlesArray[j].x;
                const dy = particlesArray[i].y - particlesArray[j].y;
                const distance = Math.sqrt(dx * dx + dy * dy);

                if (distance < 150) { 
                ctx.beginPath();
                const opacity = 1 - (distance / 150);
                ctx.strokeStyle = `rgba(65, 226, 238, ${opacity * 0.3})`;
                ctx.lineWidth = 2;
                ctx.moveTo(particlesArray[i].x, particlesArray[i].y);
                ctx.lineTo(particlesArray[j].x, particlesArray[j].y);
                ctx.stroke();
                }
            }
        }
        animationFrameId = requestAnimationFrame(animate);
    };
    animate();

    return () => {
        window.removeEventListener('resize', setSize);
        window.removeEventListener('mousemove', updateMouse);
        cancelAnimationFrame(animationFrameId);
    };
};

onMounted(() => {
    type(); 
    const cleanupParticles = initParticles(); 
  
    onUnmounted(() => {
        if (cleanupParticles) cleanupParticles();
    });
});

</script>       

<template>
    <section id="about" class="bg-slate-600 relative w-full h-screen md:pt-0 lg:pt-28 overflow-hidden" data-aos="zoom-in-up ">
        <div class="absolute top-0 inset-x-0 h-64 flex items-start">
            <div class="h-24 w-2/3 bg-linear-to-br from-[#6ce2ebbe] blur-2xl invisible opacity-40">
            </div>
            <div class="h-20 w-3/4 bg-linear-to-r from-[#6ce2ebbe] opacity-40 blur-2xl"> 
            </div>
        </div>
           
        <canvas ref="canvasRef" class="absolute inset-0 z-0 pointer-events-none"></canvas>

        <div class="w-full px-5 sm:px-8 md:px-12 lg:px-8 max-w-5xl 
            lg:max-w-7xl mx-auto lg:mb-40 relative z-10">
            <div class="grid lg:grid-cols-2 gap-10 xl:gap-14 relative pt-24
            lg:max-w-none max-w-2xl md:max-w-3xl mx-auto">
                <div class="lg:py-6">
                    <div class="text-center lg:next-left">
                        <h1 class="text-4xl pt-4 font-bold text-white md:text-5xl lg:text-6xl">
                            Hi, I'm <span class="bg-linear-to-r from-primary 
                            to-cyan-200 bg-clip-text text-transparent">{{ typedText }}</span>
                        <span class="cursor inline-block w-0.75 h-9 bg-white ml-1 align-middle animate-pulse"></span>
                        <span class="inline-block animate-wave origin-[70%_70%]">👋</span>
                        </h1>
                    </div>
                    <p class="text-gray-200 pt-8 text-center lg:text-left
                    mx-auto max-w-xl">
                        a full‑stack web developer with experience in   
                        Laravel, Vue, JavaScript, HTML, and CSS. 
                        In my first company role, I applied these 
                        technologies to build systems that supported 
                        daily operations — from monitoring installed 
                        software on company laptops and CPUs to 
                        streamlining office supply requests and 
                        replenishment, as well as tracking incoming 
                        and outgoing materials. I enjoy learning and 
                        applying modern frameworks to create solutions
                        that make work more efficient.
                    </p>   
                    <div class="flex items-center gap-3 pt-9 flex-col 
                        sm:flex-row sm:w-max sm:mx-auto lg:mx-0">
                        
                        <button 
                            @mouseenter="isHoveringBtn = true"
                            @mouseleave="isHoveringBtn = false"
                            class="border border-primary px-6 md:px-7 py-3 
                            rounded-full relative group w-full sm:w-max
                            flex justify-center bg-gray-900/50 backdrop-blur-sm cursor-pointer"
                        > 
                            <div class="hover:scale-105 transition-all
                            ease-in-out flex justify-center relative">
                                <div class="scg-container">
                                    <Download :size="18" class="text-primary animate-bounce"/>
                                    <div class="download-loader text-white hidden"/>
                                </div>
                                <a :href="resumePdf" 
                                    download="RaymondCV.pdf"
                                    class="pl-2 text-primary ">Download Resume
                                </a>
                            </div>
                        </button>
                    </div>
                </div>
                <div class="lg:h-full md:flex">
                    <div class="flex w-full h-96 min-h-96 lg:min-h-[none]
                    lg:w-full lg:h-full items-center relative">
                        <div class="absolute z-0 top-1/2 -translate-y-1/2
                        w-5/6 right-0 h-[calc(80%+20px)] bg-linear-to-tr
                        opacity-25 from-[#41e2eebe] to-primary blur-2xl">
                        </div>
                        <div class="absolute h-full z-10 p-2 -translate-y-1/2 
                            top-1/2 lg:right-3 md:right-40 sm:right-16">
                            <img :src="mypic" alt="Me"
                            width="500"
                            height="auto"
                            loading="lazy"
                            class="w-full h-full rounded-[30%_70%_70%_30%/30%_30%_70%_70%]
                            object-cover"
                            >
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>