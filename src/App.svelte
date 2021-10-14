<script lang="ts">
  import Background from './lib/Background.svelte'
  import Countdown from './lib/Countdown.svelte';
  import fbImg from './assets/icon-facebook.svg'
  import pinterestImg from './assets/icon-pinterest.svg'
  import instagramImg from './assets/icon-instagram.svg'

</script>

<main>
  <Background/>
  <h1>WE'RE LAUNCHING SOON</h1>
  <Countdown/>
  <div class="social-media">
    <a href="https://www.facebook.com" target="_blank">
      <img src="{fbImg}" alt="facebook-img">
    </a>
    <a href="https://www.pinterest.com">

      <img src="{pinterestImg}" alt="pinterest-img">
    </a>
    <a href="https://www.instagram.com">
      <img src="{instagramImg}" alt="instagram-img">

    </a>
  </div>
</main>

<style>

@import url('https://fonts.googleapis.com/css2?family=Red+Hat+Text:wght@700&display=swap');

  :root {
    font-family: 'Red Hat Text', sans-serif;

    --primary-blue: hsl(237, 18%, 59%);
    --primary-red: hsl(345, 95%, 68%);
    --primary-green: rgba(251, 96, 135);

    --neutral-desaturated-blue: hsl(236, 21%, 26%);
    --neutral-dark-blue: hsl(235, 16%, 14%);
    --neutral-very-dark-blue: hsl(234, 17%, 12%);
  }
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }
  main {
   height: 100vh;
   position: relative;
  }
  h1 {
    color: #fff;
    font-size: 1.5rem;
    width: 100%;
    text-align: center;
    word-spacing: 0.7rem;
    letter-spacing: 0.4rem;
    padding: 7rem;
  }
  .social-media {
    position: absolute;
    bottom: 10%;
    width: 100%;
    display: flex;
    justify-content: center;
  }
  a {
    margin-right: 2rem;
  }
  img:hover {
    /* Make svg the same as color as primary red */
    filter: invert(71%) sepia(69%) saturate(4947%) hue-rotate(310deg) brightness(100%) contrast(98%);
  }
  @media only screen and (max-width: 650px) {
      h1 {
        padding: 10rem 0.7rem 4rem 0.7rem;
      }
    }
</style>
