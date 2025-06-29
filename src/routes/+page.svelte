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
                    service_id: 'your_service_id',      // Reemplaza con tu service_id real
                    template_id: 'your_template_id',    // Reemplaza con tu template_id real
                    user_id: 'your_user_id',            // Reemplaza con tu user_id real
                    template_params: formData,
                }),
            });

            if (res.ok) {
                isSent = true;
                name = '';
                email = '';
                message = '';
            } else {
                isSent = false;
                console.log('Failed to send email');
            }
        } catch (error) {
            isSent = false;
            console.error('Error sending email:', error);
        }
    };

</script>

<!-- svelte-ignore css_unused_selector -->
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

<!-- Floating Sidebar Social -->
<div class="fixed top-1/3 left-4 z-50 flex flex-col gap-4 items-center">
  <!-- LinkedIn -->
  <a href="https://www.linkedin.com/in/diegogarciascannapieco/" target="_blank" rel="noopener" class="group">
    <Icon icon="mdi:linkedin" class="w-8 h-8 text-blue-700 group-hover:scale-110 transition" />
  </a>
  <!-- GitHub -->
  <a href="https://github.com/scannapieco" target="_blank" rel="noopener" class="group">
    <Icon icon="mdi:github" class="w-8 h-8 text-black dark:text-white group-hover:scale-110 transition" />
  </a>
  <!-- CV -->
  <a href="/CV.pdf" download class="group">
    <Icon icon="mdi:file-account" class="w-8 h-8 text-green-700 group-hover:scale-110 transition" />
  </a>
  <!-- Email -->
  <a href="mailto:diego.scannapieco@gmail.com" class="group">
    <Icon icon="mdi:email" class="w-8 h-8 text-red-600 group-hover:scale-110 transition" />
  </a>
</div>

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

      <!-- Proyecto: GoPass -->
      <div class="bg-gray-100 dark:bg-gray-800 rounded-2xl p-6 shadow-md hover:shadow-lg transition">
        <h3 class="text-2xl font-semibold text-gray-900 dark:text-white mb-2">GoPass - Plataforma Antirreventa</h3>
        <div class="mb-4">
          <iframe width="100%" height="215" src="https://www.youtube.com/embed/GbVOSw_JDzw" title="GoPass Demo" frameborder="0" allowfullscreen class="rounded-lg"></iframe>
        </div>
        <p class="text-gray-700 dark:text-gray-300 mb-4">
          GoPass es una plataforma web enfocada en combatir la reventa fraudulenta de entradas para eventos deportivos en Argentina. Como responsable del equipo frontend, participé en el desarrollo de componentes clave para el registro de usuarios, la compra y reventa de entradas, así como en la integración con el backend para garantizar transferencias seguras.<br>
          Trabajamos con tecnologías como React, TypeScript, Redux Toolkit, Tailwind CSS, .NET, C#, y la API de Ticketmaster.
        </p>
        <div class="flex flex-wrap gap-2 mb-4 justify-center">
          <span class="bg-blue-200 text-blue-800 px-2 py-1 rounded text-xs">React</span>
          <span class="bg-blue-100 text-blue-900 px-2 py-1 rounded text-xs">TypeScript</span>
          <span class="bg-green-200 text-green-800 px-2 py-1 rounded text-xs">Redux Toolkit</span>
          <span class="bg-cyan-200 text-cyan-800 px-2 py-1 rounded text-xs">Tailwind CSS</span>
          <span class="bg-gray-200 text-gray-800 px-2 py-1 rounded text-xs">.NET</span>
          <span class="bg-gray-300 text-gray-900 px-2 py-1 rounded text-xs">C#</span>
          <span class="bg-yellow-200 text-yellow-800 px-2 py-1 rounded text-xs">Ticketmaster API</span>
        </div>
        <a href="https://github.com/IgrowkerTraining/i003-gopass-front" target="_blank" class="inline-flex items-center justify-center w-12 h-12 bg-black rounded-full hover:bg-gray-800 transition" aria-label="Ver en GitHub">
          <Icon icon="mdi:github" class="w-7 h-7 text-white" />
        </a>
      </div>

                       <div class="bg-gray-100 dark:bg-gray-800 rounded-2xl p-6 shadow-md hover:shadow-lg transition flex flex-col h-full">
                  <h3 class="text-2xl font-semibold text-gray-900 dark:text-white mb-2">WeatherAppReact</h3>
                  <div class="mb-4">
                    <img src="/weatherapp-preview.png" alt="WeatherAppReact preview" class="w-full h-48 object-cover rounded-lg mb-2" />
                  </div>
                  <p class="text-gray-700 dark:text-gray-300 mb-4">
                    WeatherAppReact es una aplicación web que muestra información meteorológica actualizada de cualquier ciudad del mundo. Permite buscar ciudades y ver detalles como temperatura, humedad y condiciones del clima, utilizando la API de OpenWeatherMap.
                  </p>
                  <div class="flex flex-wrap gap-2 mb-4 justify-center">
                    <span class="bg-blue-200 text-blue-800 px-2 py-1 rounded text-xs">React</span>
                    <span class="bg-blue-100 text-blue-900 px-2 py-1 rounded text-xs">JavaScript</span>
                    <span class="bg-cyan-200 text-cyan-800 px-2 py-1 rounded text-xs">CSS</span>
                    <span class="bg-gray-200 text-gray-800 px-2 py-1 rounded text-xs">OpenWeatherMap API</span>
                  </div>
                  <div class="flex flex-col items-center mt-auto gap-2">
                    <a href="https://github.com/scannapieco/weatherappreact" target="_blank" class="inline-flex items-center justify-center w-12 h-12 bg-black rounded-full hover:bg-gray-800 transition mb-2" aria-label="Ver en GitHub">
                      <Icon icon="mdi:github" class="w-7 h-7 text-white" />
                    </a>
                    <a href="https://tiempapp.netlify.app/" target="_blank" class="inline-block bg-blue-600 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded transition">
                      Ver Demo
                    </a>
                  </div>
                </div>
