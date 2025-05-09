<script lang="ts">
  import { onMount } from 'svelte';
  import Header from '$lib/components/Header.svelte';
  
  // Contact form state
  let formData = {
    name: '',
    email: '',
    phone: '',
    message: '',
    service: ''
  };
  
  let formSubmitted = false;
  let formError = false;
  let whatsappNumber = "+254704800614";
  let formspreeId = "xnndpjbk"; // Replace this with your actual Formspree form ID
  let currentUrl = '';
  
  onMount(() => {
    // Set current URL for redirect after form submission
    currentUrl = window.location.href;
  });
  
  // Available services grouped by categories
  const serviceCategories = [
    {
      name: "Cuts & Styling",
      services: [
        { id: 'precision-cut', name: 'Precision Cut' },
        { id: 'bridal-style', name: 'Bridal Style' },
        { id: 'blowout', name: 'Luxury Blowout' }
      ]
    },
    {
      name: "Braiding",
      services: [
        { id: 'normal-braids', name: 'Normal Braids' },
        { id: 'knotless-braids', name: 'Knotless Braids' },
        { id: 'goddess-braids', name: 'Goddess Braids' },
        { id: 'boho-braids', name: 'Boho Braids' },
        { id: 'loose-braids', name: 'Loose Braids' }
      ]
    },
    {
      name: "Twists & Coils",
      services: [
        { id: 'marley-twist', name: 'Marley Twist' },
        { id: 'coco-twists', name: 'Coco Twists' },
        { id: 'spring-twist', name: 'Spring Twist' },
        { id: 'passion-twist', name: 'Passion Twist' },
        { id: 'twist-outs', name: 'Twist Outs' }
      ]
    },
    {
      name: "Cornrows & Lines",
      services: [
        { id: 'ghanaians', name: 'Ghanaians' },
        { id: 'half-liners', name: 'Half Liners' }
      ]
    },
    {
      name: "Hair Treatments",
      services: [
        { id: 'deep-conditioning', name: 'Deep Conditioning' },
        { id: 'hair-treatment', name: 'Hair Treatment' },
        { id: 'keratin', name: 'Keratin/Botox Treatment' },
        { id: 'scalp-treatment', name: 'Scalp Treatment' }
      ]
    },
    {
      name: "Coloring Services",
      services: [
        { id: 'balayage', name: 'Balayage' },
        { id: 'eco-color', name: 'Eco Color' },
        { id: 'color-correction', name: 'Color Correction' },
        { id: 'hair-dyeing', name: 'Hair Coloring/Dyeing' }
      ]
    },
    {
      name: "Styling Tools & Enhancements",
      services: [
        { id: 'washing', name: 'Hair Washing & Conditioning' },
        { id: 'blowdry-iron', name: 'Blow-Dry & Flat Ironing' },
        { id: 'silk-press', name: 'Silk Press' },
        { id: 'extensions', name: 'Hair Extensions/Weaves' },
        { id: 'dreadlocks', name: 'Dreadlocks/Retwisting' }
      ]
    }
  ];
  
  // Flat list of all services for WhatsApp link generation
  const services = [
    { id: '', name: 'Select a service (optional)' },
    ...serviceCategories.flatMap(category => category.services)
  ];
  
  // Generate WhatsApp message
  function createWhatsAppLink() {
    let message = `Hello Belle Royale, my name is ${formData.name}`;
    
    if (formData.service) {
      const serviceObj = services.find(s => s.id === formData.service);
      if (serviceObj) {
        message += ` and I'm interested in ${serviceObj.name}`;
      }
    }
    
    message += ". Here's my message: " + formData.message;
    
    if (formData.email) {
      message += ` (My email: ${formData.email})`;
    }
    
    if (formData.phone) {
      message += ` (My phone: ${formData.phone})`;
    }
    
    return `https://wa.me/${whatsappNumber.replace(/\D/g, '')}?text=${encodeURIComponent(message)}`;
  }
  
  // Handle form submission
  async function handleSubmit(event: Event) {
    // Prevent default form submission
    event.preventDefault();
    
    // Get form element
    const form = event.target as HTMLFormElement;
    
    // For Formspree, we'll send the form data as FormData
    try {
      const response = await fetch(`https://formspree.io/f/${formspreeId}`, {
        method: "POST",
        body: new FormData(form),
        headers: {
          Accept: "application/json"
        }
      });
      
      if (response.ok) {
        formSubmitted = true;
        formData = {
          name: '',
          email: '',
          phone: '',
          message: '',
          service: ''
        };
      } else {
        formError = true;
      }
    } catch (error) {
      formError = true;
    }
  }
