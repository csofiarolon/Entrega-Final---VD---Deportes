<script>
  import * as d3 from "d3";

  //importamos los JSONS con los datos
  import atletas from "/src/data/Musculo porcentaje.json";

  import Cuerpo from "./Cuerpo.svelte";

  let slider1 = 0; // El valor del slider, desde 0 hasta 100
  let slider2 = 0; // El valor del slider, desde 0 hasta 100
  let slider3 = 0; // El valor del slider, desde 0 hasta 100

  // Función para calcular la extensión de la línea superior
  const calculateWidth = (value) => {
    return (value / 100) * 150; // Esto hace que la línea superior crezca hasta 150px
  };

  let orden = "todos";
  let muscOrden = [];

  const sortMusculo = () => {
    // Ordenar de mayor a menor por valores de cada músculo
    if (orden == "todos") {
      muscOrden = d3.sort(atletas, (a) => a.Deporte);
    } else if (orden == "brazos") {
      muscOrden = d3.sort(atletas, (a) => a.Brazos);
    } else if (orden == "pierna") {
      muscOrden = d3.sort(atletas, (a) => a.Piernas);
    } else if (orden == "core") {
      muscOrden = d3.sort(atletas, (a) => a.Core);
    } else if (orden == "espalda") {
      muscOrden = d3.sort(atletas, (a) => a.Espalda_Hombros);
    }
  };
  sortMusculo();
</script>

<main>
  <div class="header">
    <h3 class="headline">
      <b>El deporte como escultura corporal</b>
    </h3>
    <p class="bajada">
      El deporte ha moldeado los cuerpos de las personas desde hace muchos años.
      Acompáñanos a ver los cambios corporales según los deportes de alto
      rendimiento.
    </p>
  </div>

  <!-- <h2 class="subtitulo">Desarrollo muscular deportivo - Referencias</h2> -->
  <br />
  <img
    src="public/images/Refe primer graf.png"
    alt="referencias primer grafico"
    style="width: 50%; align-content:center; display:block; margin-left: auto; margin-right:auto;"
  />
  <br />
  <br />
  <h2 class="subtitulo">Los músculos por deporte</h2>
  <p class="bajadita">
    Cada deporte requiere el desarrollo de distintos grupos musuclares y es por
    esto que los atletas tienen cuerpos tan diferentes.
  </p>

  <!--BOTONES-->

  <div class="botones">
    <button
      class="MiBoton1"
      class:active={orden === "todos"}
      on:click={() => {
        orden = "todos";
        sortMusculo();
      }}
      >Todos
    </button>
    <button
      class="MiBoton1"
      class:active={orden === "brazos"}
      on:click={() => {
        orden = "brazos";
        sortMusculo();
      }}
      >Brazos
    </button>
    <button
      class="MiBoton1"
      class:active={orden === "espalda"}
      on:click={() => {
        orden = "espalda";
        sortMusculo();
      }}
      >Espalda
    </button>
    <button
      class="MiBoton1"
      class:active={orden === "pierna"}
      on:click={() => {
        orden = "pierna";
        sortMusculo();
      }}
      >Piernas
    </button>
    <button
      class="MiBoton1"
      class:active={orden === "core"}
      on:click={() => {
        orden = "core";
        sortMusculo();
      }}
      >Abdomen
    </button>
  </div>

  <!-- Grafico principal de atletas -->

  <div class="coffes-container">
    {#each muscOrden as a}
      <div class="column-wrapper">
        <Cuerpo atleta={a} />
        <p id="deporte">{a.Deporte}</p>
      </div>
    {/each}
  </div>

  <br />
  <br />
  <br />
  <h2 class="subtitulo">Estadísticas deportivas</h2>
  <p class="bajadita">
    Los deportes tienen distintos niveles de fuerza, velocidad máxima y
    resistencia aeróbica que influyen el moldeado del atleta.
  </p>

  <div
    style="min-height:685px; display:block; margin-left: auto; margin-right:auto; margin-top: 5%;"
    id="datawrapper-vis-zxWxj"
  >
    <script
      type="text/javascript"
      defer
      src="https://datawrapper.dwcdn.net/zxWxj/embed.js"
      charset="utf-8"
      data-target="#datawrapper-vis-zxWxj"
    ></script><noscript
      ><img
        src="https://datawrapper.dwcdn.net/zxWxj/full.png"
        alt="Heatmap"
      /></noscript
    >
  </div>

  <!-- Slider para controlar la deformación 
  <div class="container">
    <div
      class="rectangle"
      style="clip-path: polygon(50% 0%, {50 -
        calculateWidth(sliderValue) / 2}% 100%, {50 +
        calculateWidth(sliderValue) / 2}% 100%);"
    ></div>
  </div>
  <input
    type="range"
    min="35"
    max="100"
    bind:value={sliderValue}
    class="slider"
  /> -->
  <p class="queatletasos">Qué atleta sos?</p>
  <p class="enquedeporte">
    En qué deporte inscribirte en las próximas olimpiadas?
  </p>
  <p class="kilos">Cuántos kilos levantás con los brazos?</p>


