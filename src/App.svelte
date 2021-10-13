<script>
  import { rawData } from './data'
  import { bestScore } from './store'
  import Card from './Card.svelte'

  let shuffledCards = []
  let cards = []
  let clicks = 0

  const randomizeCards = () => {
    cards = [...rawData, ...rawData]
    shuffledCards = cards.sort(() => Math.random() - 0.5)
  }

  if (localStorage.getItem('bestScore')) {
    $bestScore = localStorage.getItem('bestScore')
  }
</script>

<svelte:head>
  <title>Memory Game - Highlands Motoring Festival</title>
  <meta property="og:locale" content="en_US" />
  <meta property="og:type" content="website" />
  <meta
    property="og:title"
    content="Memory Game - Highlands Motoring Festival"
  />
  <meta
    property="og:description"
    content="Play the Highlands Motoring Festival Memory Game!"
  />
  <meta property="og:url" content="https://hmf-memory.netlify.app/" />
  <meta
    property="og:site_name"
    content="Highlands Motoring Festival Memory Game"
  />
  <meta
    property="article:publisher"
    content="https://www.facebook.com/highlandsmotoringfestival"
  />
  <meta
    property="og:image"
    content="https://highlandsmotoringfestival.com/wp-content/uploads/highlands-motoring-festival-logo-alternate-1.png"
  />
  <meta property="og:image:width" content="794" />
  <meta property="og:image:height" content="386" />
</svelte:head>

<svelte:body use:randomizeCards />

<main>
  <h1>Memory ({clicks} {clicks === 1 ? 'try' : 'tries'})</h1>
  <h2>Best Score: {$bestScore === Infinity ? 'No score' : $bestScore}</h2>
  <section>
    {#each shuffledCards as card}
      <Card {card} {randomizeCards} bind:clicks />
    {/each}
  </section>
</main>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@700&display=swap');
  h1,
  h2 {
    margin-bottom: 1rem;
    text-align: center;
    font-family: 'Poppins', sans-serif;
    color: white;
  }
  main {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    background-color: #00003e;
    background-repeat: no-repeat;
    background-size: cover;
  }
  section {
    display: grid;
    grid-template-columns: repeat(4, 8vw);
    grid-template-rows: repeat(4, 8vw);
    gap: 2rem;
    perspective: 800px;
    -webkit-perspective: 800px;
  }
  @media screen and (max-width: 600px) {
    h1 {
      font-size: 1.5rem;
    }
    h2 {
      font-size: 1rem;
    }
  }
</style>
