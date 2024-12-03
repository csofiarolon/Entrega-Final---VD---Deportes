<script>
  export let atleta = {};
  
</script>

<div class="grid-container">
  <div class="cabeza">
    <img src="/images/Cabeza.svg" alt="Cabeza" />
  </div>
  <div class="torso" 
  class:coreMax={atleta.Core > 66}
  class:coreMed={atleta.Core >= 33 && atleta.Core < 66}
  class:coreMin={atleta.Core < 33}
  >
    {#if atleta.Espalda_Hombros < 33}
      <img src="/images/Torzo minimun.svg" alt="Torso" />
    {:else if atleta.Espalda_Hombros < 66}
      <img src="/images/Torzo medium.svg" alt="Torso" />
    {:else}
      <img src="/images/Torzo maximun.svg" alt="Torso" />
    {/if}
  </div>
  <div class="brazo-izquierdo">
    {#if atleta.Brazos < 33}
      <img
        src="public/images/Brazo izq min.svg"
        alt="brazo"
        style="width: 50%;"
      />
    {:else if (atleta.Brazos >= 33 && atleta.Brazos < 66)}
      <img
        src="public/images/Brazo izq med.svg"
        alt="brazo"
        style="width: 70%;"
      />
    {:else}
      <img src="public/images/Brazo izq max.svg" alt="brazo" />
    {/if}
  </div>
  <div class="brazo-derecho">
    {#if atleta.Brazos < 33}
      <img
        src="public/images/Brazo der min.svg"
        alt="brazo"
        style="width: 50%;"
      />
    {:else if (atleta.Brazos >= 33 && atleta.Brazos < 66)}
      <img
        src="public/images/Brazo der med.svg"
        alt="brazo"
        style="width: 70%;"
      />
    {:else}
      <img src="public/images/Brazo der max.svg" alt="brazo" />
    {/if}
  </div>
  <div class="piernas">
    {#if atleta.Piernas < 67}
      <img src="public/images/Piernas min.svg" alt="brazo" />
    {:else if (atleta.Piernas >= 67 && atleta.Piernas < 84)}
      <img src="public/images/Piernas med.svg" alt="brazo" />
    {:else}
      <img src="public/images/Piernas max.svg" alt="brazo" />
    {/if}
  </div>
</div>

<style>
  .grid-container {
    display: grid;
    grid-template-columns: 22.5% 55% 22.5%;
    grid-template-rows: 15% 32% 53%;
    width: 100px;
    height: 200px;
    margin-left: 19%;
  }

  .cabeza,
  .torso,
  .brazo-izquierdo,
  .brazo-derecho,
  .piernas {
    display: flex;
    justify-content: center;
    align-items: center;
    /* border: 1px dashed black; */
  }

  .cabeza {
    grid-column: 2 / 3;
    grid-row: 1 / 2;
  }

  .torso {
    grid-column: 2 / 3;
    grid-row: 2 / 3;
    align-items: start;
  }

  .brazo-izquierdo {
    grid-column: 1 / 2;
    grid-row: 2 / 4;
    align-items: start;
  }

  .brazo-derecho {
    grid-column: 3 / 4;
    grid-row: 2 / 4;
    align-items: start;
  }

  .piernas {
    grid-column: 2 / 3;
    grid-row: 3 / 4;
  }

  /* Imagenes */
  .torso img {
    height: 100%;
  }
  .cabeza img {
    height: 100%;
  }
  .piernas img {
    height: 100%;
  }

  /* Coloreado */
  .coreMax {
    filter: invert(100%) sepia(100%) saturate(600%) hue-rotate(310deg) brightness(100%) contrast(110%);
}



.coreMed {
  
  filter: invert(20%) sepia(100%) saturate(500%) hue-rotate(298deg) brightness(196%) contrast(110%);



}


.coreMin {
  
  filter: invert(100%) sepia(40%) saturate(400%) hue-rotate(260deg) brightness(50%) contrast(720%);

}


</style>
