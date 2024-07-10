<script lang="ts">
	import { onMount } from 'svelte';
	import Lenis from 'lenis';
	import { gsap } from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';
	
	gsap.registerPlugin(ScrollTrigger);
	
	let title: HTMLElement;
	let content: HTMLElement;
	let background: HTMLElement;
	let projects: HTMLElement;
	let scrollArrow: HTMLElement;
	
	const techStack = [
		{ name: "JavaScript", url: "https://developer.mozilla.org/en-US/docs/Web/JavaScript" },
		{ name: "HTML", url: "https://developer.mozilla.org/en-US/docs/Web/HTML" },
		{ name: "CSS", url: "https://developer.mozilla.org/en-US/docs/Web/CSS" },
		{ name: "TypeScript", url: "https://www.typescriptlang.org/" },
		{ name: "Next.js", url: "https://nextjs.org/" },
		{ name: "React", url: "https://reactjs.org/" },
		{ name: "Svelte", url: "https://svelte.dev/" },
		{ name: "Bash", url: "https://www.gnu.org/software/bash/" },
		{ name: "Node.js", url: "https://nodejs.org/" },
		{ name: "Lua", url: "https://www.lua.org/" },
		{ name: "Python", url: "https://www.python.org/" }
	];
	
	const projectList = [
	  { name: "AppleBlox", description: "A lightweight Roblox launcher", url: "https://github.com/OrigamingWasTaken/appleblox" },
	  { name: "ce-discord-bot", description: "Discord bot that notifies you of Minecraft events", url: "https://github.com/Communaute-Events/ce-discord-bot" },
	  { name: "paper-comet", description: "A basic addon for Meteor, made for me to learn Java", url: "https://github.com/OrigamingWasTaken/paper-comet" },
	];
	
	onMount(() => {
	  const lenis = new Lenis({
		duration: 1.2,
		easing: (t) => Math.min(1, 1.001 - Math.pow(2, -10 * t)),
		// @ts-expect-error
		direction: 'vertical',
		gestureDirection: 'vertical',
		smooth: true,
		smoothTouch: false,
		touchMultiplier: 2,
	  });
	
	  function raf(time: number) {
		lenis.raf(time);
		requestAnimationFrame(raf);
	  }
	
	  requestAnimationFrame(raf);
	
	  // Title animation
	  gsap.to(title, {
		scrollTrigger: {
		  trigger: title,
		  start: 'center center',
		  end: 'center top+=100',
		  scrub: true,
		},
		y: '-20vh',
		scale: 0.8,
		opacity: 0.7,
	  });
	
	  // Content animation
	  gsap.from(content, {
		scrollTrigger: {
		  trigger: content,
		  start: 'top bottom-=100',
		  end: 'top center+=100',
		  scrub: true,
		},
		y: 50,
		opacity: 0,
		scale: 0.95,
	  });
	
	  // Background parallax effect
	  gsap.to(background, {
		scrollTrigger: {
		  trigger: 'main',
		  start: 'top top',
		  end: 'bottom top',
		  scrub: true,
		},
		y: '30%',
	  });
	
	  // Projects animation
	  gsap.from(projects, {
		scrollTrigger: {
		  trigger: projects,
		  start: 'top bottom-=100',
		  end: 'top center+=100',
		  scrub: true,
		},
		y: 50,
		opacity: 0,
		scale: 0.95,
	  });

	  // Scroll arrow animation
	  gsap.to(scrollArrow, {
		y: 10,
		opacity: 0.5,
		duration: 1,
		repeat: -1,
		yoyo: true,
		ease: "power1.inOut"
	  });
	});
	</script>
	
	<main class="overflow-y-clip relative min-h-[200vh] bg-black text-green-400 font-mono">
		<div class="glitch-effect"></div>
		<div class="h-screen flex flex-col items-center justify-center relative">
		  <h1 bind:this={title} class="text-6xl text-shadow shadow-green-400 text-center z-10 glitch" data-text="Origaming">
			Origaming
		  </h1>
		  <div bind:this={scrollArrow} class="absolute bottom-8 left-1/2 transform -translate-x-1/2 cursor-pointer">
			<svg xmlns="http://www.w3.org/2000/svg" width="40" height="40" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="text-green-400">
			  <path d="M12 5v14M19 12l-7 7-7-7"/>
			</svg>
		  </div>
		</div>
		<div bind:this={content} class="min-h-[50vh] flex items-start justify-center pt-20">
		  <div class="bg-black/50 border border-green-400 p-8 rounded-lg shadow-lg max-w-2xl w-full">
			<h2 class="text-3xl font-bold mb-4 glitch" data-text="Welcome to My Code Realm">Welcome to My Code Realm</h2>
			<p class="mb-4">
				I'm Origaming (she/he) and I am a passionate fullstack developper! I know TypeScript, Bash, and Python, and hope to learn 🦀 Rust in the future!
			  </p>
			  <p class="mb-4">
				But coding and solving problems is not my only passion. I also love playing the drums and cycling :D
			  </p>
			  <p class="mb-4">
				Now, scroll down through the projects that made the developper I am today...
			  </p>
			<h3 class="text-2xl font-bold mb-2">Tech Stack</h3>
			<div class="flex flex-wrap gap-2 mb-4">
			  {#each techStack as tech}
				<a href={tech.url} target="_blank" rel="noopener noreferrer" class="px-2 py-1 bg-green-400/20 text-green-300 rounded hover:bg-green-400/30 transition-colors duration-300">
				  {tech.name}
				</a>
			  {/each}
			</div>
			<div class="mt-6 flex justify-center space-x-4">
				<a href={`https://github.com/OrigamingWasTaken`} target="_blank" rel="noopener noreferrer" class="github-icon">
				  <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="hover:text-green-300 transition-colors duration-300">
					<path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"></path>
				  </svg>
				</a>
				<a href={`mailto:contact@origaming.ch`} class="email-icon">
				  <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="hover:text-green-300 transition-colors duration-300">
					<path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"></path>
					<polyline points="22,6 12,13 2,6"></polyline>
				  </svg>
				</a>
			</div>
		  </div>
		</div>
		<div bind:this={projects} class="min-h-[50vh] flex items-start justify-center pt-20 pb-20">
		  <div class="bg-black/50 border border-green-400 p-8 rounded-lg shadow-lg max-w-2xl w-full">
			<h2 class="text-3xl font-bold mb-6 glitch" data-text="My Projects">My Projects</h2>
			<div class="space-y-6">
			  {#each projectList as project}
			  <div>
				<button class="w-full border border-green-400 p-4 rounded-lg hover:bg-green-400/10 transition-colors duration-300 focus">
					<h3 class="text-xl font-bold mb-2">{project.name}</h3>
					<p class="mb-2">{project.description}</p>
					<a href={project.url} target="_blank" rel="noopener noreferrer" class="text-green-300 hover:text-green-100 transition-colors duration-300">
					  View on GitHub &rarr;
					</a>
				  </button>
			  </div>
			  {/each}
			</div>
		  </div>
		</div>
		<div bind:this={background} class="fixed inset-x-0 bottom-0 overflow-visible flex justify-center items-center pointer-events-none">
		  <div class="absolute bottom-0 h-[100vw] bg-gradient-to-t from-green-500 to-transparent w-full rounded-full transform -translate-x-1/2 translate-y-1/2 opacity-20">
		  </div>
		</div>
	  </main>
	
	<style>

	  :global(html, body) {
		overflow-x: hidden;
		background-color: black;
	  }
	
	  .glitch-effect {
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background: repeating-linear-gradient(
		  0deg,
		  rgba(0, 255, 0, 0.15) 0px,
		  rgba(0, 255, 0, 0.15) 1px,
		  transparent 1px,
		  transparent 2px
		);
		pointer-events: none;
		z-index: 1;
	  }
	
	  .glitch {
		position: relative;
		animation: glitch 1s infinite;
	  }
	
	  .glitch::before,
	  .glitch::after {
		content: attr(data-text);
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		opacity: 0.8;
	  }
	
	  .glitch::before {
		left: 2px;
		text-shadow: -2px 0 #ff00c1;
		clip: rect(44px, 450px, 56px, 0);
		animation: glitch-anim 5s infinite linear alternate-reverse;
	  }
	
	  .glitch::after {
		left: -2px;
		text-shadow: -2px 0 #00fff9, 2px 2px #ff00c1;
		animation: glitch-anim2 1s infinite linear alternate-reverse;
	  }
	
	  @keyframes glitch {
		0% {
		  transform: translate(0);
		}
		20% {
		  transform: translate(-2px, 2px);
		}
		40% {
		  transform: translate(-2px, -2px);
		}
		60% {
		  transform: translate(2px, 2px);
		}
		80% {
		  transform: translate(2px, -2px);
		}
		100% {
		  transform: translate(0);
		}
	  }
	
	  @keyframes glitch-anim {
		0% {
		  clip: rect(96px, 9999px, 29px, 0);
		}
		10% {
		  clip: rect(58px, 9999px, 95px, 0);
		}
		20% {
		  clip: rect(30px, 9999px, 7px, 0);
		}
		30% {
		  clip: rect(97px, 9999px, 91px, 0);
		}
		40% {
		  clip: rect(62px, 9999px, 43px, 0);
		}
		50% {
		  clip: rect(82px, 9999px, 10px, 0);
		}
		60% {
		  clip: rect(54px, 9999px, 42px, 0);
		}
		70% {
		  clip: rect(92px, 9999px, 16px, 0);
		}
		80% {
		  clip: rect(10px, 9999px, 3px, 0);
		}
		90% {
		  clip: rect(37px, 9999px, 88px, 0);
		}
		100% {
		  clip: rect(46px, 9999px, 68px, 0);
		}
	  }
	
	  @keyframes glitch-anim2 {
		0% {
		  clip: rect(33px, 9999px, 97px, 0);
		}
		10% {
		  clip: rect(89px, 9999px, 38px, 0);
		}
		20% {
		  clip: rect(6px, 9999px, 46px, 0);
		}
		30% {
		  clip: rect(76px, 9999px, 22px, 0);
		}
		40% {
		  clip: rect(88px, 9999px, 19px, 0);
		}
		50% {
		  clip: rect(11px, 9999px, 72px, 0);
		}
		60% {
		  clip: rect(5px, 9999px, 23px, 0);
		}
		70% {
		  clip: rect(82px, 9999px, 59px, 0);
		}
		80% {
		  clip: rect(99px, 9999px, 27px, 0);
		}
		90% {
		  clip: rect(44px, 9999px, 56px, 0);
		}
		100% {
		  clip: rect(18px, 9999px, 3px, 0);
		}
	  }
	
	  .github-icon:hover svg,
	  .email-icon:hover svg {
		filter: drop-shadow(0 0 5px #4ade80);
	  }

	  
	</style>