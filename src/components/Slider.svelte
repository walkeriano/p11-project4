<script>
  import { onMount } from "svelte";
  import replay from "../img/ver-01.svg";
  import arrow from "../img/icon-flecha-01.svg";

  const options = {
    method: "GET",
    headers: {
      accept: "application/json",
      Authorization:
        "Bearer eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiIwYTQ4YTNhOTY1MWQ3MjI3YzA1NWUzYzgxMTRkMGYxZiIsInN1YiI6IjY1MmU3ZTI3MDI0ZWM4MDBhZWNkNjg5YyIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.wcxAWg3WYbvS9yD0D_aCCiWel6vH6ZysgaxhhdYIpM4",
    },
  };

  const link =
    "https://api.themoviedb.org/3/movie/upcoming?api_key=0a48a3a9651d7227c055e3c8114d0f1f";

  let estrenos = [];
  let isLoading = true;

  onMount(async () => {
    try {
      const response = await fetch(link, options);
      const data = await response.json();
      estrenos = data.results;
    } catch (error) {
      console.error(error);
    } finally {
      isLoading = false;
    }
  });

  
  let container;
  let scrollPosition = 0;
  const getWindowWidth = () => window.innerWidth;

  const next = () => {
    if (container) {
      scrollPosition += getWindowWidth();
      container.scroll({ left: scrollPosition, behavior: "smooth" });
    }
  };

  const back = () => {
    if (container) {
      scrollPosition -= getWindowWidth();
      container.scroll({ left: scrollPosition, behavior: "smooth" });
    }
  };

</script>

<section class="bg-slider">
  <button on:click={next} class="bt-next">
    <img src={arrow} alt="arrow" />
  </button>
  {#if isLoading}
    <div class="cont-load">
      <span class="span-loading" />
    </div>
  {:else}
    <section class="cont-img-slider" bind:this={container}>
      {#each estrenos as estreno}
        <div class="sec-imgs">
          <div class="info-img">
            <h1>{estreno.title}</h1>
            <p>Alejandro Rojas y Juan Sebastian Vasquez</p>
            <div class="fun-slider">
              <button class="btn-ver">VER AHORA</button>
              <button class="btn-replay">
                <img src={replay} alt="i-replay" />
              </button>
            </div>
          </div>
          <span class="grad-slid" />
          <img
            src={`https://image.tmdb.org/t/p/original/${estreno.poster_path}`}
            alt="Cover"
            class="img-slider"
          />
        </div>
      {/each}
    </section>
  {/if}
  <button on:click={back} class="bt-back">
    <img src={arrow} alt="arrow" />
  </button>
</section>

<style>
  .cont-load {
    background-color: white;
    width: 90px;
    height: 90px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
  }

  .span-loading {
    width: 35px;
    height: 35px;
    border: 7px dotted #00103d;
    border-radius: 50%;
    animation: load 5s infinite ease-out;
    background-color: white;
  }

  @keyframes load {
    0% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(360deg);
    }
  }
  
  .bg-slider {
    width: 100%;
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #00103d;
  }

  .bt-next {
    position: absolute;
    right: 40px;
    z-index: 1000;
    border: none;
    background-color: transparent;
    cursor: pointer;
  }

  .bt-next img {
    width: 35px;
    transform: rotate(-90deg);
  }

  .bt-back {
    position: absolute;
    left: 40px;
    z-index: 1000;
    border: none;
    background-color: transparent;
    cursor: pointer;
  }

  .bt-back img {
    width: 35px;
    transform: rotate(90deg);
  }

  .cont-img-slider {
    width: 100vw;
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: start;
    overflow-x: hidden;
    overflow-y: hidden;
  }

  .sec-imgs {
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    position: relative;
  }

  .img-slider {
    min-width: 100vw;
    height: 100%;
    object-fit: cover;
  }

  .info-img {
    width: 95%;
    position: absolute;
    bottom: 20px;
    color: white;
    z-index: 1900;
  }

  .info-img h1 {
    font-size: 2.5rem;
    margin-bottom: 10px;
    font-weight: bold;
    text-transform: uppercase;
    letter-spacing: 1px;
  }

  .info-img p {
    font-size: 1rem;
    margin-bottom: 20px;
    letter-spacing: 0.5px;
  }

  .grad-slid {
    width: 100%;
    height: 350px;
    position: absolute;
    background: linear-gradient(to top, #00103d, #00103d00);
    bottom: 0px;
    z-index: 90;
  }

  .fun-slider {
    width: 100%;
    height: 100px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    z-index: 100;
  }

  .btn-ver {
    background-color: white;
    border: none;
    padding: 10px 15px;
    border-radius: 5px;
    letter-spacing: 0.4px;
    font-size: 1rem;
    letter-spacing: 0.5px;
    font-weight: bold;
    cursor: pointer;
  }

  .btn-ver:hover {
    background-color: #00ff9e;
  }

  .btn-replay {
    width: 50px;
    height: 50px;
    border-radius: 50%;
    background-color: #040031;
    border: none;
    cursor: pointer;
  }

  .btn-replay:hover {
    background-color: #001149;
  }

  .btn-replay img {
    width: 20px;
  }

  .bt-next:hover, .bt-back:hover{
    transform: scale(1.3);
    transition: 0.3s linear;
  }
</style>
