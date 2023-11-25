<script>
  import Header from './components/Header.svelte'
  import Slider from './components/Slider.svelte'
  import Movies from './components/Movies.svelte'
  import Top from './components/Top.svelte'
</script>

<main  class="main">
  <Header/>
  <Slider/>
  <Movies/>
  <Top/>
</main>


<style>
  .main{
    padding-bottom: 80px;
    background-color: #00103d;
  }
</style>