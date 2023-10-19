<script>
  import logoFilmin from "../img/logo-filmin.png";
  import flecha from "../img/icon-flecha-01.svg";
</script>

<header>
  <section class="space-nav" >
    <img src={logoFilmin} alt="logo-filmin" />
    <nav>
      <a href="/">Inicio</a>
      <a href="/">Películas</a>
      <a href="/">Series</a>
      <a href="/">Colecciones</a>
      <a href="/">Festivales</a>
      <a href="/">Kids</a>
      <a href="/">
        más
        <img src={flecha} alt="flecha-icon" class="i-flecha" />
      </a>
    </nav>
  </section>
  <section class="space-buttons" >
    <button class="btn-registro" >REGISTRO</button>
    <button class="btn-inicio" >INICIAR SESION</button>
  </section>
</header>


<style>
  header {
    width: 100%;
    height: 250px;
    display: flex;
    align-items: flex-start;
    justify-content: space-around;
    padding-top: 30px;
    background: linear-gradient(to bottom, #00103d, #00103d00);
    position: absolute;
    top: 0;
    z-index: 100;
  }

  .space-nav{
    width: 70%;
    display: flex;
    align-items: center;
    justify-content:flex-start;
    gap: 30px;
    padding-left: 30px;
  }

  img {
    width: 20%;
  }

  nav{
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 15px;
  }

  nav a{
    text-decoration: none;
    color: white;
    letter-spacing: 0.5px;
  }

  nav a:last-child{
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .i-flecha{
    width: 13px;
    margin-left: 5px;
    margin-top: 3px;
  }

  .space-buttons{
    width: 30%;
    display: flex;
    align-items: center;
    justify-content: flex-end;
    padding-right: 40px;
    gap: 12px;
  }

  .btn-registro{
    padding: 10px 15px;
    border: none;
    background-color: #00FF9E;
    color: black;
    border-radius: 5px;
    font-size:0.9rem;
    cursor: pointer;
  }

  .btn-registro:hover{
    background-color:white;
  }

  .btn-inicio{
    padding: 10px 15px;
    border: 2px solid white;
    color: white;
    background-color:transparent;
    border-radius: 5px;
    font-size:0.9rem;
    cursor: pointer;
  }

  .btn-inicio:hover{
    background-color:white;
    color: black;
  }


  
</style>
