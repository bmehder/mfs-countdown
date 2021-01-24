<svelte:options tag="mfs-countdown" />

<script>
  import { onMount } from 'svelte';
  // Change the date/time for the countdown
  export let end = 'February 1, 2025 5:00:00 GMT';
  export let title;

  let later = new Date(`${end}`).getTime();
  let days = 0;
  let hours = 0;
  let mins = 0;
  let seconds = 0;

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
        countdown.style.color = '#17a2b8';
        countdown.innerHTML = `SALE has ended.`;
      }
    }, 1000);
  });

  function handleClick() {
    window.location =
      'https://myfunscience.com/course-tag/full-year-2021-2022/;';
  }
</script>

<main>
  <h3>{title}</h3>
  <section on:click={handleClick} bind:this={countdown} class="countdown">
    <div>{days}<span>Days</span></div>
    <div>{hours}<span>Hours</span></div>
    <div>{mins}<span>Minutes</span></div>
    <div>{seconds}<span>Seconds</span></div>
  </section>
</main>

<style>
  main {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  h3 {
    font-size: 2em;
    line-height: 1.5em;
    text-align: center;
  }
  .countdown {
    cursor: pointer;
    font-size: 25px;
    color: #fff;
    font-weight: bold;
    display: flex;
    /* flex-wrap: wrap; */
    justify-content: center;
    align-items: center;
    text-align: center;
    max-width: 800px;
    margin: 0 auto;
    /* -webkit-box-reflect: below -16px -webkit-gradient(
        linear,
        left top,
        left bottom,
        from(transparent),
        color-stop(66%, transparent),
        to(rgba(250, 250, 250, 0.2))
      ); */
    text-shadow: 0 0 4px rgba(0, 0, 0, 0.24);
  }

  .countdown div {
    padding: 1em;
    min-width: 25%;
    border-radius: 25px;
    margin: 10px;
    background-color: #307ad5;
    border-color: transparent;
  }

  .countdown span {
    display: block;
    color: #fdc735;
    font-size: 20px;
    padding-top: 5px;
    text-shadow: 0 0 4px rgba(0, 0, 0, 0.24);
  }

  .countdown span:hover {
    transform: scale(1.1);
    transition: transform 0.5s ease-in-out;
  }

  @media (max-width: 480px) {
    .countdown {
      flex-direction: column;
      align-items: center;
      font-size: 20px;
    }

    .countdown span {
      font-size: 10px;
    }

    .countdown div {
      /* display: block; */
      width: 100%;
      padding: 10px;
    }
  }
</style>