</script>

<svelte:head>
  <title>Contact Us | Belle Royale</title>
  <meta name="description" content="Get in touch with Belle Royale salon. Contact us for appointments, questions about our services, or to join our team.">
</svelte:head>

<Header />

<main id="main-content" class="pt-24 pb-20">
  <!-- Hero Banner -->
  <div class="bg-black text-white py-16 px-4">
    <div class="max-w-4xl mx-auto text-center">
      <h1 class="text-4xl md:text-5xl font-bold font-playfair mb-4">Contact <span class="text-gold">Us</span></h1>
      <p class="text-lg font-lato font-light max-w-2xl mx-auto">
        Have questions or want to book an appointment? Reach out to our team.
      </p>
    </div>
  </div>
  
  <!-- Contact Info & Form Section -->
  <section class="py-16 px-4">
    <div class="max-w-5xl mx-auto">
      <div class="grid grid-cols-1 md:grid-cols-2 gap-12">
        <!-- Contact Information -->
        <div>
          <h2 class="text-3xl font-bold font-playfair mb-6">Get In Touch</h2>
          
          <div class="space-y-8">
            <div class="flex items-start">
              <div class="bg-gold/20 rounded-full p-3 mr-4">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-gold" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z" />
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" />
                </svg>
              </div>
              <div>
                <h3 class="text-xl font-bold font-playfair mb-2">Location</h3>
                <p class="text-gray-600 font-lato">
                  Nairobi, Kenya<br>
                  Khetias Supermarket, Mirema<br>
                  Zimmerman
                </p>
              </div>
            </div>
            
            <div class="flex items-start">
              <div class="bg-gold/20 rounded-full p-3 mr-4">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-gold" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" />
                </svg>
              </div>
              <div>
                <h3 class="text-xl font-bold font-playfair mb-2">Hours</h3>
                <p class="text-gray-600 font-lato">
                  Monday - Friday: 9:00 AM - 8:00 PM<br>
                  Saturday: 9:00 AM - 6:00 PM<br>
                  Sunday: 10:00 AM - 4:00 PM
                </p>
              </div>
            </div>
            
            <div class="flex items-start">
              <div class="bg-gold/20 rounded-full p-3 mr-4">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-gold" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z" />
                </svg>
              </div>
              <div>
                <h3 class="text-xl font-bold font-playfair mb-2">Phone</h3>
                <p class="text-gray-600 font-lato">
                  <a href="tel:+254704800614" class="hover:text-gold transition-colors">(254) 704-800-614</a>
                </p>
              </div>
            </div>
            
            <div class="flex items-start">
              <div class="bg-gold/20 rounded-full p-3 mr-4">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-gold" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
                </svg>
              </div>
              <div>
                <h3 class="text-xl font-bold font-playfair mb-2">Email</h3>
                <p class="text-gray-600 font-lato">
                  <a href="mailto:info@belleroyale.com" class="hover:text-gold transition-colors">infobelleroyale@gmail.com</a>
                </p>
              </div>
            </div>
          </div>
          
          <!-- Social Media Links -->
          <div class="mt-10">
            <h3 class="text-xl font-bold font-playfair mb-4">Follow Us</h3>
            <div class="flex space-x-4">
              <a href="https://instagram.com" target="_blank" rel="noopener noreferrer" class="bg-gold/20 p-3 rounded-full text-gold hover:bg-gold hover:text-white transition-colors">
                <span class="sr-only">Instagram</span>
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="currentColor" viewBox="0 0 24 24">
                  <path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zm0-2.163c-3.259 0-3.667.014-4.947.072-4.358.2-6.78 2.618-6.98 6.98-.059 1.281-.073 1.689-.073 4.948 0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.058 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98-1.281-.059-1.69-.073-4.949-.073zm0 5.838c-3.403 0-6.162 2.759-6.162 6.162s2.759 6.163 6.162 6.163 6.162-2.759 6.162-6.163c0-3.403-2.759-6.162-6.162-6.162zm0 10.162c-2.209 0-4-1.79-4-4 0-2.209 1.791-4 4-4s4 1.791 4 4c0 2.21-1.791 4-4 4zm6.406-11.845c-.796 0-1.441.645-1.441 1.44s.645 1.44 1.441 1.44c.795 0 1.439-.645 1.439-1.44s-.644-1.44-1.439-1.44z"/>
                </svg>
              </a>
              
              <a href="https://facebook.com" target="_blank" rel="noopener noreferrer" class="bg-gold/20 p-3 rounded-full text-gold hover:bg-gold hover:text-white transition-colors">
                <span class="sr-only">Facebook</span>
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="currentColor" viewBox="0 0 24 24">
                  <path d="M9 8h-3v4h3v12h5v-12h3.642l.358-4h-4v-1.667c0-.955.192-1.333 1.115-1.333h2.885v-5h-3.808c-3.596 0-5.192 1.583-5.192 4.615v3.385z"/>
                </svg>
              </a>
              
              <a href="https://pinterest.com" target="_blank" rel="noopener noreferrer" class="bg-gold/20 p-3 rounded-full text-gold hover:bg-gold hover:text-white transition-colors">
                <span class="sr-only">Pinterest</span>
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="currentColor" viewBox="0 0 24 24">
                  <path d="M12 0c-6.627 0-12 5.372-12 12 0 5.084 3.163 9.426 7.627 11.174-.105-.949-.2-2.405.042-3.441.218-.937 1.407-5.965 1.407-5.965s-.359-.719-.359-1.782c0-1.668.967-2.914 2.171-2.914 1.023 0 1.518.769 1.518 1.69 0 1.029-.655 2.568-.994 3.995-.283 1.194.599 2.169 1.777 2.169 2.133 0 3.772-2.249 3.772-5.495 0-2.873-2.064-4.882-5.012-4.882-3.414 0-5.418 2.561-5.418 5.207 0 1.031.397 2.138.893 2.738.098.119.112.224.083.345l-.333 1.36c-.053.22-.174.267-.402.161-1.499-.698-2.436-2.889-2.436-4.649 0-3.785 2.75-7.262 7.929-7.262 4.163 0 7.398 2.967 7.398 6.931 0 4.136-2.607 7.464-6.227 7.464-1.216 0-2.359-.631-2.75-1.378l-.748 2.853c-.271 1.043-1.002 2.35-1.492 3.146 1.124.347 2.317.535 3.554.535 6.627 0 12-5.373 12-12 0-6.628-5.373-12-12-12z"/>
                </svg>
              </a>
              
              <a href="https://tiktok.com" target="_blank" rel="noopener noreferrer" class="bg-gold/20 p-3 rounded-full text-gold hover:bg-gold hover:text-white transition-colors">
                <span class="sr-only">TikTok</span>
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="currentColor" viewBox="0 0 24 24">
                  <path d="M12.525.02c1.31-.02 2.61-.01 3.91-.02.08 1.53.63 3.09 1.75 4.17 1.12 1.11 2.7 1.62 4.24 1.79v4.03c-1.44-.05-2.89-.35-4.2-.97-.57-.26-1.1-.59-1.62-.93-.01 2.92.01 5.84-.02 8.75-.08 1.4-.54 2.79-1.35 3.94-1.31 1.92-3.58 3.17-5.91 3.21-1.43.08-2.86-.31-4.08-1.03-2.02-1.19-3.44-3.37-3.65-5.71-.02-.5-.03-1-.01-1.49.18-1.9 1.12-3.72 2.58-4.96 1.66-1.44 3.98-2.13 6.15-1.72.02 1.48-.04 2.96-.04 4.44-.99-.32-2.15-.23-3.02.37-.63.41-1.11 1.04-1.36 1.75-.21.51-.15 1.07-.14 1.61.24 1.64 1.82 3.02 3.5 2.87 1.12-.01 2.19-.66 2.77-1.61.19-.33.4-.67.41-1.06.1-1.79.06-3.57.07-5.36.01-4.03-.01-8.05.02-12.07z"/>
                </svg>
              </a>
            </div>
          </div>
        </div>
        
        <!-- Contact Form -->
        <div class="bg-light-gray p-8 rounded-lg shadow-md">
          <h2 class="text-2xl font-bold font-playfair mb-6">Send Us a Message</h2>
          
          {#if formSubmitted}
            <div class="bg-eco-green/20 text-eco-green p-4 rounded-md mb-6">
              <p class="font-bold">Thank you for your message!</p>
              <p>We'll get back to you as soon as possible.</p>
            </div>
          {/if}
          
          {#if formError}
            <div class="bg-red-100 text-red-700 p-4 rounded-md mb-6">
              <p class="font-bold">There was an error sending your message.</p>
              <p>Please try again later or contact us directly by phone.</p>
            </div>
          {/if}
          
          <form on:submit|preventDefault={handleSubmit} class="space-y-4">
            <div>
              <label for="name" class="block text-gray-700 font-bold mb-2">Name *</label>
              <input 
                type="text" 
                id="name" 
                name="name"
                bind:value={formData.name} 
                required
                class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-gold"
              />
            </div>
            
            <div>
              <label for="email" class="block text-gray-700 font-bold mb-2">Email *</label>
              <input 
                type="email" 
                id="email" 
                name="email"
                bind:value={formData.email} 
                required
                class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-gold"
              />
              <!-- Hidden field for Formspree reply-to feature -->
              <input type="hidden" name="_replyto" value={formData.email} />
            </div>
            
            <div>
              <label for="phone" class="block text-gray-700 font-bold mb-2">Phone</label>
              <input 
                type="tel" 
                id="phone" 
                name="phone"
                bind:value={formData.phone}
                class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-gold"
              />
            </div>
            
            <div>
              <label for="service" class="block text-gray-700 font-bold mb-2">Service of Interest</label>
              <select 
                id="service" 
                name="service"
                bind:value={formData.service}
                class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-gold"
              >
                <option value="">Select a service (optional)</option>
                
                {#each serviceCategories as category}
                  <optgroup label={category.name}>
                    {#each category.services as service}
                      <option value={service.id}>{service.name}</option>
                    {/each}
                  </optgroup>
                {/each}
              </select>
            </div>
            
            <div>
              <label for="message" class="block text-gray-700 font-bold mb-2">Message *</label>
              <textarea 
                id="message" 
                name="message"
                bind:value={formData.message} 
                required
                rows="5"
                class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-gold"
              ></textarea>
            </div>
            
            <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
              <button 
                type="submit" 
                class="bg-gold hover:bg-gold-dark text-black font-bold py-3 px-6 rounded-full transition-colors focus:outline-none focus:ring-2 focus:ring-gold focus:ring-opacity-50 flex items-center justify-center"
              >
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
                </svg>
                Send via Email
              </button>
              
              <a 
                href={createWhatsAppLink()}
                target="_blank"
                rel="noopener noreferrer"
                class="bg-[#25D366] hover:bg-[#128C7E] text-white font-bold py-3 px-6 rounded-full transition-colors focus:outline-none focus:ring-2 focus:ring-[#25D366] focus:ring-opacity-50 flex items-center justify-center disabled:opacity-50 disabled:pointer-events-none"
                class:pointer-events-none={!formData.name || !formData.message}
                aria-disabled={!formData.name || !formData.message}
              >
                <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" fill="currentColor" class="mr-2" viewBox="0 0 16 16">
                  <path d="M13.601 2.326A7.854 7.854 0 0 0 7.994 0C3.627 0 .068 3.558.064 7.926c0 1.399.366 2.76 1.057 3.965L0 16l4.204-1.102a7.933 7.933 0 0 0 3.79.965h.004c4.368 0 7.926-3.558 7.93-7.93A7.898 7.898 0 0 0 13.6 2.326zM7.994 14.521a6.573 6.573 0 0 1-3.356-.92l-.24-.144-2.494.654.666-2.433-.156-.251a6.56 6.56 0 0 1-1.007-3.505c0-3.626 2.957-6.584 6.591-6.584a6.56 6.56 0 0 1 4.66 1.931 6.557 6.557 0 0 1 1.928 4.66c-.004 3.639-2.961 6.592-6.592 6.592zm3.615-4.934c-.197-.099-1.17-.578-1.353-.646-.182-.065-.315-.099-.445.099-.133.197-.513.646-.627.775-.114.133-.232.148-.43.05-.197-.1-.836-.308-1.592-.985-.59-.525-.985-1.175-1.103-1.372-.114-.198-.011-.304.088-.403.087-.088.197-.232.296-.346.1-.114.133-.198.198-.33.065-.134.034-.248-.015-.347-.05-.099-.445-1.076-.612-1.47-.16-.389-.323-.335-.445-.34-.114-.007-.247-.007-.38-.007a.729.729 0 0 0-.529.247c-.182.198-.691.677-.691 1.654 0 .977.71 1.916.81 2.049.098.133 1.394 2.132 3.383 2.992.47.205.84.326 1.129.418.475.152.904.129 1.246.08.38-.058 1.171-.48 1.338-.943.164-.464.164-.86.114-.943-.049-.084-.182-.133-.38-.232z"/>
                </svg>
                Send via WhatsApp
              </a>
            </div>
            
            <!-- Hidden field to help prevent spam -->
            <input type="text" name="_gotcha" style="display:none" />
            
            <!-- Redirect after form submission -->
            <input type="hidden" name="_next" value={currentUrl} />
          </form>
        </div>
      </div>
    </div>
  </section>
  
  <!-- Map Section -->
  <section class="py-16 px-4 bg-light-gray">
    <div class="max-w-5xl mx-auto">
      <div class="text-center mb-12">
        <span class="text-gold uppercase tracking-wider font-lato text-sm font-bold">Find Us</span>
        <h2 class="text-3xl font-bold mt-2 mb-4 font-playfair">Our Location</h2>
        <div class="w-24 h-1 bg-gold mx-auto"></div>
      </div>
      
      <div class="bg-white p-4 rounded-lg shadow-md">
        <!-- Google Maps embed of Khetias Supermarket Mirema -->
        <iframe 
          src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3988.9238010317245!2d36.89060977486707!3d-1.2132883987751213!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x182f3f607f74d0f1%3A0xf31b117875d8099e!2sKHETIAS%20SUPERMARKET%20Mirema!5e0!3m2!1sen!2ske!4v1746178665935!5m2!1sen!2ske" 
          width="100%" 
          height="400" 
          style="border:0;" 
          allowFullScreen={true}
          loading="lazy" 
          referrerpolicy="no-referrer-when-downgrade"
          title="Belle Royale Salon Location"
          class="rounded-lg"
        ></iframe>
      </div>
    </div>
  </section>
  
  <!-- Join Our Team CTA -->
  <section class="py-16 px-4">
    <div class="max-w-4xl mx-auto text-center">
      <div class="bg-black text-white p-12 rounded-xl relative overflow-hidden">
        <!-- Decorative background pattern -->
        <div class="absolute inset-0 opacity-10">
          <svg width="100%" height="100%" xmlns="http://www.w3.org/2000/svg">
            <defs>
              <pattern id="grid" width="40" height="40" patternUnits="userSpaceOnUse">
                <path d="M 0 20 L 40 20 M 20 0 L 20 40" stroke="white" stroke-width="1"/>
              </pattern>
            </defs>
            <rect width="100%" height="100%" fill="url(#grid)" />
          </svg>
        </div>
        
        <div class="relative z-10">
          <h2 class="text-3xl font-bold font-playfair mb-4">Join Our Team</h2>
          <p class="text-lg font-lato font-light max-w-2xl mx-auto mb-8">
            Are you a passionate stylist committed to sustainable beauty? We're always looking for 
            talented individuals to join our team. Send us your portfolio and resume.
          </p>
          
          <a 
            href="mailto:infobelleroyale@gmail.com" 
            class="bg-gold hover:bg-gold-dark text-black font-bold py-3 px-8 rounded-full transition-colors inline-flex items-center"
          >
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
            </svg>
            infobelleroyale@gmail.com
          </a>
        </div>
      </div>
    </div>
  </section>
</main>

<style>
  .bg-light-gray {
    background-color: #F5F5F5;
  }
  
  .text-gold {
    color: #D4AF37;
  }
  
  .bg-gold {
    background-color: #D4AF37;
  }
  
  .hover\:bg-gold-dark:hover {
    background-color: #B8860B;
  }
  
  .bg-eco-green {
    background-color: #5D8C66;
  }
  
  .text-eco-green {
    color: #5D8C66;
  }
  
  .font-playfair {
    font-family: 'Playfair Display', serif;
  }
  
  .font-lato {
    font-family: 'Lato', sans-serif;
  }
</style> 