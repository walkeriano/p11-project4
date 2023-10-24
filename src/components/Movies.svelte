<script>
  import { onMount } from "svelte";
  import play from "../img/play-01.svg";
  import time from "../img/time-01.svg";
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
    "https://api.themoviedb.org/3/movie/popular?api_key=0a48a3a9651d7227c055e3c8114d0f1f";

  let carteleras = [];
  let isLoading = true;

  onMount(async () => {
    try {
      const response = await fetch(link, options);
      const data = await response.json();
      carteleras = data.results;
    } catch (error) {
      console.error(error);
    } finally {
      isLoading = false;
    }
  });

  let containerMovies;
  let scrollPosition = 0;

  const next = () => {
    if (containerMovies) {
      scrollPosition += 200;
      containerMovies.scroll({ left: scrollPosition, behavior: "smooth" });
    }
  };

  const back = () => {
    if (containerMovies) {
      scrollPosition -= 200;
      containerMovies.scroll({ left: scrollPosition, behavior: "smooth" });
    }
  };
</script>

<section class="sec-movies">
  <button on:click={next} class="bt-next">
    <img src={arrow} alt="arrow" />
  </button>
  {#if isLoading}
    <div class="cont-load">
      <span class="span-loading" />
    </div>
  {:else}
    <section class="categoria">
      <p>Más populares</p>
      <span class="sombra-om" />
      <div class="cartelera-cont" bind:this={containerMovies}>
        {#each carteleras as cartelera}
          <div class="items">
            <img
              src={`https://image.tmdb.org/t/p/original/${cartelera.poster_path}`}
              alt="Cover"
            />
            <section class="detalles-items">
              <div class="img-detail-grad">
                <img
                  src={`https://image.tmdb.org/t/p/original/${cartelera.poster_path}`}
                  alt="Cover-detail"
                  class="img-detail"
                />
                <div class="grad-img" />
              </div>
              <div class="cont-info">
                <div class="votos-space">
                  <p>{cartelera.vote_average}</p>
                  <p>{cartelera.vote_count}</p>
                </div>
                <div class="cont-btns">
                  <button class="play-btn">
                    <img src={play} class="play" alt="i-play" />
                    VER AHORA
                  </button>
                  <button class="time-btn">
                    <img src={time} class="time" alt="i-play" />
                  </button>
                </div>
                <h2 class="title-cartelera">{cartelera.title}</h2>
                <p class="fecha">{cartelera.release_date}</p>
                <p class="descrip">{cartelera.overview}</p>
              </div>
            </section>
          </div>
        {/each}
      </div>
      <span class="sombra-two" />
    </section>
  {/if}
  <button on:click={back} class="bt-back">
    <img src={arrow} alt="arrow" />
  </button>
</section>

<style>
  .sec-movies {
    width: 100%;
    height: 1500px;
    background-color: #00103d;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: flex-start;
  }

  .categoria {
    width: 100%;
    height: 350px;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: space-between;
    padding-top: 100px;
    position: relative;
  }

  .categoria p {
    font-size: 1.5rem;
    color: white;
    letter-spacing: 0.5px;
    margin-left: 80px;
    position: relative;
  }

  .cartelera-cont {
    width: 100%;
    height: 300px;
    display: flex;
    align-items: center;
    justify-content: start;
    overflow-x: hidden;
    overflow-y: hidden;
  }

  .categoria .sombra-two {
    width: 200px;
    height: 350px;
    background: linear-gradient(to left, #00103d, #04003100);
    position: absolute;
    right: 0px;
    top: 100px;
  }
  .categoria .sombra-om {
    width: 100px;
    height: 300px;
    background: linear-gradient(to right, #00103d, #04003100);
    position: absolute;
    left: 0px;
    top: 150px;
  }

  .items {
    min-width: 200px;
    height: 280px;
    margin-left: 30px;
  }

  .items:first-child {
    margin-left: 80px;
  }

  .items img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 10px;
  }

  .detalles-items {
    display: none;
  }

  .items:hover {
    transition: 5s ease-out;
    & .detalles-items {
      display: inline-block;
      width: 300px;
      background-color: #00103d;
      border: 1px solid #001172;
      position: absolute;
      top: 50px;
      z-index: 900;
      padding-bottom: 30px;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: flex-start;
      box-shadow: 0px 2px 54px 10px #00071d;
      border-radius: 10px;
    }
    & .img-detail-grad {
      width: 100%;
      height: 150px;
      position: relative;
    }
    & .img-detail {
      width: 100%;
      height: 100%;
      object-fit: cover;
      border-radius: 10px;
    }
    & .grad-img {
      width: 100%;
      height: 70px;
      background: linear-gradient(to top, #00103d, #00103d00);
      position: absolute;
      bottom: 0px;
    }
    & .cont-info {
      width: 80%;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      margin-top: 10px;
    }

    & .cont-info p {
      margin-left: 0px;
    }

    & .votos-space {
      width: 100%;
      display: flex;
      align-items: center;
      justify-content: flex-start;
      padding: 0;
    }
    & .votos-space p:first-child {
      margin-left: 0px;
      font-size: 1.1rem;
      border: 1px solid white;
      padding: 10px 10px;
      border-radius: 5px;
      margin-right: 15px;
      font-weight: bold;
      letter-spacing: 1px;
    }
    & .votos-space p:last-child {
      margin-left: 0px;
      font-size: 0.9rem;
    }
    & .cont-btns {
      width: 100%;
      display: flex;
      align-items: center;
      justify-content: flex-start;
      margin-top: 15px;
    }
    & .play-btn {
      border: none;
      height: 50px;
      width: 160px;
      border-radius: 5px;
      background-color: #00ff9e;
      color: black;
      font-weight: bold;
      margin-right: 20px;
      display: flex;
      align-items: center;
      justify-content: space-evenly;
      font-size: 0.9rem;
      cursor: pointer;
    }
    & .play-btn .play {
      width: 30px;
      height: 30px;
    }
    & .time-btn {
      width: 50px;
      height: 50px;
      background-color: rgba(0, 0, 0, 0.623);
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    & .time-btn .time {
      width: 25px;
      height: 25px;
    }
    & .title-cartelera {
      color: white;
      margin-top: 20px;
      text-align: left;
      width: 100%;
      font-size: 1.2rem;
      font-weight: bold;
      letter-spacing: 0.5px;
      line-height: 1.3;
      margin-bottom: 10px;
    }
    & .cont-info .fecha {
      width: 100%;
      font-size: 0.8rem;
      margin-bottom: 20px;
    }
    & .cont-info .descrip {
      font-size: 0.9rem;
      line-height: 1.1;
      letter-spacing: 1px;
    }
  }

  .bt-next {
    position: absolute;
    right: 20px;
    bottom: -310px;
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
    left: 20px;
    bottom: -310px;
    border: none;
    background-color: transparent;
    cursor: pointer;
  }

  .bt-back img {
    width: 35px;
    transform: rotate(90deg);
  }

  .bt-next:hover,
  .bt-back:hover {
    transform: scale(1.3);
    transition: 0.3s linear;
  }

  .cont-load {
    width: 100%;
    height: 550px;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .span-loading {
    width: 35px;
    height: 35px;
    border: 7px dotted white;
    border-radius: 50%;
    animation: load 5s infinite ease-out;
  }

  @keyframes load {
    0% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(360deg);
    }
  }
</style>
