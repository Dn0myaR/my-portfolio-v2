<script setup>
import { reactive, ref } from 'vue';
import emailjs from 'emailjs-com';
import emails from '../assets/gmail.png';
import linkedin from '../assets/linkedin.png';
import github from '../assets/github.png';
import bgvideo from '../assets/contactbg.mp4'
    const contactInfo = [
        { 
            id: 1,
            image: emails,
            title: "Email",
            value: "cer.rhei@gmail.com",
            link: "https://mail.google.com/mail/?view=cm&fs=1&to=cer.rhei@gmail.com"
        },
        { 
            id: 2,
            image: linkedin,
            title: "LinkedIN",
            value: "www.linkedin.com/in/raymondsereno",
            link: "https://www.linkedin.com/in/raymondsereno"
        },
        {
            id: 3,
            image: github,
            title: "GitHub",
            value: "github.com/Dn0myaR",
            link: "https://github.com/Dn0myaR"
        }
    ]

    const formData = reactive({
        name: '',
        email: '',
        subject: '',
        message: ''
    })

    const isSubmitting = ref(false)
    const handleSubmit = async () => {
        isSubmitting.value = true
        try {
            await emailjs.send(
            'service_qwf78a4',      
            'template_kynjmbl',
            {   name: formData.name,
                from_email: formData.email,
                subject: formData.subject,
                message: formData.message
            },
            'IzAY2DUjGGn7SHua3'       
            )
            alert('Message sent successfully!')
            formData.subject = ''
            formData.message = ''
        } catch (error) {
            alert('Failed to send message. Please try again')
        } finally {
            isSubmitting.value = false
        }
    }
</script>
<template>
    <!-- INAYOS: Pinalitan ang h-screen ng min-h-screen, at dinagdagan ng flex flex-col justify-between -->
    <section class="relative py-20 overflow-hidden md:min-h-screen flex flex-col justify-between bg-slate-400" id="contact">
        <video 
            autoplay 
            loop 
            muted 
            playsinline 
            class="absolute top-0 left-0 w-full h-full object-cover z-0">
            <source :src="bgvideo" type="video/mp4" />
        </video>
        
        <!-- Overlay Layer (I-uncomment mo ito kung gusto mong medyo madilim ang video background mo) -->
        <!-- <div class="absolute top-0 left-0 w-full h-full bg-slate-900/85 backdrop-blur-[2px] z-10"></div> -->
        
        <!-- INAYOS: Dinagdagan ng class na "grow w-full" para kainin nito ang space sa itaas at itulak ang footer pababa -->
        <div class="container mx-auto px-4 max-w-6xl relative z-20 grow w-full ">
            <div class="text-center mb-12">
                <h2 class="text-3xl md:text-5xl font-extrabold text-blue-400 mb-2">
                    Connect with me
                </h2>
                <div class="w-28 h-1 bg-primary mx-auto mt-2 rounded-2xl"></div>
            </div>
            
            <div class="grid md:grid-cols-2 gap-8 ">
                <div>
                    <p class="text-gray-400 mb-8 leading-relaxed">
                        <!-- Let’s chat. Drop a message! -->
                    </p>
                    <div class="space-y-6">
                        <div v-for="info in contactInfo" :key="info.id"
                        class="flex items-center gap-4 group">
                            <div class="w-10 h-10 rounded-full flex items-center justify-center group-hover:bg-primary/20 transition-colors">
                                <img :src="info.image" :alt="info.title"
                                    class="w-7 h-7 text-primary group-hover:rotate-12 transition-transform duration-300 ease-in-out hover:scale-105 cursor-pointer">
                            </div>
                            <div>
                                <h4 class="text-white font-medium text-sm">
                                    {{ info.title }}
                                </h4>
                                <a v-if="info.link"
                                    :href="info.link"
                                    class="text-gray-300 text-sm hover:text-primary transition-colors"
                                    target="_blank"
                                    rel="noopener noreferrer">
                                    {{ info.value }}
                                </a>
                                <p v-else class="text-gray-400 text-sm">
                                    {{ info.value }}
                                </p>
                            </div>
                        </div>
                    </div>
                </div>
                
                <!-- Form -->
                <div class="bg-gray-800/50 border border-gray-700/50 rounded-lg p-6 backdrop-blur-sm">
                    <form @submit.prevent="handleSubmit">
                        <div class="mb-4">
                            <label for="name" class="text-white block mb-2 text-sm font-medium">
                                Name
                            </label>
                            <input id="name"
                            v-model="formData.name"
                            class="w-full px-4 py-2 bg-gray-700 border border-gray-600 rounded-lg text-white text-sm focus:outline-none focus:border-primary transition-colors"
                            placeholder="Input your name"
                            required>
                        </div>

                        <div class="mb-4">
                            <label for="email" class="text-white block mb-2 text-sm font-medium">
                                Email
                            </label>
                            <input type="email" id="email"
                            v-model="formData.email"
                            class="w-full px-4 py-2 bg-gray-700 border border-gray-600 rounded-lg text-white text-sm focus:outline-none focus:border-primary transition-colors"
                            placeholder="your@email.com"
                            required>
                        </div>

                        <div class="mb-6">
                            <label for="message" class="text-white block mb-2 text-sm font-medium">
                                Message
                            </label>
                            <textarea id="message"
                            v-model="formData.message"
                            class="w-full px-4 py-2 bg-gray-700 border border-gray-600 rounded-lg text-white text-sm focus:outline-none focus:border-primary transition-colors"
                            placeholder="Let’s chat. Drop a message!"
                            rows="4"
                            required />
                        </div>
                        
                        <!-- INAYOS: Sinara nang buo ang naputol mong button element at form tag -->
                        <button type="submit" :disabled="isSubmitting"
                        class="w-full px-6 py-2.5 bg-primary text-white rounded-lg font-medium hover:bg-primary/80 transition-colors disabled:opacity-50 disabled:cursor-not-allowed">
                            {{ isSubmitting ? 'Sending...' : 'Send Message' }}
                        </button>
                    </form>
                </div>
            </div>
        </div>

        <!-- FOOTER LAYER: Narito na siya sa loob ng section pero selyadong nasa pinakailalim na ngayon -->
        <div class="w-full text-center relative z-10 text-sm text-white">
            <p>© All Rights Reserved. |  Raymond Seeno</p>
        </div>
        
    </section>
</template>