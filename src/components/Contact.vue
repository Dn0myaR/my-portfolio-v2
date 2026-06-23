<script setup>
import { Github, Linkedin, Mail } from 'lucide-vue-next';
import { reactive, ref } from 'vue';
import emailjs from 'emailjs-com'

    
    const contactInfo = [
        { 
            id: 1,
            icon: Mail,
            title: "Email",
            value: "cer.rhei@gmail.com",
            link: "https://mail.google.com/mail/?view=cm&fs=1&to=cer.rhei@gmail.com"

        },
        { 
            id: 2,
            icon: Linkedin,
            title: "LinkedIN",
            value: "www.linkedin.com/in/raymondsereno",
            link: "https://www.linkedin.com/in/raymondsereno"

        },
        {
            id: 3,
            icon: Github, // import { Github } from 'lucide-vue-next'
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
            'service_qwf78a4',      // Service ID
            // 'template_ilh84t2',     // Template ID
            'template_kynjmbl',
            {   name: formData.name,
                from_email: formData.email,
                subject: formData.subject,
                message: formData.message
            },
            'IzAY2DUjGGn7SHua3'       // Public Key
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
    <section class="py-20 bg-gray-900" id="contact">
        <div class="container mx-auto px-4 max-w-6xl">
            <div class="text-center mb-12">
                <h2 class="text-3xl md:text-5xl font-extrabold
                text-white mb-2">
                    Connect with me
                </h2>
                <div class="w-28 h-1 bg-primary mx-auto mt-2
                rounded-2xl"></div>
            </div>
            <div class="grid md:grid-cols-2 gap-8">
                <div>
                    <p class="text-gray-400 mb-8 leading-relaxed">
                        <!-- Let’s chat. Drop a message! -->
                    </p>
                    <div class="space-y-6">
                        <div v-for="info in contactInfo" :key="info.id"
                        class="flex items-center gap-4 group">
                            <div class="w-10 h-10 rounded-full bg-primary/10
                            flex items-center justify-center 
                            group-hover:bg-primary/20 transition-colors">
                                <component :is="info.icon" :size="18"
                                class="text-primary" />
                            </div>
                            <div>
                                <h4 class="text-white font-medium text-sm">
                                    {{ info.title }}
                                </h4>
                                <!-- <a v-if="info.link"  :href="info.link"
                                    class="text-gray-400 text-sm
                                    hover:text-primary transition-colors"
                                    :target="info.title === 'Location' ?
                                    '_self' : '_blank'"
                                    :ref="info.title === 'Location' ? ''
                                    : 'noopener noreferrer'">
                                    {{ info.value }}
                                </a> -->
                                <a v-if="info.link"
                                    :href="info.link"
                                    class="text-gray-400 text-sm hover:text-primary transition-colors"
                                    :target="info.title === 'Location' ? '_self' : '_blank'"
                                    :rel="info.title === 'Location' ? '' : 'noopener noreferrer'">
                                    {{ info.value }}
                                </a>


                                <p v-else class="text-gray-400 text-sm">
                                    {{ info.value }}
                                </p>
                            </div>
                        </div>
                    </div>
                </div>
                     <!-- form -->
                <div class="bg-gray-800 rounded-lg p-6">
                    <form @submit.prevent="handleSubmit">
                        <div class="mb-4">
                            <label for="name" class="text-white
                            block mb-2 text-sm font-medium">
                                Name
                            </label>
                            <input id="name"
                            v-model="formData.name"
                            class="w-full px-4 py-2 bg-gray-700
                            border border-gray-600 rounded-lg text-white 
                            text-sm focus:outline-none focus:border-primary
                            transition-colors"
                            placeholder="Input your name"
                            required>
                        </div>

                        <div class="mb-4">
                            <label for="email" class="text-white
                            block mb-2 text-sm font-medium">
                                Email
                            </label>
                            <input type="email" id="email"
                            v-model="formData.email"
                            class="w-full px-4 py-2 bg-gray-700
                            border border-gray-600 rounded-lg text-white 
                            text-sm focus:outline-none focus:border-primary
                            transition-colors"
                            placeholder="your@email.com"
                            required>
                        </div>


                         <div class="mb-6">
                            <label for="message" class="text-white
                            block mb-2 text-sm font-medium">
                                Message
                            </label>
                            <textarea id="message"
                            v-model="formData.message"
                            class="w-full px-4 py-2 bg-gray-700
                            border border-gray-600 rounded-lg text-white 
                            text-sm focus:outline-none focus:border-primary
                            transition-colors"
                            placeholder="Let’s chat. Drop a message!"
                            rows="4"
                            required />
                        </div>
                        <button type="submit" :disabled="isSubmitting"
                        class="w-full px-6 py-2.5 bg-primary text-white
                        rounded-lg font-medium hover:bg-primary/80
                        transition-colors disabled:opacity-50 
                        disabled:cursor-not-allowed">
                            {{ isSubmitting ? 'Sending...' : 'Send Message' }}
                        </button>
                    </form>
                </div>
            </div>
        </div>
    </section>
</template>

