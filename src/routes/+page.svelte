<script lang="ts">
    import { onMount } from 'svelte';
    
    let showModsBackground = false;
    
    function scrollToProjects() {
        document.getElementById('projects')?.scrollIntoView({ behavior: 'smooth' });
    }
    
    onMount(() => {
        const observer = new IntersectionObserver(
            (entries) => {
                entries.forEach((entry) => {
                    if (entry.target.id === 'projects') {
                        showModsBackground = entry.isIntersecting;
                    }
                });
            },
            { threshold: 0.1 }
        );
        
        const projectsSection = document.getElementById('projects');
        if (projectsSection) {
            observer.observe(projectsSection);
        }
        
        // Custom Cursor logic
        if (typeof window !== 'undefined') {
            let cursorDot: HTMLElement | null;
            
            const initCursor = () => {
                cursorDot = document.querySelector('.cursor-dot');
                
                document.addEventListener('mousemove', (e) => {
                    if (cursorDot) {
                        cursorDot.style.left = e.clientX + 'px';
                        cursorDot.style.top = e.clientY + 'px';
                    }
                });
                
                document.addEventListener('mousedown', () => {
                    if (cursorDot) {
                        cursorDot.style.transform = 'translate(-50%, -50%) scale(0.8)';
                    }
                });
                
                document.addEventListener('mouseup', () => {
                    if (cursorDot) {
                        cursorDot.style.transform = 'translate(-50%, -50%) scale(1)';
                    }
                });
            };
            
            if (document.readyState === 'loading') {
                document.addEventListener('DOMContentLoaded', initCursor);
            } else {
                initCursor();
            }
        }

        return () => observer.disconnect();
    });
</script>

<svelte:head>
    <title>Aes Efficio</title> 
    <meta name="description" content="Aes Efficio Software">
    <meta name="keywords" content="AesEfficio, Efficio, Software">
    <meta name="author" content="Alexander Akira Weimer">
    <meta name="copyright" content="Alexander Akira Weimer">
    <meta property="og:site_name" content="Aes Efficio">
    <meta property="og:image" content="/img/wordmark.png"> 
    <meta property="fb:admins" content="268094773018996">
</svelte:head>

