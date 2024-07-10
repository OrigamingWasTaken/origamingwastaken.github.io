<script lang="ts">
  import { onMount } from 'svelte';
  import { tweened } from 'svelte/motion';

  const canvasWidth = window.innerWidth;
  const canvasHeight = window.innerHeight;
  const starsCount = 100;
  let stars: Star[] = [];

  interface Star {
    x: number;
    y: number;
    opacity: number;
    size: number;
    speed: number;
    curveX: number;
    curveY: number;
  }

  let ctx: CanvasRenderingContext2D | null = null;
  let canvas: { subscribe: any };

  canvas = tweened(null, { duration: 1000 });

  onMount(() => {
    const canvasElem = document.getElementById('star-canvas') as HTMLCanvasElement;
    // @ts-expect-error
    canvas.set(canvasElem);

    ctx = canvasElem.getContext('2d');
    canvasElem.width = canvasWidth;
    canvasElem.height = canvasHeight;

    createStars();

    const animationFrame = () => {
      updateStars();
      drawStars();
      requestAnimationFrame(animationFrame);
    };

    animationFrame();

    return () => {
      // Clean up
      stars = [];
    };
  });

  function createStars() {
    for (let i = 0; i < starsCount; i++) {
      stars.push({
        x: Math.random() * canvasWidth,
        y: Math.random() * canvasHeight,
        opacity: Math.random() * 0.5 + 0.5,
        size: Math.random(),
        speed: Math.random() * 0.5 + 0.1,
        curveX: Math.random() * 2 - 1,
        curveY: Math.random() * 2 - 1
      });
    }
  }

  function updateStars() {
    stars.forEach(star => {
      star.x += star.curveX * star.speed;
      star.y += star.curveY * star.speed;

      if (star.x < 0 || star.x > canvasWidth) star.curveX *= -1;
      if (star.y < 0 || star.y > canvasHeight) star.curveY *= -1;
    });
  }

  function drawStars() {
    if (!ctx) return;

    ctx.clearRect(0, 0, canvasWidth, canvasHeight);

    stars.forEach(star => {
      ctx!.beginPath();
      ctx!.arc(star.x, star.y, star.size, 0, Math.PI * 2);
      ctx!.fillStyle = `rgba(255, 255, 255, ${star.opacity})`;
      ctx!.fill();
    });
  }
</script>

<style>
  #star-canvas {
    position: fixed;
    top: 0;
    left: 0;
    pointer-events: none;
    z-index: -1;
  }
</style>

<canvas id="star-canvas"></canvas>