<div class="contenedortodo">


  <div class="container">
    <!-- 1ER SLIDER -->

    <input
      type="range"
      min="0"
      max="100"
      bind:value={slider1}
      class="slideruno"
    />

    <div class="slider-ticks1">
      <svg width="100%" height="40">
        <g transform="translate(0, 10)">
          <!-- Generate tick marks -->
          {#each d3.range(1, 11) as tick}
            <line
              x1="{(tick - 1) * 10}%"
              x2="{(tick - 1) * 10}%"
              y1="0"
              y2="10"
              stroke="black"
              stroke-width="1"
            ></line>
            <!-- Tick labels -->
            <text
              x="{(tick - 1) * 10}%"
              y="25"
              text-anchor="middle"
              font-size="12px"
              fill="black"
            >
              {tick}
            </text>
          {/each}
        </g>
      </svg>
    </div>
  <!-- final contenedor sliders -->

  <div class="kilosabajo">
    <p class="unkilo">1 kilo :(</p>
    <p class="diezkilo">10 kilos <br /> soy re capo</p>
  </div>

  <!-- 2DO SLIDER -->

  <p class="kilos">Qué tan rápido corrés?</p>

  <input
    type="range"
    min="0"
    max="100"
    bind:value={slider2}
    class="sliderdos"
  />

  <div class="slider-ticks1">
    <svg width="100%" height="40">
      <g transform="translate(0, 10)">
        <!-- Generate tick marks -->
        {#each d3.range(1, 11) as tick}
          <line
            x1="{(tick - 1) * 10}%"
            x2="{(tick - 1) * 10}%"
            y1="0"
            y2="10"
            stroke="black"
            stroke-width="1"
          ></line>
          <!-- Tick labels -->
          <text
            x="{(tick - 1) * 10}%"
            y="25"
            text-anchor="middle"
            font-size="12px"
            fill="black"
          >
            {tick}
          </text>
        {/each}
      </g>
    </svg>
  </div>

  <div class="kilosabajo">
    <p class="unkilo">muy despacio soy una tortuga</p>
    <p class="diezkilo">Colapinto es lento a mi lado</p>
  </div>

  <!-- 3ER SLIDER -->

  <p class="kilos">Cuántas cuadras corrés sin cansarte?</p>

  <input
    type="range"
    min="0"
    max="100"
    bind:value={slider3}
    class="slidertres"
  />

  <div class="slider-ticks1">
    <svg width="100%" height="40">
      <g transform="translate(0, 10)">
        <!-- Generate tick marks -->
        {#each d3.range(1, 11) as tick}
          <line
            x1="{(tick - 1) * 10}%"
            x2="{(tick - 1) * 10}%"
            y1="0"
            y2="10"
            stroke="black"
            stroke-width="1"
          ></line>
          <!-- Tick labels -->
          <text
            x="{(tick - 1) * 10}%"
            y="25"
            text-anchor="middle"
            font-size="12px"
            fill="black"
          >
            {tick}
          </text>
        {/each}
      </g>
    </svg>
  </div>

  <div class="kilosabajo">
    <p class="unkilo">no aguanto <br /> una cuadra :(</p>
    <p class="diezkilo">más de 10 <br /> me la re banco</p>
  </div>


</div>


  <div class="result">
    {#if slider1 >= 0 && slider1 < 20 && slider2 >= 33 && slider2 < 49 && slider3 >= 80 && slider3 <= 99}
      <p>Gimnasia Piso</p>
      <img src="/images/gimnasia piso.png" alt="Grafico" />
    {:else if slider1 >= 0 && slider1 < 20 && slider2 >= 65 && slider2 <= 80 && slider3 >= 60 && slider3 <= 79}
      <p>Hockey sobre Césped</p>
      <img src="/images/Hockey.png" alt="Grafico" />
    {:else if slider1 >= 20 && slider1 < 40 && slider2 >= 49 && slider2 <= 64 && slider3 >= 80 && slider3 <= 99}
      <p>Natación</p>
      <img src="/images/natacion.png" alt="Grafico" />
    {:else if slider1 >= 20 && slider1 < 40 && slider2 >= 81 && slider2 <= 100 && slider3 >= 40 && slider3 <= 59}
      <p>Carreras de Velocidad</p>
      <img src="/images/Carrera de velocidad.png" alt="Grafico" />
    {:else if slider1 >= 20 && slider1 < 40 && slider2 >= 65 && slider2 <= 80 && slider3 >= 60 && slider3 <= 79}
      <p>Fútbol</p>
      <img src="/images/futbol.png" alt="Grafico" />
    {:else if slider1 >= 40 && slider1 < 60 && slider2 >= 17 && slider2 <= 32 && slider3 >= 20 && slider3 <= 39}
      <p>Lanzamiento de Disco</p>
      <img src="/images/Lanzamiento de disco.png" alt="Grafico" />
    {:else if slider1 >= 60 && slider1 < 80 && slider2 >= 0 && slider2 < 17 && slider3 >= 20 && slider3 <= 39}
      <p>Lanzamiento de Martillo</p>
      <img src="/images/Lanzamiento de martillo.png" alt="Grafico" />
    {:else if slider1 >= 80 && slider1 < 100 && slider2 >= 17 && slider2 <= 32 && slider3 >= 0 && slider3 < 20}
      <p>Lanzamiento de Peso</p>
      <img src="/images/Lanzamiento de pesas.png" alt="Grafico" />
    {:else if slider1 >= 80 && slider1 < 100 && slider2 >= 17 && slider2 <= 32 && slider3 >= 20 && slider3 <= 39}
      <p>Lanzamiento de Jabalina</p>
      <img src="/images/Lanzamiento de jabalina.png" alt="Grafico" />
    {:else if slider1 >= 20 && slider1 < 40 && slider2 >= 17 && slider2 <= 32 && slider3 >= 40 && slider3 <= 59}
      <p>Gimnasia Barras</p>
      <img src="/images/gimnasia barras.png" alt="Grafico" />
    {:else if slider1 >= 30 && slider1 < 50 && slider2 >= 33 && slider2 <= 48 && slider3 >= 40 && slider3 <= 59}
      <p>Carreras de Larga Distancia</p>
      <img src="/images/Carreras de larga distancia.png" alt="Grafico" />
    {:else if slider1 >= 40 && slider1 < 60 && slider2 >= 49 && slider2 <= 64 && slider3 >= 40 && slider3 <= 59}
      <p>Carreras de Media Distancia</p>
      <img src="/images/carreras de media distancia.png" alt="Grafico" />
    {:else if slider1 >= 30 && slider1 < 50 && slider2 >= 49 && slider2 <= 64 && slider3 >= 40 && slider3 <= 59}
      <p>Básquetbol</p>
      <img src="/images/Basquetbol.png" alt="Grafico" />
    {/if}
  </div>

</div>

</main>

<style>
  /* Estilos del contenedor del rectángulo */
  /*
  
    */

  /* Estilos del rectángulo */

  /*
  .rectangle {
    position: absolute;
    top: 50px; /* Desplaza el rectángulo hacia abajo 
    left: 0;
    width: 100%;
    height: 100%;
    background-color: #3498db;
    transition:
      clip-path 0.3s ease,
      transform 0.3s ease;
    transform: rotate(180deg); /* Aquí aplicas la rotación 
  }

  */

  /* Slider */
  /*
  .slider {
    width: 100%;
    margin-top: 20px;
  }
    */

    .contenedortodo{
      position: relative;
      display: grid; /* Activa CSS Grid */
  grid-template-columns: 1fr 1fr; /* Dos columnas iguales */
  height: 600px; /* Alto del contenedor */

    }
    
  .result {
    position: absolute;
    text-align: left;
    font-size: 30px;
    font-family: Jaro;
    color: #7107aa;
    width: 500px;
  flex-shrink: 0;
  }

  .unkilo {
    text-align: left;
   width: 95px;
    word-wrap: break-word; /* También puedes usar overflow-wrap: break-word */
    overflow-wrap: break-word;
  }

  .diezkilo {
    text-align: right;
    white-space: normal;
    overflow: visible;
    margin-left: 80px;
    margin-right: 20px;
  }

  .kilosabajo {
    display: flex;
    text-align: right;
    gap: 390px;
    margin-left: 650px;
    color: #0258a9;
    white-space: normal;
    overflow: visible;
    font-size: 10px;
    margin-bottom: 0px;
  }

  .kilos {
    display: flex;
    justify-content: left;
    margin-top: 0;
    width: 100%;
    margin-top: 20px;
    margin-left: 645px;
    margin-bottom: 0px;
    font-size: 30px;
    font-family: Jaro;
    color: #0258a9;
  }

  .queatletasos {
    font-size: 50px;
    font-family: Jaro;
    color: #0258a9;
  }

  .enquedeporte {
    font-family: Inter;
    color: #0258a9;
    font-size: 20px;
  }

  .slideruno {
    width: 47%;
    margin-top: 20px;
    margin-left: 645px;
    height: 20px;
  }

  .sliderdos {
    width: 47%;
    margin-top: 20px;
    margin-left: 645px;
    height: 20px;
  }

  .slidertres {
    width: 47%;
    margin-top: 20px;
    margin-left: 645px;
    height: 20px;
  }

  .slider-ticks1 {
    display: flex;
    justify-content: center;
    margin-top: 0;
    width: 100%;
    margin-top: -10px;
    margin-left: 350px;
  }

  .slider-ticks1 svg {
    width: 50%; /* Matches the width of your slider */
  }

  .bajadita {
    font-family: Inter;
    color: #0258a9;
    font-size: 20px;
    text-align: center;
    max-width: 60%;
    margin-right: auto;
    margin-left: auto;
  }

  .MiBoton1 {
    margin: 0;
  }

  #deporte {
    font-family: Inter;
    color: #0258a9;
    font-size: 15px;
    text-align: center;
  }

  .subtitulo {
    font-family: Jaro;
    color: #0258a9;
    text-align: center;
    margin-top: 2%;
  }

  .coffes-container {
    display: flex;
    flex-wrap: wrap;
    gap: 80px;
    row-gap: 70px;
    justify-content: center;
  }
  .column-wrapper {
    position: relative;
    width: 160px;
    height: 200px;
  }

  .header {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    /* margin-top: 20px;
  margin-bottom: 80px; */
  }
  .headline {
    font-size: 80px;
    font-family: Jaro;
    line-height: 1.2;
    text-align: center;
    margin-top: 0px;
    color: #0258a9;
    margin-bottom: 10px;
  }
  .bajada {
    font-size: 24px;
    font-family: Inter;
    text-align: center;
    color: #0258a9;
    margin-top: 0px;
    width: 85%;
    margin-bottom: 30px;
  }

  .botones {
    display: flex;
    gap: 10px;
    justify-content: center;
    /* margin-left: 23%; */
    margin-top: 3%;
    margin-bottom: 3%;
    align-items: center;
    align-content: center;
  }

  .MiBoton1:hover {
    background-color: #80c1f7;
    color: #c2e1fb;
  }

  .MiBoton1 {
    width: 10%;
    height: 30px;
    background-color: #c2e1fb;
    color: #0258a9;
    display: flex;
    justify-content: center; /* Centrado horizontal */
    align-items: center; /* Centrado vertical */
    border-radius: 5px;
    border: 1.4px, solid, #0258a9;
    font-size: 100%;
  }

  .active {
    width: 10%;
    height: 30px;
    background-color: #0258a9;
    color: #f2f8ff;
    display: flex;
    justify-content: center; /* Centrado horizontal */
    align-items: center; /* Centrado vertical */
    border-radius: 5px;
  }
</style>
