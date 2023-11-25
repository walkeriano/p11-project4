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
      "https://api.themoviedb.org/3/movie/top_rated?api_key=0a48a3a9651d7227c055e3c8114d0f1f";
  
    let tops = [];
    let isLoading = true;
  
    onMount(async () => {
      try {
        const response = await fetch(link, options);
        const data = await response.json();
        tops = data.results;
      } catch (error) {
        console.error(error);
      } finally {
        isLoading = false;
      }
    });
  
    let containerTop;
    let scrollPosition = 0;
  
    const nextTwo = () => {
      if (containerTop) {
        scrollPosition += 200;
        containerTop.scroll({ left: scrollPosition, behavior: "smooth" });
      }
    };
  
    const backTwo = () => {
      if (containerTop) {
        scrollPosition -= 200;
        containerTop.scroll({ left: scrollPosition, behavior: "smooth" });
      }
    };
  </script>
  
  <section class="sec-movies-two">
    <button on:click={nextTwo} class="bt-next-two">
      <img src={arrow} alt="arrow" />
    </button>
    {#if isLoading}
      <div class="cont-load-two">
        <span class="span-loading-two" />
      </div>
    {:else}
      <section class="categoria-two">
        <p>Recomendadas</p>
        <span class="sombra-om-two" />
        <div class="cartelera-cont-two" bind:this={containerTop}>
          {#each tops as cartelera}
            <div class="items-two">
              <img
                src={`https://image.tmdb.org/t/p/original/${cartelera.poster_path}`}
                alt="Cover"
              />
              <section class="detalles-items-two">
                <div class="img-detail-grad-two">
                  <img
                    src={`https://image.tmdb.org/t/p/original/${cartelera.poster_path}`}
                    alt="Cover-detail"
                    class="img-detail-two"
                  />
                  <div class="grad-img-two" />
                </div>
                <div class="cont-info-two">
                  <div class="votos-space-two">
                    <p>{cartelera.vote_average}</p>
                    <p>{cartelera.vote_count}</p>
                  </div>
                  <div class="cont-btns-two">
                    <button class="play-btn-two">
                      <img src={play} class="play" alt="i-play" />
                      VER AHORA
                    </button>
                    <button class="time-btn-two">
                      <img src={time} class="time-two" alt="i-play" />
                    </button>
                  </div>
                  <h2 class="title-cartelera-two">{cartelera.title}</h2>
                  <p class="fecha-two">{cartelera.release_date}</p>
                  <p class="descrip-two">{cartelera.overview}</p>
                </div>
              </section>
            </div>
          {/each}
        </div>
        <span class="sombra-two-two" />
      </section>
    {/if}
    <button on:click={backTwo} class="bt-back-two">
      <img src={arrow} alt="arrow" />
    </button>
  </section>
  
  <style>
    .sec-movies-two {
      width: 100%;
      background-color: #00103d;
      display: flex;
      flex-direction: column;
      align-items: flex-start;
      justify-content: flex-start;
      position: relative;
    }
  
    .categoria-two {
      width: 100%;
      height: 350px;
      display: flex;
      flex-direction: column;
      align-items: flex-start;
      justify-content: space-between;
      padding-top: 100px;
      position: relative;
    }
  
    .categoria-two p {
      font-size: 1.5rem;
      color: white;
      letter-spacing: 0.5px;
      margin-left: 80px;
      position: relative;
    }
  
    .cartelera-cont-two {
      width: 100%;
      height: 300px;
      display: flex;
      align-items: center;
      justify-content: start;
      overflow-x: hidden;
      overflow-y: hidden;
    }
  
    .categoria-two .sombra-two-two {
      width: 200px;
      height: 350px;
      background: linear-gradient(to left, #00103d, #04003100);
      position: absolute;
      right: 0px;
      top: 100px;
    }
    .categoria-two .sombra-om-two {
      width: 100px;
      height: 300px;
      background: linear-gradient(to right, #00103d, #04003100);
      position: absolute;
      left: 0px;
      top: 150px;
    }
  
    .items-two {
      min-width: 200px;
      height: 280px;
      margin-left: 30px;
    }
  
    .items-two:first-child {
      margin-left: 80px;
    }
  
    .items-two img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      border-radius: 10px;
    }
  
    .detalles-items-two {
      display: none;
    }
  
    .items-two:hover {
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
      & .img-detail-grad-two {
        width: 100%;
        height: 150px;
        position: relative;
      }
      & .img-detail-two {
        width: 100%;
        height: 100%;
        object-fit: cover;
        border-radius: 10px;
      }
      & .grad-img-two {
        width: 100%;
        height: 70px;
        background: linear-gradient(to top, #00103d, #00103d00);
        position: absolute;
        bottom: 0px;
      }
      & .cont-info-two {
        width: 80%;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        margin-top: 10px;
      }
  
      & .cont-info-two p {
        margin-left: 0px;
      }
  
      & .votos-space-two {
        width: 100%;
        display: flex;
        align-items: center;
        justify-content: flex-start;
        padding: 0;
      }
      & .votos-space-two p:first-child {
        margin-left: 0px;
        font-size: 1.1rem;
        border: 1px solid white;
        padding: 10px 10px;
        border-radius: 5px;
        margin-right: 15px;
        font-weight: bold;
        letter-spacing: 1px;
      }
      & .votos-space-two p:last-child {
        margin-left: 0px;
        font-size: 0.9rem;
      }
      & .cont-btns-two {
        width: 100%;
        display: flex;
        align-items: center;
        justify-content: flex-start;
        margin-top: 15px;
      }
      & .play-btn-two {
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
      & .play-btn-two .play-two {
        width: 30px;
        height: 30px;
      }
      & .time-btn-two {
        width: 50px;
        height: 50px;
        background-color: rgba(0, 0, 0, 0.623);
        border: none;
        border-radius: 5px;
        cursor: pointer;
      }
      & .time-btn-two .time-two {
        width: 25px;
        height: 25px;
      }
      & .title-cartelera-two {
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
      & .cont-info-two .fecha-two {
        width: 100%;
        font-size: 0.8rem;
        margin-bottom: 20px;
      }
      & .cont-info-two .descrip-two {
        font-size: 0.9rem;
        line-height: 1.1;
        letter-spacing: 1px;
      }
    }
  
    .bt-next-two {
      position: absolute;
      right: 20px;
      bottom: 30%;
      z-index: 1000;
      border: none;
      background-color: transparent;
      cursor: pointer;
    }
  
    .bt-next-two img {
      width: 35px;
      transform: rotate(-90deg);
    }
  
    .bt-back-two {
      position: absolute;
      left: 20px;
      bottom: 30%;
      border: none;
      background-color: transparent;
      cursor: pointer;
    }
  
    .bt-back-two img {
      width: 35px;
      transform: rotate(90deg);
    }
  
    .bt-next-two:hover,
    .bt-back-two:hover {
      transform: scale(1.3);
      transition: 0.3s linear;
    }
  
    .cont-load-two {
      width: 100%;
      height: 550px;
      display: flex;
      align-items: center;
      justify-content: center;
    }
  
    .span-loading-two {
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
  