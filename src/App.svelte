<svelte:options tag="mfs-countdown" />

<script>
  import { onMount } from 'svelte';
  // Change the date/time for the countdown
  export let end = 'March 1, 2021 5:00:00 GMT';
  export let title = '';

  let later = new Date(`${end}`).getTime();
  let days = 0;
  let hours = 0;
  let mins = 0;
  let seconds = 0;
  let isEnded = false;

  let countdown;
  onMount(() => {
    const interval = setInterval(() => {
      // Time calculation
      const now = new Date().getTime();
      const difference = later - now;

      days = Math.floor(difference / (1000 * 60 * 60 * 24));
      hours = Math.floor(
        (difference % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)
      );
      mins = Math.floor((difference % (1000 * 60 * 60)) / (1000 * 60));
      seconds = Math.floor((difference % (1000 * 60)) / 1000);

      // If the end date/time has passed...
      if (difference < 0) {
        clearInterval(interval);
        isEnded = true;
        countdown.style.color = '#307ad5';
        countdown.innerHTML = 'The Sale Has Ended.';
      }
    }, 1000);
  });

  function handleClick() {
    window.location =
      'https://myfunscience.com/course-tag/full-year-2021-2022/;';
  }
</script>

<main>
  {#if !isEnded}
    <h3>{title}</h3>
  {/if}
  <section on:click={handleClick} bind:this={countdown} class="countdown">
    <div style="background-color: #10c45c;">{days}<span>Days</span></div>
    <div style="background-color: #307ad5;">{hours}<span>Hours</span></div>
    <div style="background-color: #fdc735;">{mins}<span>Minutes</span></div>
    <div style="background-color: #d94da6;">{seconds}<span>Seconds</span></div>
  </section>
</main>

<style>
  main {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  h3 {
    margin: 0 0 0.5em 0;
    font-size: 2em;
    line-height: 1.5em;
    text-align: center;
    color: #444;
  }
  .countdown {
    cursor: pointer;
    font-size: 24px;
    color: white;
    font-weight: bold;
    display: flex;
    /* flex-wrap: wrap; */
    justify-content: center;
    align-items: center;
    text-align: center;
    max-width: 800px;
    margin: 0 auto;
    /* text-shadow: 0 0 4px rgba(0, 0, 0, 0.24); */
  }

  .countdown div {
    /* padding: 1em; */
    /* min-width: 25%; */
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width: 120px;
    height: 120px;
    border-radius: 50%;
    margin: 10px;
    background-color: #fdc735;
    border-color: transparent;
    box-shadow: 0 20px 30px rgba(0, 0, 0, 0.24);
    background-image: linear-gradient(
      to bottom right,
      transparent,
      rgba(0, 0, 0, 0.05)
    );
    /* text-shadow: none; */
    animation: spin 1.2s ease-in-out;
  }
  @keyframes spin {
    0% {
      transform: rotate(0deg);
      box-shadow: none;
    }
    100% {
      transform: rotate3d(1, 1, 1, 360deg);
    }
  }

  .countdown span {
    display: block;
    color: #333;
    font-size: 18px;
    padding-top: 5px;
    text-shadow: 0 0 2px rgba(255, 255, 255, 0.24);
  }

  .countdown span:hover {
    transform: scale(1.1);
    transition: transform 0.5s ease-in-out;
  }

  @media (max-width: 480px) {
    .countdown {
      flex-direction: column;
    }
  }
</style>