<!-- Proyecto: Research Imagen -->
<div class="bg-gray-100 dark:bg-gray-800 rounded-2xl p-6 shadow-md hover:shadow-lg transition">
  <h3 class="text-2xl font-semibold text-gray-900 dark:text-white mb-2">Research Imagen</h3>
  <div class="mb-4">
    <img src="https://raw.githubusercontent.com/scannapieco/reserch-imagen/main/public/preview.png" alt="Research Imagen preview" class="w-full h-48 object-cover rounded-lg mb-2" />
  </div>
  <p class="text-gray-700 dark:text-gray-300 mb-4">
    Research Imagen es una aplicación web para buscar, visualizar y guardar imágenes de alta calidad utilizando la API de Unsplash. Permite explorar tendencias, realizar búsquedas personalizadas y gestionar una galería personal de favoritos.
  </p>
  <div class="flex flex-wrap gap-2 mb-4 justify-center">
    <span class="bg-blue-200 text-blue-800 px-2 py-1 rounded text-xs">React</span>
    <span class="bg-blue-100 text-blue-900 px-2 py-1 rounded text-xs">JavaScript</span>
    <span class="bg-cyan-200 text-cyan-800 px-2 py-1 rounded text-xs">CSS</span>
    <span class="bg-gray-200 text-gray-800 px-2 py-1 rounded text-xs">Unsplash API</span>
    
  </div>
  <a href="https://github.com/scannapieco/reserch-imagen" target="_blank" class="inline-flex items-center justify-center w-12 h-12 bg-black rounded-full hover:bg-gray-800 transition" aria-label="View on GitHub">
    <Icon icon="mdi:github" class="w-7 h-7 text-white" />
  </a>
</div>
  
      <div class="bg-gray-100 dark:bg-gray-800 rounded-2xl p-6 shadow-md hover:shadow-lg transition">
        <h3 class="text-2xl font-semibold text-gray-900 dark:text-white mb-2">Bento-grid</h3>
        <p class="text-gray-700 dark:text-gray-300 mb-4">A modern bento grid layout with responsive design using HTML and CSS.</p>
        <img src="./Bento.png" alt="ilustracion" class="w-full h-auto rounded-l mb-4">
        <a href="https://github.com/scannapieco/Bento-grid" target="_blank" class="inline-flex items-center justify-center w-12 h-12 bg-black rounded-full hover:bg-gray-800 transition" aria-label="View on GitHub">
          <Icon icon="mdi:github" class="w-7 h-7 text-white" />
        </a>
      </div>
  
      <div class="bg-gray-100 dark:bg-gray-800 rounded-2xl p-6 shadow-md hover:shadow-lg transition">
        <h3 class="text-2xl font-semibold text-gray-900 dark:text-white mb-2">Blog Preview Card</h3>
        <p class="text-gray-700 dark:text-gray-300 mb-4">A component that previews a blog post with elegant layout and semantic HTML.</p>
        <a href="https://github.com/scannapieco/Blog-Preview-Card" target="_blank" class="inline-flex items-center justify-center w-12 h-12 bg-black rounded-full hover:bg-gray-800 transition" aria-label="View on GitHub">
          <Icon icon="mdi:github" class="w-7 h-7 text-white" />
        </a>
      </div>
  
      <div class="bg-gray-100 dark:bg-gray-800 rounded-2xl p-6 shadow-md hover:shadow-lg transition">
        <h3 class="text-2xl font-semibold text-gray-900 dark:text-white mb-2">Contact Form</h3>
        <p class="text-gray-700 dark:text-gray-300 mb-4">A styled contact form made with HTML and CSS focused on accessibility and design.</p>
        <a href="https://github.com/scannapieco/Contact-form" target="_blank" class="inline-flex items-center justify-center w-12 h-12 bg-black rounded-full hover:bg-gray-800 transition" aria-label="View on GitHub">
          <Icon icon="mdi:github" class="w-7 h-7 text-white" />
        </a>
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
        { icon: 'logos:git-icon', label: 'Git' },
        { icon: 'logos:flutter', label: 'Flutter' }
      ] as tech, i}
        {#if tech && tech.icon && tech.label}
          <div
            class="flex flex-col items-center transition-transform duration-300 transform hover:scale-110"
            in:fly={{ y: 20, duration: 500, delay: i * 100 }}
          >
            <Icon icon={tech.icon} class="w-12 h-12" aria-label={tech.label} />
            <span class="mt-2 text-sm text-black">{tech.label}</span>
          </div>
        {/if}
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