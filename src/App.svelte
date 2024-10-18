<script>
  import { onMount } from "svelte";
  import axios from "axios";

  let characters = [];

  //obtener los personajes
  const fetchCharacters = async () => {
    try {
      const response = await axios.get(
        "https://rickandmortyapi.com/api/character"
      );
      characters = response.data.results; //almacena los resultados
    } catch (e) {
      console.error("Error: ", e);
    }
  };

  //cargar a los personajes
  onMount(() => {
    fetchCharacters();
  });
</script>

<style>
  .card {
    transition: transform 0.2s; /* Transición suave */
  }

  .card:hover {
    transform: scale(1.05); /* Efecto de zoom al pasar el mouse */
  }
</style>

<div class="container mt-4">
  <h1 class="text-center mb-4">Rick and Morty</h1>
  <div class="row">
    {#each characters as character}
      <div class="col-md-4 mb-4 col-sm-6 mb-4">
        <div class="card shadow border-light">
          <img
            src={character.image}
            class="card-img-top"
            alt={character.name}
          />
          <div class="card-body">
            <h5 class="card-title">{character.name}</h5>
          </div>
        </div>
      </div>
    {/each}
  </div>
</div>