<main class={`justify-between items-center l-0 drop-shadow-xl transition-all duration-1000 ease-in-out${showModsBackground ? ' bg-gradient-to-br from-purple-900/40 via-fuchsia-900/30 to-pink-900/40' : ''}`}>
    <div class="flex flex-col h-[100vh] pt-2 md:pt-4 w-full px-2">
        <h1 class="transform scale-0">Aes Efficio Website</h1> <!-- SEO -->
        <span class="pr-1 pt-[30vh] mx-auto w-full text-center justify-center flex items-center md:text-center font-bold font-mastery text-fuchsia-50">
            <!-- Logo SVGs here -->
            <h2 class="text-[2.5rem] leading-none md:text-6xl inline mx-7 text-center ">aes<br>efficio</h2>
            <!-- Logo SVGs here -->
        </span>
        <span class="w-full pt-[10vh] text-center justify-center flex items-center md:text-center font-bold font-mastery text-fuchsia-50 pb-4 md:pb-8">
            <a class="mr-8 relative group" data-text="@aesefficio" href="https://github.com/aesefficio" target="_blank" rel="noopener noreferrer">
                <svg width="32px" height="32px" class="linkicon inline cursor-pointer" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 496 512">
                    <path d="M165.9 397.4c0 2-2.3 3.6-5.2 3.6-3.3 .3-5.6-1.3-5.6-3.6 0-2 2.3-3.6 5.2-3.6 3-.3 5.6 1.3 5.6 3.6zm-31.1-4.5c-.7 2 1.3 4.3 4.3 4.9 2.6 1 5.6 0 6.2-2s-1.3-4.3-4.3-5.2c-2.6-.7-5.5 .3-6.2 2.3zm44.2-1.7c-2.9 .7-4.9 2.6-4.6 4.9 .3 2 2.9 3.3 5.9 2.6 2.9-.7 4.9-2.6 4.6-4.6-.3-1.9-3-3.2-5.9-2.9zM244.8 8C106.1 8 0 113.3 0 252c0 110.9 69.8 205.8 169.5 239.2 12.8 2.3 17.3-5.6 17.3-12.1 0-6.2-.3-40.4-.3-61.4 0 0-70 15-84.7-29.8 0 0-11.4-29.1-27.8-36.6 0 0-22.9-15.7 1.6-15.4 0 0 24.9 2 38.6 25.8 21.9 38.6 58.6 27.5 72.9 20.9 2.3-16 8.8-27.1 16-33.7-55.9-6.2-112.3-14.3-112.3-110.5 0-27.5 7.6-41.3 23.6-58.9-2.6-6.5-11.1-33.3 2.6-67.9 20.9-6.5 69 27 69 27 20-5.6 41.5-8.5 62.8-8.5s42.8 2.9 62.8 8.5c0 0 48.1-33.6 69-27 13.7 34.7 5.2 61.4 2.6 67.9 16 17.7 25.8 31.5 25.8 58.9 0 96.5-58.9 104.2-114.8 110.5 9.2 7.9 17 22.9 17 46.4 0 33.7-.3 75.4-.3 83.6 0 6.5 4.6 14.4 17.3 12.1C428.2 457.8 496 362.9 496 252 496 113.3 383.5 8 244.8 8zM97.2 352.9c-1.3 1-1 3.3 .7 5.2 1.6 1.6 3.9 2.3 5.2 1 1.3-1 1-3.3-.7-5.2-1.6-1.6-3.9-2.3-5.2-1zm-10.8-8.1c-.7 1.3 .3 2.9 2.3 3.9 1.6 1 3.6 .7 4.3-.7 .7-1.3-.3-2.9-2.3-3.9-2-.6-3.6-.3-4.3 .7zm32.4 35.6c-1.6 1.3-1 4.3 1.3 6.2 2.3 2.3 5.2 2.6 6.5 1 1.3-1.3 .7-4.3-1.3-6.2-2.2-2.3-5.2-2.6-6.5-1zm-11.4-14.7c-1.6 1-1.6 3.6 0 5.9 1.6 2.3 4.3 3.3 5.6 2.3 1.6-1.3 1.6-3.9 0-6.2-1.4-2.3-4-3.3-5.6-2z"/>
                </svg>
                <svg class="absolute -top-1 -right-1 w-3 h-3 text-fuchsia-200 opacity-0 group-hover:opacity-100 transition-opacity duration-200" fill="currentColor" viewBox="0 0 12 12">
                    <path d="M3.5 3L8.5 3L8.5 8M8.5 3L3.5 8"/>
                </svg>
            </a>
            <a class="relative group" href="https://modrinth.com/organization/aes" target="_blank" rel="noopener noreferrer">
                <svg width="32px" height="32px" class="linkicon inline cursor-pointer" xmlns="http://www.w3.org/2000/svg" x="0px" y="0px" viewBox="0 0 512 514">
                    <path fill-rule="evenodd" clip-rule="evenodd" d="M503.16 323.56C514.55 281.47 515.32 235.91 503.2 190.76C466.57 54.2299 326.04 -26.8001 189.33 9.77991C83.8101 38.0199 11.3899 128.07 0.689941 230.47H43.99C54.29 147.33 113.74 74.7298 199.75 51.7098C306.05 23.2598 415.13 80.6699 453.17 181.38L411.03 192.65C391.64 145.8 352.57 111.45 306.3 96.8198L298.56 140.66C335.09 154.13 364.72 184.5 375.56 224.91C391.36 283.8 361.94 344.14 308.56 369.17L320.09 412.16C390.25 383.21 432.4 310.3 422.43 235.14L464.41 223.91C468.91 252.62 467.35 281.16 460.55 308.07L503.16 323.56Z" fill="currentColor"/>
                    <path d="M321.99 504.22C185.27 540.8 44.7501 459.77 8.11011 323.24C3.84011 307.31 1.17 291.33 0 275.46H43.27C44.36 287.37 46.4699 299.35 49.6799 311.29C53.0399 323.8 57.45 335.75 62.79 347.07L101.38 323.92C98.1299 316.42 95.39 308.6 93.21 300.47C69.17 210.87 122.41 118.77 212.13 94.7601C229.13 90.2101 246.23 88.4401 262.93 89.1501L255.19 133C244.73 133.05 234.11 134.42 223.53 137.25C157.31 154.98 118.01 222.95 135.75 289.09C136.85 293.16 138.13 297.13 139.59 300.99L188.94 271.38L174.07 231.95L220.67 184.08L279.57 171.39L296.62 192.38L269.47 219.88L245.79 227.33L228.87 244.72L237.16 267.79C237.16 267.79 253.95 285.63 253.98 285.64L277.7 279.33L294.58 260.79L331.44 249.12L342.42 273.82L304.39 320.45L240.66 340.63L212.08 308.81L162.26 338.7C187.8 367.78 226.2 383.93 266.01 380.56L277.54 423.55C218.13 431.41 160.1 406.82 124.05 361.64L85.6399 384.68C136.25 451.17 223.84 484.11 309.61 461.16C371.35 444.64 419.4 402.56 445.42 349.38L488.06 364.88C457.17 431.16 398.22 483.82 321.99 504.22Z" fill="currentColor"/>
                </svg>
                <svg class="absolute -top-1 -right-1 w-3 h-3 text-fuchsia-200 opacity-0 group-hover:opacity-100 transition-opacity duration-200" stroke="currentColor" stroke-width="1.5" fill="none" viewBox="0 0 12 12">
                    <path d="M3.5 3L8.5 3L8.5 8M8.5 3L3.5 8"/>
                </svg>
            </a>
            <a class="ml-8 relative group" data-text=".gg/kw7hx73wVA" href="https://discord.gg/kw7hx73wVA" target="_blank" rel="noopener noreferrer">
                <svg width="36px" height="36px" class="linkicon inline cursor-pointer" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 640 512">
                    <path d="M524.5 69.8a1.5 1.5 0 0 0 -.8-.7A485.1 485.1 0 0 0 404.1 32a1.8 1.8 0 0 0 -1.9 .9 337.5 337.5 0 0 0 -14.9 30.6 447.8 447.8 0 0 0 -134.4 0 309.5 309.5 0 0 0 -15.1-30.6 1.9 1.9 0 0 0 -1.9-.9A483.7 483.7 0 0 0 116.1 69.1a1.7 1.7 0 0 0 -.8 .7C39.1 183.7 18.2 294.7 28.4 404.4a2 2 0 0 0 .8 1.4A487.7 487.7 0 0 0 176 479.9a1.9 1.9 0 0 0 2.1-.7A348.2 348.2 0 0 0 208.1 430.4a1.9 1.9 0 0 0 -1-2.6 321.2 321.2 0 0 1 -45.9-21.9 1.9 1.9 0 0 1 -.2-3.1c3.1-2.3 6.2-4.7 9.1-7.1a1.8 1.8 0 0 1 1.9-.3c96.2 43.9 200.4 43.9 295.5 0a1.8 1.8 0 0 1 1.9 .2c2.9 2.4 6 4.9 9.1 7.2a1.9 1.9 0 0 1 -.2 3.1 301.4 301.4 0 0 1 -45.9 21.8 1.9 1.9 0 0 0 -1 2.6 391.1 391.1 0 0 0 30 48.8 1.9 1.9 0 0 0 2.1 .7A486 486 0 0 0 610.7 405.7a1.9 1.9 0 0 0 .8-1.4C623.7 277.6 590.9 167.5 524.5 69.8zM222.5 337.6c-29 0-52.8-26.6-52.8-59.2S193.1 219.1 222.5 219.1c29.7 0 53.3 26.8 52.8 59.2C275.3 311 251.9 337.6 222.5 337.6zm195.4 0c-29 0-52.8-26.6-52.8-59.2S388.4 219.1 417.9 219.1c29.7 0 53.3 26.8 52.8 59.2C470.7 311 447.5 337.6 417.9 337.6z"/>
                </svg>
                <svg class="absolute -top-1 -right-1 w-3 h-3 text-fuchsia-200 opacity-0 group-hover:opacity-100 transition-opacity duration-200" stroke="currentColor" stroke-width="1.5" fill="none" viewBox="0 0 12 12">
                    <path d="M3.5 3L8.5 3L8.5 8M8.5 3L3.5 8"/>
                </svg>
            </a>
        </span>
        
        <!-- Our Projects Section -->
        <div class="w-full pt-[8vh] text-center justify-center flex flex-col items-center">
            <button on:click={scrollToProjects} class="group cursor-pointer text-center">
                <p class="text-2xl md:text-3xl font-bold font-mastery text-fuchsia-50 mb-4">our projects</p>
                <svg class="w-8 h-8 mx-auto text-fuchsia-50 animate-bounce" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 14l-7 7m0 0l-7-7m7 7V3"></path>
                </svg>
            </button>
        </div>
    </div>
    
    <!-- Projects Section -->
    <section id="projects" class="min-h-screen w-full bg-gradient-to-b from-transparent to-black/20 py-16 px-4">
        <div class="max-w-4xl mx-auto">
            <h2 class="text-4xl md:text-5xl font-bold font-mastery text-fuchsia-50 text-center mb-16">Our Minecraft Mods</h2>
            
            <div class="space-y-8">
                <!-- Mod Card 1 -->
                <div class="bg-white/10 backdrop-blur-sm rounded-lg p-6 hover:bg-white/15 transition-colors duration-300">
                    <div class="flex flex-col md:flex-row items-center md:items-start gap-6">
                        <div class="w-24 h-24 rounded-lg flex items-center justify-center flex-shrink-0 overflow-hidden">
                            <img src="https://media.forgecdn.net/avatars/1068/436/638602929407669140.png" alt="Create Interiors Logo" class="w-full h-full object-cover">
                        </div>
                        <div class="flex-1 text-center md:text-left">
                            <h3 class="text-2xl font-bold text-fuchsia-50 mb-2">Create Interiors</h3>
                            <p class="text-gray-200 mb-4">A complement to the Create mod that adds new furniture. Enhance your builds with decorative and functional interior elements perfect for any Create-powered contraption.</p>
                            <div class="flex flex-wrap justify-center md:justify-start gap-2 mb-4">
                                <span class="px-3 py-1 bg-purple-600/50 text-white text-sm rounded-full">Fabric</span>
                                <span class="px-3 py-1 bg-orange-600/50 text-white text-sm rounded-full">Forge</span>
                                <span class="px-3 py-1 bg-green-600/50 text-white text-sm rounded-full">1.18.2-1.21.1</span>
                                <span class="px-3 py-1 bg-blue-600/50 text-white text-sm rounded-full">8.93M downloads</span>
                            </div>
                            <div class="flex flex-wrap justify-center md:justify-start gap-2">
                                <a href="https://modrinth.com/mod/interiors" target="_blank" rel="noopener noreferrer" class="inline-flex items-center px-4 py-2 bg-fuchsia-600 hover:bg-fuchsia-700 text-white rounded-lg transition-colors duration-200">
                                    Download on Modrinth
                                </a>
                                <a href="https://curseforge.com/minecraft/mc-mods/interiors" target="_blank" rel="noopener noreferrer" class="inline-flex items-center px-4 py-2 bg-orange-600 hover:bg-orange-700 text-white rounded-lg transition-colors duration-200">
                                    Download on CurseForge
                                </a>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Mod Card 2 -->
                <div class="bg-white/10 backdrop-blur-sm rounded-lg p-6 hover:bg-white/15 transition-colors duration-300">
                    <div class="flex flex-col md:flex-row items-center md:items-start gap-6">
                        <div class="w-24 h-24 rounded-lg flex items-center justify-center flex-shrink-0 overflow-hidden">
                            <img src="https://media.forgecdn.net/avatars/1068/437/638602929669872740.png" alt="Bells & Whistles Logo" class="w-full h-full object-cover">
                        </div>
                        <div class="flex-1 text-center md:text-left">
                            <h3 class="text-2xl font-bold text-fuchsia-50 mb-2">Bells & Whistles</h3>
                            <p class="text-gray-200 mb-4">Focused on the player experience, adding decorative and utility blocks. Perfect for builders who want to add those extra details that make all the difference.</p>
                            <div class="flex flex-wrap justify-center md:justify-start gap-2 mb-4">
                                <span class="px-3 py-1 bg-purple-600/50 text-white text-sm rounded-full">Fabric</span>
                                <span class="px-3 py-1 bg-orange-600/50 text-white text-sm rounded-full">Forge</span>
                                <span class="px-3 py-1 bg-green-600/50 text-white text-sm rounded-full">1.18.2-1.21.1</span>
                                <span class="px-3 py-1 bg-blue-600/50 text-white text-sm rounded-full">9.06M downloads</span>
                            </div>
                            <div class="flex flex-wrap justify-center md:justify-start gap-2">
                                <a href="https://modrinth.com/mod/bellsandwhistles" target="_blank" rel="noopener noreferrer" class="inline-flex items-center px-4 py-2 bg-fuchsia-600 hover:bg-fuchsia-700 text-white rounded-lg transition-colors duration-200">
                                    Download on Modrinth
                                </a>
                                <a href="https://curseforge.com/minecraft/mc-mods/bellsandwhistles" target="_blank" rel="noopener noreferrer" class="inline-flex items-center px-4 py-2 bg-orange-600 hover:bg-orange-700 text-white rounded-lg transition-colors duration-200">
                                    Download on CurseForge
                                </a>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Mod Card 3 -->
                <div class="bg-white/10 backdrop-blur-sm rounded-lg p-6 hover:bg-white/15 transition-colors duration-300">
                    <div class="flex flex-col md:flex-row items-center md:items-start gap-6">
                        <div class="w-24 h-24 rounded-lg flex items-center justify-center flex-shrink-0 overflow-hidden">
                            <img src="https://media.forgecdn.net/avatars/1068/434/638602928990115218.png" alt="Dynamic Village Logo" class="w-full h-full object-cover">
                        </div>
                        <div class="flex-1 text-center md:text-left">
                            <h3 class="text-2xl font-bold text-fuchsia-50 mb-2">Dynamic Village</h3>
                            <p class="text-gray-200 mb-4">Adds a whole host of village professions & structures. Breathe new life into villages with diverse NPCs and buildings that make every village unique and engaging.</p>
                            <div class="flex flex-wrap justify-center md:justify-start gap-2 mb-4">
                                <span class="px-3 py-1 bg-orange-600/50 text-white text-sm rounded-full">Forge</span>
                                <span class="px-3 py-1 bg-green-600/50 text-white text-sm rounded-full">1.19.2-1.20.1</span>
                                <span class="px-3 py-1 bg-blue-600/50 text-white text-sm rounded-full">3.73M downloads</span>
                            </div>
                            <div class="flex flex-wrap justify-center md:justify-start gap-2">
                                <a href="https://modrinth.com/mod/dynamic-village" target="_blank" rel="noopener noreferrer" class="inline-flex items-center px-4 py-2 bg-fuchsia-600 hover:bg-fuchsia-700 text-white rounded-lg transition-colors duration-200">
                                    Download on Modrinth
                                </a>
                                <a href="https://curseforge.com/minecraft/mc-mods/dynamic-village" target="_blank" rel="noopener noreferrer" class="inline-flex items-center px-4 py-2 bg-orange-600 hover:bg-orange-700 text-white rounded-lg transition-colors duration-200">
                                    Download on CurseForge
                                </a>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <div class="fixed inset-x-0 bottom-3 flex justify-center font-bold font-varela text-white text-sm hover:underline decoration-dotted ">
        <a href="./privacy">privacy policy</a>
    </div>
    
    <!-- Custom Cursor -->
    <div class="cursor-dot"></div>
</main>

<style>
    /* Custom Cursor */
    :global(body) {
        cursor: none;
    }
</style>