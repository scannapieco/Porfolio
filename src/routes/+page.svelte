<script>
    import Icon from '@iconify/svelte';
    let name = '';
    let email = '';
    let message = '';
    let isSent = false;

    const sendEmail = async (e) => {
        e.preventDefault();

        const formData = {
            user_name: name,
            user_email: email,
            message: message,
        };

        try {
            const res = await fetch('https://api.emailjs.com/api/v1.0/email/send', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify({
                    service_id: 'your_service_id',
                    template_id: 'your_template_id',
                    user_id: 'your_user_id',
                    template_params: formData,
                }),
            });

            if (res.ok) {
                isSent = true;
                name = '';
                email = '';
                message = '';
            } else {
                console.log('Failed to send email');
            }
        } catch (error) {
            console.error('Error sending email:', error);
        }
    };
</script>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@500&family=Raleway:wght@400;700&display=swap');

    body {
        background-color: #0f172a;
        
        font-family: 'Raleway', sans-serif;
        margin: 0;
        padding: 0;
    }
    nav {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 1rem 2rem;
        background-color: #d7ef04e7;
    }
    nav .logo {
        font-size: 1.5rem;
        font-weight: bold;
        font-family: 'Orbitron', sans-serif;
        color: #000000;
    }
    nav ul {
        display: flex;
        gap: 1.5rem;
        list-style: none;
    }
    nav ul li a {
        text-decoration: none;
        color: rgb(7, 7, 7);
        font-weight: 500;
    }
    .hero {
        text-align: center;
        padding: 2rem 2rem;
        background: linear-gradient(to bottom, #1e2b1a, #2a3b24);
    }
    .hero img {
        border-radius: 50%;
        width: 120px;
        height: 120px;
        margin-bottom: 1rem;
    }
    .section {
        padding: 4rem 2rem;
        max-width: 900px;
        margin: 0 auto;
    }
    .projects, .technologies {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
        gap: 2rem;
       
    }
    .card {
        background-color: #2d3a2f;
        padding: 1rem;
        border-radius: 0; /* sin radius para minimalismo */
        border: 1px solid #445544;
    }
    .card:nth-child(even) {
        border-radius: 0.75rem;
    }
    .contact-form {
        background-color: #2d3a2f;
        padding: 2rem;
        border: 1px solid #445544;
        display: flex;
        flex-direction: column;
        gap: 1rem;
    }
    .contact-form input,
    .contact-form textarea {
        padding: 0.75rem;
        border: none;
        border-radius: 0;
        background-color: #1e293b;
        color: white;
    }
    .contact-form textarea {
        border-radius: 0.5rem;
    }
    .contact-form button {
        padding: 0.75rem;
        border: none;
        border-radius: 0.5rem;
        background-color: #aeb1b2;
        color: rgb(5, 5, 5);
        font-weight: bold;
    }
</style>

<!-- Navbar -->
<nav class="flex justify-between items-center px-6 py-4 shadow-md">
    <div class="text-2xl font-bold logo">Diego Garcia</div>
    <ul class="flex space-x-6">
        <li><a href="#projects" class="hover:text-green-500">PROJECTS</a></li>
        <li><a href="#technologies" class="hover:text-green-500">SKILLS</a></li>
        <li><a href="#contact" class="hover:text-green-500">CONTACT</a></li>
    </ul>
</nav>

<!-- Hero -->
<section class="h-screen bg-gradient-to-b from-dark-600 to-white-800 flex flex-col justify-center items-center text-center px-6">
    <h1 class="text-2xl md:text-8xl font-extrabold text-blck tracking-wide mb-4" in:fly={{ y: -50, duration: 1000 }}>
        Front-End Developer
    </h1>
    <p class="font-bold text-green-800 text-2xl md:text-2xl max-w-2xl" in:fly={{ y: 70, duration: 3000, delay: 100 }}>
         Design and build clean, responsive web interfaces using modern technologies like Svelte, Tailwind CSS and JavaScript.
    </p>
</section>

  
  <!-- Projects -->
  <section id="projects" class="bg-white dark:bg-white-900 py-1 px-10 text-center">
    <h2 class="text-6xl font-bold text-gray-800 dark:text-black mb-12">PROJECTS</h2>
    <div class="grid md:grid-cols-2 gap-8 max-w-6xl mx-auto">
      
      <div class="bg-gray-100 dark:bg-gray-800 rounded-2xl p-6 shadow-md hover:shadow-lg transition">
        <h3 class="text-2xl font-semibold text-gray-900 dark:text-white mb-2">WeatherAppReact</h3>
        <p class="text-gray-700 dark:text-gray-300 mb-4">A weather app built with React that shows up-to-date weather info.</p>
        <a href="https://github.com/scannapieco/weatherappreact" target="_blank" class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition">View on GitHub</a>
      </div>
  
      <div class="bg-gray-100 dark:bg-gray-800 rounded-2xl p-6 shadow-md hover:shadow-lg transition">
        <h3 class="text-2xl font-semibold text-gray-900 dark:text-white mb-2">Bento-grid</h3>
        <p class="text-gray-700 dark:text-gray-300 mb-4">A modern bento grid layout with responsive design using HTML and CSS.</p>
        <img src="./Bento.png" alt="ilustracion" class="w-full h-auto rounded-l mb-4">
        <a href="https://github.com/scannapieco/Bento-grid" target="_blank" class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition">View on GitHub</a>
      </div>
  
      <div class="bg-gray-100 dark:bg-gray-800 rounded-2xl p-6 shadow-md hover:shadow-lg transition">
        <h3 class="text-2xl font-semibold text-gray-900 dark:text-white mb-2">Blog Preview Card</h3>
        <p class="text-gray-700 dark:text-gray-300 mb-4">A component that previews a blog post with elegant layout and semantic HTML.</p>
        <a href="https://github.com/scannapieco/Blog-Preview-Card" target="_blank" class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition">View on GitHub</a>
      </div>
  
      <div class="bg-gray-100 dark:bg-gray-800 rounded-2xl p-6 shadow-md hover:shadow-lg transition">
        <h3 class="text-2xl font-semibold text-gray-900 dark:text-white mb-2">Contact Form</h3>
        <p class="text-gray-700 dark:text-gray-300 mb-4">A styled contact form made with HTML and CSS focused on accessibility and design.</p>
        <a href="https://github.com/scannapieco/Contact-form" target="_blank" class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition">View on GitHub</a>
      </div>
    </div>
  </section>
  
  <!-- Technologies -->
  <section id="technologies" class="py-16 px-6 bg-white-800 text-center">
    <h2 class="text-4xl font-bold text-black mb-10">SKILLS</h2>
    <div class="flex justify-center gap-10 flex-wrap text-white text-center">
      
      {#each [
        { icon: 'logos:html-5', label: 'HTML' },
        { icon: 'logos:css-3', label: 'CSS' },
        { icon: 'logos:javascript', label: 'JavaScript' },
        { icon: 'logos:react', label: 'React' },
        { icon: 'logos:svelte-icon', label: 'Svelte' },
        { icon: 'logos:tailwindcss-icon', label: 'Tailwind' },
        { icon: 'logos:git-icon', label: 'Git' }
      ] as tech, i}
      
        <div
          class="flex flex-col items-center transition-transform duration-300 transform hover:scale-110"
          in:fly={{ y: 20, duration: 500, delay: i * 100 }}
        >
          <Icon icon={tech.icon} class="w-12 h-12" aria-label={tech.label} />
          <span class="mt-2 text-sm text-black">{tech.label}</span>
        </div>
      
      {/each}
    </div>
  </section>
  
  
  <!-- Contact -->
  <section id="contact" class="py-16 px-6 bg-gray-900 text-white text-center">
    <h2 class="text-4xl font-bold mb-10">CONTACT</h2>
    <form class="max-w-xl mx-auto space-y-4" on:submit={sendEmail}>
      <input type="text" bind:value={name} placeholder="Your name" required class="w-full px-4 py-2 rounded-lg bg-gray-800 border border-gray-700" />
      <input type="email" bind:value={email} placeholder="Your email" required class="w-full px-4 py-2 rounded-lg bg-gray-800 border border-gray-700" />
      <textarea rows="5" bind:value={message} placeholder="Your message" required class="w-full px-4 py-2 rounded-lg bg-gray-800 border border-gray-700"></textarea>
      <button type="submit" class="bg-blue-600 hover:bg-blue-700 px-6 py-2 rounded-lg text-white transition">Send</button>
      {#if isSent}
        <p class="text-green-400 mt-4">Message sent successfully ✅</p>
      {/if}
    </form>
  </section>
