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
            let cursorFollower: HTMLElement | null;
            let isMouseInsideViewport = true;
            
            const updateCursorPosition = (e: MouseEvent) => {
                if (cursorFollower) {
                    cursorFollower.style.left = e.clientX + 'px';
                    cursorFollower.style.top = e.clientY + 'px';
                    
                    if (!isMouseInsideViewport) {
                        cursorFollower.style.opacity = '0';
                    } else {
                        cursorFollower.style.opacity = '1';
                    }
                }
            };
            
            const initCursor = () => {
                cursorFollower = document.querySelector('.cursor-dot');
                
                document.addEventListener('mousemove', updateCursorPosition);
                
                document.addEventListener('mouseenter', () => {
                    isMouseInsideViewport = true;
                    if (cursorFollower) {
                        cursorFollower.style.opacity = '1';
                    }
                });
                
                document.addEventListener('mouseleave', () => {
                    isMouseInsideViewport = false;
                    if (cursorFollower) {
                        cursorFollower.style.opacity = '0';
                    }
                });
                
                document.addEventListener('mousedown', () => {
                    if (cursorFollower) {
                        cursorFollower.style.transform = 'translate(-50%, -50%) scale(0.8)';
                    }
                });
                
                document.addEventListener('mouseup', () => {
                    if (cursorFollower) {
                        cursorFollower.style.transform = 'translate(-50%, -50%) scale(1)';
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
            <svg class="mt-4 h-8 md:h-12" xmlns="http://www.w3.org/2000/svg" xml:space="preserve" style="shape-rendering:geometricPrecision; text-rendering:geometricPrecision; image-rendering:optimizeQuality; fill-rule:evenodd; clip-rule:evenodd" viewBox="0 0 278 160" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.0">
                <path class="white" fill="white" stroke="white" d="M211.643 54.7138l-14.3145 -13.4661c-16.957,-16.3591 -29.6255,-27.1822 -38.054,-32.5686 -8.429,-5.3364 -17.0076,-8.0297 -25.6858,-8.0297 -12.3688,0 -23.2913,4.1895 -32.7677,12.5184 -9.5259,8.3295 -14.2638,17.8053 -14.2638,28.5287 0,7.83 2.2938,14.364 6.9322,19.7504 4.6383,5.3364 10.2746,8.0297 16.9075,8.0297 8.4791,0 16.6083,-4.5388 24.3887,-13.6158 -2.2443,0.3988 -3.9897,0.5985 -5.2368,0.5985 -7.9796,0 -14.9123,-2.4441 -20.7477,-7.3817 -5.8353,-4.8875 -8.7777,-10.7729 -8.7777,-17.6056 0,-4.289 1.5457,-7.9301 4.6878,-11.0221 3.0926,-3.0425 6.7331,-4.5889 10.9226,-4.5889 11.1222,0 30.1245,13.8656 57.0068,41.6456l11.8203 12.1196c-9.1271,6.2341 -21.745,11.6707 -37.7548,16.3591 -16.0599,4.6383 -30.1245,6.9823 -42.2942,6.9823 -21.0469,0 -38.6525,-6.4339 -52.7672,-19.3016 -14.1148,-12.8176 -21.1966,-28.8274 -21.1966,-48.0293 0,-4.3892 0.5485,-8.5286 1.5958,-12.4188 -20.6481,3.6905 -30.9722,12.7681 -30.9722,27.1815 0,18.4038 9.5259,34.3641 28.5782,47.8303 19.0524,13.5156 41.496,20.2487 67.4305,20.2487 14.6136,0 34.5631,-4.9871 59.8001,-14.9124l-10.5237 10.2246c-10.7229,10.4236 -21.9447,19.1519 -33.6154,26.1842 -11.7207,7.0323 -20.8979,10.5232 -27.631,10.5232 -5.486,0 -10.0743,-1.5958 -13.8149,-4.7379 -3.7406,-3.1922 -5.6362,-7.0324 -5.6362,-11.6207 0,-1.0974 0.1496,-2.5436 0.4489,-4.3891 -13.4662,5.0371 -20.1993,11.5711 -20.1993,19.5507 0,5.5861 2.7934,10.324 8.429,14.2143 5.5862,3.8902 12.4188,5.8353 20.4985,5.8353 18.6035,0 45.9346,-17.6556 81.9941,-52.9169l10.2245 -10.0749c7.5307,-7.381 15.7105,-14.2143 24.5878,-20.4484 16.5588,16.9576 33.1671,25.4361 49.925,25.4361 10.0248,0 18.4533,-2.6932 25.1864,-8.1298 6.7831,-5.3864 10.1744,-12.0695 10.1744,-19.9495 0,-7.7804 -3.2417,-14.3144 -9.7256,-19.5012 -6.4833,-5.2368 -14.563,-7.8305 -24.2886,-7.8305 -9.8257,0 -20.2493,2.943 -31.2714,8.7783zm7.4311 6.8828c8.6782,-3.2423 15.8602,-4.8381 21.4958,-4.8381 6.9328,0 12.1196,1.0474 15.5609,3.1421 3.4414,2.0948 5.1874,5.2369 5.1874,9.4263 0,2.9424 -1.0474,5.1373 -3.0926,6.5835 -2.0447,1.4462 -5.1367,2.1943 -9.3262,2.1943 -8.9775,0 -18.9027,-5.486 -29.8253,-16.5081z"/>
            </svg>
            <h2 class="text-[2.5rem] leading-none md:text-6xl inline mx-7 text-center ">aes<br>efficio</h2>
            <svg class="scale-x-[-1] mt-4 h-8 md:h-12" xmlns="http://www.w3.org/2000/svg" xml:space="preserve" style="shape-rendering:geometricPrecision; text-rendering:geometricPrecision; image-rendering:optimizeQuality; fill-rule:evenodd; clip-rule:evenodd" viewBox="0 0 278 160" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.0">
                <path class="white" fill="white" stroke="white" d="M211.643 54.7138l-14.3145 -13.4661c-16.957,-16.3591 -29.6255,-27.1822 -38.054,-32.5686 -8.429,-5.3364 -17.0076,-8.0297 -25.6858,-8.0297 -12.3688,0 -23.2913,4.1895 -32.7677,12.5184 -9.5259,8.3295 -14.2638,17.8053 -14.2638,28.5287 0,7.83 2.2938,14.364 6.9322,19.7504 4.6383,5.3364 10.2746,8.0297 16.9075,8.0297 8.4791,0 16.6083,-4.5388 24.3887,-13.6158 -2.2443,0.3988 -3.9897,0.5985 -5.2368,0.5985 -7.9796,0 -14.9123,-2.4441 -20.7477,-7.3817 -5.8353,-4.8875 -8.7777,-10.7729 -8.7777,-17.6056 0,-4.289 1.5457,-7.9301 4.6878,-11.0221 3.0926,-3.0425 6.7331,-4.5889 10.9226,-4.5889 11.1222,0 30.1245,13.8656 57.0068,41.6456l11.8203 12.1196c-9.1271,6.2341 -21.745,11.6707 -37.7548,16.3591 -16.0599,4.6383 -30.1245,6.9823 -42.2942,6.9823 -21.0469,0 -38.6525,-6.4339 -52.7672,-19.3016 -14.1148,-12.8176 -21.1966,-28.8274 -21.1966,-48.0293 0,-4.3892 0.5485,-8.5286 1.5958,-12.4188 -20.6481,3.6905 -30.9722,12.7681 -30.9722,27.1815 0,18.4038 9.5259,34.3641 28.5782,47.8303 19.0524,13.5156 41.496,20.2487 67.4305,20.2487 14.6136,0 34.5631,-4.9871 59.8001,-14.9124l-10.5237 10.2246c-10.7229,10.4236 -21.9447,19.1519 -33.6154,26.1842 -11.7207,7.0323 -20.8979,10.5232 -27.631,10.5232 -5.486,0 -10.0743,-1.5958 -13.8149,-4.7379 -3.7406,-3.1922 -5.6362,-7.0324 -5.6362,-11.6207 0,-1.0974 0.1496,-2.5436 0.4489,-4.3891 -13.4662,5.0371 -20.1993,11.5711 -20.1993,19.5507 0,5.5861 2.7934,10.324 8.429,14.2143 5.5862,3.8902 12.4188,5.8353 20.4985,5.8353 18.6035,0 45.9346,-17.6556 81.9941,-52.9169l10.2245 -10.0749c7.5307,-7.381 15.7105,-14.2143 24.5878,-20.4484 16.5588,16.9576 33.1671,25.4361 49.925,25.4361 10.0248,0 18.4533,-2.6932 25.1864,-8.1298 6.7831,-5.3864 10.1744,-12.0695 10.1744,-19.9495 0,-7.7804 -3.2417,-14.3144 -9.7256,-19.5012 -6.4833,-5.2368 -14.563,-7.8305 -24.2886,-7.8305 -9.8257,0 -20.2493,2.943 -31.2714,8.7783zm7.4311 6.8828c8.6782,-3.2423 15.8602,-4.8381 21.4958,-4.8381 6.9328,0 12.1196,1.0474 15.5609,3.1421 3.4414,2.0948 5.1874,5.2369 5.1874,9.4263 0,2.9424 -1.0474,5.1373 -3.0926,6.5835 -2.0447,1.4462 -5.1367,2.1943 -9.3262,2.1943 -8.9775,0 -18.9027,-5.486 -29.8253,-16.5081z"/>
</svg>
            </span>
        <span class="w-full pt-[10vh] text-center justify-center flex items-center md:text-center font-bold font-mastery text-fuchsia-50 pb-4 md:pb-8">
            <a class="mr-8 relative group" data-text="@aesefficio" href="https://github.com/aesefficio" target="_blank" rel="noopener noreferrer">
                <svg width="32px" height="32px" class="linkicon inline cursor-pointer" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 496 512">
                    <path d="M165.9 397.4c0 2-2.3 3.6-5.2 3.6-3.3 .3-5.6-1.3-5.6-3.6 0-2 2.3-3.6 5.2-3.6 3-.3 5.6 1.3 5.6 3.6zm-31.1-4.5c-.7 2 1.3 4.3 4.3 4.9 2.6 1 5.6 0 6.2-2s-1.3-4.3-4.3-5.2c-2.6-.7-5.5 .3-6.2 2.3zm44.2-1.7c-2.9 .7-4.9 2.6-4.6 4.9 .3 2 2.9 3.3 5.9 2.6 2.9-.7 4.9-2.6 4.6-4.6-.3-1.9-3-3.2-5.9-2.9zM244.8 8C106.1 8 0 113.3 0 252c0 110.9 69.8 205.8 169.5 239.2 12.8 2.3 17.3-5.6 17.3-12.1 0-6.2-.3-40.4-.3-61.4 0 0-70 15-84.7-29.8 0 0-11.4-29.1-27.8-36.6 0 0-22.9-15.7 1.6-15.4 0 0 24.9 2 38.6 25.8 21.9 38.6 58.6 27.5 72.9 20.9 2.3-16 8.8-27.1 16-33.7-55.9-6.2-112.3-14.3-112.3-110.5 0-27.5 7.6-41.3 23.6-58.9-2.6-6.5-11.1-33.3 2.6-67.9 20.9-6.5 69 27 69 27 20-5.6 41.5-8.5 62.8-8.5s42.8 2.9 62.8 8.5c0 0 48.1-33.6 69-27 13.7 34.7 5.2 61.4 2.6 67.9 16 17.7 25.8 31.5 25.8 58.9 0 96.5-58.9 104.2-114.8 110.5 9.2 7.9 17 22.9 17 46.4 0 33.7-.3 75.4-.3 83.6 0 6.5 4.6 14.4 17.3 12.1C428.2 457.8 496 362.9 496 252 496 113.3 383.5 8 244.8 8zM97.2 352.9c-1.3 1-1 3.3 .7 5.2 1.6 1.6 3.9 2.3 5.2 1 1.3-1 1-3.3-.7-5.2-1.6-1.6-3.9-2.3-5.2-1zm-10.8-8.1c-.7 1.3 .3 2.9 2.3 3.9 1.6 1 3.6 .7 4.3-.7 .7-1.3-.3-2.9-2.3-3.9-2-.6-3.6-.3-4.3 .7zm32.4 35.6c-1.6 1.3-1 4.3 1.3 6.2 2.3 2.3 5.2 2.6 6.5 1 1.3-1.3 .7-4.3-1.3-6.2-2.2-2.3-5.2-2.6-6.5-1zm-11.4-14.7c-1.6 1-1.6 3.6 0 5.9 1.6 2.3 4.3 3.3 5.6 2.3 1.6-1.3 1.6-3.9 0-6.2-1.4-2.3-4-3.3-5.6-2z"/>
                </svg>
                <svg class="absolute -top-1 -right-1 w-3 h-3 text-fuchsia-100 transform group-hover:scale-[135%] group-hover:translate-x-[2px] group-hover:-translate-y-[2px] transition-all" fill="currentColor" viewBox="0 0 12 12">
                    <path d="M3.5 3L8.5 3L8.5 8M8.5 3L3.5 8"/>
                </svg>
            </a>
            <a class="relative group" href="https://modrinth.com/organization/aes" target="_blank" rel="noopener noreferrer">
                <svg width="32px" height="32px" class="linkicon inline cursor-pointer" xmlns="http://www.w3.org/2000/svg" x="0px" y="0px" viewBox="0 0 512 514">
                    <path fill-rule="evenodd" clip-rule="evenodd" d="M503.16 323.56C514.55 281.47 515.32 235.91 503.2 190.76C466.57 54.2299 326.04 -26.8001 189.33 9.77991C83.8101 38.0199 11.3899 128.07 0.689941 230.47H43.99C54.29 147.33 113.74 74.7298 199.75 51.7098C306.05 23.2598 415.13 80.6699 453.17 181.38L411.03 192.65C391.64 145.8 352.57 111.45 306.3 96.8198L298.56 140.66C335.09 154.13 364.72 184.5 375.56 224.91C391.36 283.8 361.94 344.14 308.56 369.17L320.09 412.16C390.25 383.21 432.4 310.3 422.43 235.14L464.41 223.91C468.91 252.62 467.35 281.16 460.55 308.07L503.16 323.56Z" fill="currentColor"/>
                    <path d="M321.99 504.22C185.27 540.8 44.7501 459.77 8.11011 323.24C3.84011 307.31 1.17 291.33 0 275.46H43.27C44.36 287.37 46.4699 299.35 49.6799 311.29C53.0399 323.8 57.45 335.75 62.79 347.07L101.38 323.92C98.1299 316.42 95.39 308.6 93.21 300.47C69.17 210.87 122.41 118.77 212.13 94.7601C229.13 90.2101 246.23 88.4401 262.93 89.1501L255.19 133C244.73 133.05 234.11 134.42 223.53 137.25C157.31 154.98 118.01 222.95 135.75 289.09C136.85 293.16 138.13 297.13 139.59 300.99L188.94 271.38L174.07 231.95L220.67 184.08L279.57 171.39L296.62 192.38L269.47 219.88L245.79 227.33L228.87 244.72L237.16 267.79C237.16 267.79 253.95 285.63 253.98 285.64L277.7 279.33L294.58 260.79L331.44 249.12L342.42 273.82L304.39 320.45L240.66 340.63L212.08 308.81L162.26 338.7C187.8 367.78 226.2 383.93 266.01 380.56L277.54 423.55C218.13 431.41 160.1 406.82 124.05 361.64L85.6399 384.68C136.25 451.17 223.84 484.11 309.61 461.16C371.35 444.64 419.4 402.56 445.42 349.38L488.06 364.88C457.17 431.16 398.22 483.82 321.99 504.22Z" fill="currentColor"/>
                </svg>
                <svg class="absolute -top-1 -right-1 w-3 h-3 text-fuchsia-100 transform group-hover:scale-[135%] group-hover:translate-x-[2px] group-hover:-translate-y-[2px] transition-all" fill="currentColor" viewBox="0 0 12 12">
                    <path d="M3.5 3L8.5 3L8.5 8M8.5 3L3.5 8"/>
                </svg>
            </a>
            <a class="ml-8 relative group" data-text=".gg/kw7hx73wVA" href="https://discord.gg/kw7hx73wVA" target="_blank" rel="noopener noreferrer">
                <svg width="36px" height="36px" class="linkicon inline cursor-pointer" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 640 512">
                    <path d="M524.5 69.8a1.5 1.5 0 0 0 -.8-.7A485.1 485.1 0 0 0 404.1 32a1.8 1.8 0 0 0 -1.9 .9 337.5 337.5 0 0 0 -14.9 30.6 447.8 447.8 0 0 0 -134.4 0 309.5 309.5 0 0 0 -15.1-30.6 1.9 1.9 0 0 0 -1.9-.9A483.7 483.7 0 0 0 116.1 69.1a1.7 1.7 0 0 0 -.8 .7C39.1 183.7 18.2 294.7 28.4 404.4a2 2 0 0 0 .8 1.4A487.7 487.7 0 0 0 176 479.9a1.9 1.9 0 0 0 2.1-.7A348.2 348.2 0 0 0 208.1 430.4a1.9 1.9 0 0 0 -1-2.6 321.2 321.2 0 0 1 -45.9-21.9 1.9 1.9 0 0 1 -.2-3.1c3.1-2.3 6.2-4.7 9.1-7.1a1.8 1.8 0 0 1 1.9-.3c96.2 43.9 200.4 43.9 295.5 0a1.8 1.8 0 0 1 1.9 .2c2.9 2.4 6 4.9 9.1 7.2a1.9 1.9 0 0 1 -.2 3.1 301.4 301.4 0 0 1 -45.9 21.8 1.9 1.9 0 0 0 -1 2.6 391.1 391.1 0 0 0 30 48.8 1.9 1.9 0 0 0 2.1 .7A486 486 0 0 0 610.7 405.7a1.9 1.9 0 0 0 .8-1.4C623.7 277.6 590.9 167.5 524.5 69.8zM222.5 337.6c-29 0-52.8-26.6-52.8-59.2S193.1 219.1 222.5 219.1c29.7 0 53.3 26.8 52.8 59.2C275.3 311 251.9 337.6 222.5 337.6zm195.4 0c-29 0-52.8-26.6-52.8-59.2S388.4 219.1 417.9 219.1c29.7 0 53.3 26.8 52.8 59.2C470.7 311 447.5 337.6 417.9 337.6z"/>
                </svg>
                <svg class="absolute -top-1 -right-1 w-3 h-3 text-fuchsia-100 transform group-hover:scale-[135%] group-hover:translate-x-[2px] group-hover:-translate-y-[2px] transition-all" fill="currentColor" viewBox="0 0 12 12">
                    <path d="M3.5 3L8.5 3L8.5 8M8.5 3L3.5 8"/>
                </svg>
            </a>
        </span>
        
        <!-- Our Projects Section -->
        <div class="w-full pt-[8vh] text-center justify-center flex flex-col items-center">
            <button on:click={scrollToProjects} class="group cursor-pointer text-center">
                <p class="text-2xl md:text-3xl font-bold font-mastery text-fuchsia-50 mb-4">our work</p>
                <svg class="w-8 h-8 mx-auto mt-2 text-fuchsia-50 animate-bounce" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="4.5" d="M19 14l-7 7m0 0l-7-7m7 7V3"></path>
                </svg>
            </button>
        </div>
    </div>
    
    <!-- Projects Section -->
    <section id="projects" class="min-h-screen w-full bg-gradient-to-b from-transparent to-black/20 py-16 px-4">
        <div class="max-w-4xl mx-auto">            
            <div class="space-y-8">
                                                <!-- Mod Card 1 -->
                                <div class="bg-gray-800 notched-corners p-6 hover:bg-gray-700 transition-colors duration-300">
                                    <div class="flex flex-col md:flex-row items-center md:items-start gap-6">
                                        <div class="w-24 h-24 flex items-center justify-center flex-shrink-0 overflow-hidden notched-corners">
                                            <img src="https://media.forgecdn.net/avatars/1068/437/638602929669872740.png" alt="Bells & Whistles Logo" class="w-full h-full object-cover">
                                        </div>
                                        <div class="flex-1 text-center md:text-left">
                                            <h3 class="text-3xl font-bold font-mastery text-fuchsia-50 mb-2">Bells & Whistles</h3>
                                            <p class="text-gray-200 mb-4">Add greater depth and utility to your builds with new blocks to expand your creative horizons.</p>
                                            <div class="flex flex-wrap justify-center md:justify-start gap-3 mb-4">
                                                <span class="px-3 py-1 notched-corners mod-tag">Fabric</span>
                                                <span class="px-3 py-1 notched-corners mod-tag">Forge</span>
                                                <span class="px-3 py-1 notched-corners mod-tag">1.18.2-1.21.1</span>
                                                <span class="px-3 py-1 notched-corners mod-tag">9.06M downloads</span>
                                            </div>
                                            <div class="flex flex-wrap justify-center md:justify-start gap-2">
                                                <a href="https://modrinth.com/mod/bellsandwhistles" target="_blank" rel="noopener noreferrer" class="button-download notched-corners">
                                                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" class="mr-2">
                                                        <g id="Interface / Download">
                                                            <path id="Vector" d="M6 21H18M12 3V17M12 17L17 12M12 17L7 12" stroke="currentColor" stroke-width="4" stroke-linecap="round" stroke-linejoin="round"/>
                                                        </g>
                                                    </svg>
                                                    modrinth
                                                </a>
                                                <a href="https://curseforge.com/minecraft/mc-mods/bellsandwhistles" target="_blank" rel="noopener noreferrer" class="button-download notched-corners">
                                                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" class="mr-2">
                                                        <g id="Interface / Download">
                                                            <path id="Vector" d="M6 21H18M12 3V17M12 17L17 12M12 17L7 12" stroke="currentColor" stroke-width="4" stroke-linecap="round" stroke-linejoin="round"/>
                                                        </g>
                                                    </svg>
                                                    curseforge
                                                </a>
                                            </div>
                                        </div>
                                    </div>
                                </div>

                                <!-- Mod Card 2 -->
                                <div class="bg-gray-800 notched-corners p-6 hover:bg-gray-700 transition-colors duration-300">
                                    <div class="flex flex-col md:flex-row items-center md:items-start gap-6">
                                        <div class="w-24 h-24 flex items-center justify-center flex-shrink-0 overflow-hidden notched-corners">
                                            <img src="https://media.forgecdn.net/avatars/1068/436/638602929407669140.png" alt="Create Interiors Logo" class="w-full h-full object-cover">
                                        </div>
                                        <div class="flex-1 text-center md:text-left">
                                            <h3 class="text-3xl font-bold font-mastery text-fuchsia-50 mb-2">Create Interiors</h3>
                                            <p class="text-gray-200 mb-4">New blocks & mechanics to improve your Create mod experience.</p>
                                            <div class="flex flex-wrap justify-center md:justify-start gap-3 mb-4">
                                                <span class="px-3 py-1 notched-corners mod-tag">Fabric</span>
                                                <span class="px-3 py-1 notched-corners mod-tag">Forge</span>
                                                <span class="px-3 py-1 notched-corners mod-tag">1.18.2-1.21.1</span>
                                                <span class="px-3 py-1 notched-corners mod-tag">8.93M downloads</span>
                                            </div>
                                            <div class="flex flex-wrap justify-center md:justify-start gap-2">
                                                <a href="https://modrinth.com/mod/interiors" target="_blank" rel="noopener noreferrer" class="button-download notched-corners">
                                                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" class="mr-2">
                                                        <g id="Interface / Download">
                                                            <path id="Vector" d="M6 21H18M12 3V17M12 17L17 12M12 17L7 12" stroke="currentColor" stroke-width="4" stroke-linecap="round" stroke-linejoin="round"/>
                                                        </g>
                                                    </svg>
                                                    modrinth
                                                </a>
                                                <a href="https://curseforge.com/minecraft/mc-mods/interiors" target="_blank" rel="noopener noreferrer" class="button-download notched-corners">
                                                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" class="mr-2">
                                                        <g id="Interface / Download">
                                                            <path id="Vector" d="M6 21H18M12 3V17M12 17L17 12M12 17L7 12" stroke="currentColor" stroke-width="4" stroke-linecap="round" stroke-linejoin="round"/>
                                                        </g>
                                                    </svg>
                                                    curseforge
                                                </a>
                                            </div>
                                        </div>
                                    </div>
                                </div>
            
                
                                <!-- Mod Card 3 -->
                                <div class="bg-gray-800 notched-corners p-6 hover:bg-gray-700 transition-colors duration-300">
                                    <div class="flex flex-col md:flex-row items-center md:items-start gap-6">
                                        <div class="w-24 h-24 flex items-center justify-center flex-shrink-0 overflow-hidden notched-corners">
                                            <img src="https://media.forgecdn.net/avatars/1068/434/638602928990115218.png" alt="Dynamic Village Logo" class="w-full h-full object-cover">
                                        </div>
                                        <div class="flex-1 text-center md:text-left">
                                            <h3 class="text-3xl font-bold font-mastery text-fuchsia-50 mb-2">Dynamic Village</h3>
                                            <p class="text-gray-200 mb-4">Breathe new life into villages with a whole host of modern professions and buildings.</p>
                                            <div class="flex flex-wrap justify-center md:justify-start gap-3 mb-4">
                                                <span class="px-3 py-1 notched-corners mod-tag">Forge</span>
                                                <span class="px-3 py-1 notched-corners mod-tag">1.19.2-1.20.1</span>
                                                <span class="px-3 py-1 notched-corners mod-tag">3.73M downloads</span>
                                            </div>
                                            <div class="flex flex-wrap justify-center md:justify-start gap-2">
                                                <a href="https://modrinth.com/mod/dynamic-village" target="_blank" rel="noopener noreferrer" class="button-download notched-corners">
                                                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" class="mr-2">
                                                        <g id="Interface / Download">
                                                            <path id="Vector" d="M6 21H18M12 3V17M12 17L17 12M12 17L7 12" stroke="currentColor" stroke-width="4" stroke-linecap="round" stroke-linejoin="round"/>
                                                        </g>
                                                    </svg>
                                                    modrinth
                                                </a>
                                                <a href="https://curseforge.com/minecraft/mc-mods/dynamic-village" target="_blank" rel="noopener noreferrer" class="button-download notched-corners">
                                                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" class="mr-2">
                                                        <g id="Interface / Download">
                                                            <path id="Vector" d="M6 21H18M12 3V17M12 17L17 12M12 17L7 12" stroke="currentColor" stroke-width="4" stroke-linecap="round" stroke-linejoin="round"/>
                                                        </g>
                                                    </svg>
                                                    curseforge
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
    </main>

<style> 

    :global(.mod-tag) { 
        @apply bg-black/20 text-blue-100 text-sm/6 lowercase font-bold 
    }
    :global(.button-download) {
        @apply notched-corners inline-flex items-center px-4 py-2 bg-slate-600 text-white  hover:bg-slate-500 transition-colors duration-200;
    }
    :global(.notched-corners) {
        clip-path: polygon(
            0% 5px,
            5px 5px,
            5px 0%,
            calc(100% - 5px) 0%,
            calc(100% - 5px) 5px,
            100% 5px,
            100% calc(100% - 5px),
            calc(100% - 5px) calc(100% - 5px),
            calc(100% - 5px) 100%,
            5px 100%,
            5px calc(100% - 5px),
            0% calc(100% - 5px)
        );
    }
</style>