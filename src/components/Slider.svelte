<script>
  import { onMount } from "svelte";

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

  // let orden = 0;

  // const back = () => {
  //   if (orden > 0) {
  //     orden -= 1;
  //   }
  // };

  // const next = () => {
  //   if (orden < estrenos.length - 1) {
  //     orden += 1;
  //   }
  // };

</script>

<section class="bg-slider">
  {#if isLoading}
    <p>Cargando...</p>
  {:else}
    <section class="cont-img-slider">
      {#each estrenos as estreno}
        <div class="sec-imgs">
          <div class="info-img">
            <h1>{estreno.title}</h1>
            <p>Alejandro Rojas y Juan Sebastian Vasquez</p>
            <div class="fun-slider">
              <button class="btn-ver">VER AHORA</button>
              <div class="circles-slider">
                <span />
                <span />
              </div>
              <button class="btn-replay" />
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
</section>

<style>
  .bg-slider {
    width: 100%;
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: green;
  }

  .cont-img-slider {
    width: 100vw;
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: start;
    overflow-x: auto;
    overflow-y: hidden;
  }

  .sec-imgs {
    width: 100%;
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
    bottom: 0;
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
  }

  .circles-slider {
    width: 30%;
    display: flex;
    align-items: center;
    justify-content: space-evenly;
  }

  .circles-slider span {
    width: 10px;
    height: 10px;
    border-radius: 50%;
    background-color: white;
  }

  .btn-replay {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    background-color: #040031;
    border: none;
  }
</style>
