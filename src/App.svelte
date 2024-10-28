<script>
  import * as d3 from "d3"
  //import diseñadoras from "/src/data/diseñadoras.csv"
  import diseñadoras from "/src/data/diseñadoras.json"

  console.log("diseñadoras", diseñadoras)
  
    // Función para obtener el intervalo de consagración
    function getConsagracionInterval(anio) {
    if (anio >= 1930 && anio <= 1939) return "1930 - 1939";
    if (anio >= 1940 && anio <= 1949) return "1940 - 1949";
    if (anio >= 1950 && anio <= 1959) return "1950 - 1959";
    if (anio >= 1960 && anio <= 1969) return "1960 - 1969";
    if (anio >= 1970 && anio <= 1979) return "1970 - 1979";
    if (anio >= 1980 && anio <= 1999) return "1980 - 1999";
    if (anio >= 2000 && anio <= 2009) return "2000 - 2009";
    if (anio >= 2010 && anio <= 2019) return "2010 - 2019";
  }

  const ordenIntervalos = [
  "1930 - 1939",
  "1940 - 1949",
  "1950 - 1959",
  "1960 - 1969",
  "1970 - 1979",
  "1980 - 1999",
  "2000 - 2009",
  "2010 - 2019"
];

// Agrupar diseñadoras por intervalo de consagración
  const diseñadorasAgrupadas = d3.group(diseñadoras, d => getConsagracionInterval(d["Anio de consagracion"]));

  const imagesacademicauno = {
    "Formacion tecnica": "./images/tecnicauno.svg",
    "Escuela de disenio": "./images/escuelauno.svg",
    "Universitaria": "./images/universitariauno.svg",
    "Autodidacta": "./images/autodidactauno.svg"
  };

  const imagesacademicados = {
    "Formacion tecnica": "./images/tecnicados.svg",
    "Escuela de disenio": "./images/escuelados.svg",
    "Universitaria": "./images/universitariados.svg",
    "Autodidacta": "./images/autodidactados.svg"
  };


  const imagesnacionalidaduno = {
   "America del norte": "./images/americadelnorteuno.svg",
    "Europa": "./images/europauno.svg",
    "Latinoamerica": "./images/latinoamericauno.svg",
    "Medio oriente": "./images/medioorienteuno.svg"
  };

  const imagesnacionalidaddos = {
    "America del norte": "./images/americadelnortedos.svg",
    "Europa": "./images/europados.svg",
    "Latinoamerica": "./images/latinoamericados.svg",
    "Medio oriente": "./images/medioorientedos.svg"
  };

  const imagenesmarido = {
    "Si":"./images/maridosi.svg",
    "No":"./images/maridono.svg"
  }

  const imagesaños = {
    "1870 - 1889 rojo": "./images/1870 - 1889 rojo.svg",
    "1890 - 1899 rojo": "./images/1890 - 1899 rojo.svg",
    "1900 - 1919 rojo": "./images/1900 - 1919 rojo.svg",
    "1920 - 1939 rojo": "./images/1920 - 1939 rojo.svg",
    "1940 - 1959 rojo": "./images/1940 - 1959 rojo.svg",
    "1960 - 1979 rojo": "./images/1960 - 1979 rojo.svg",
    "1980 - 1999 rojo": "./images/1980 - 1999 rojo.svg",

    "1870 - 1889 rosa": "./images/1870 - 1889 rosa.svg",
    "1890 - 1899 rosa": "./images/1890 - 1899 rosa.svg",
    "1900 - 1919 rosa": "./images/1900 - 1919 rosa.svg",
    "1920 - 1939 rosa": "./images/1920 - 1939 rosa.svg",
    "1940 - 1959 rosa": "./images/1940 - 1959 rosa.svg",
    "1960 - 1979 rosa": "./images/1960 - 1979 rosa.svg",
    "1980 - 1999 rosa": "./images/1980 - 1999 rosa.svg",

    "1870 - 1889 azul": "./images/1870 - 1889 azul.svg",
    "1890 - 1899 azul": "./images/1890 - 1899 azul.svg",
    "1900 - 1919 azul": "./images/1900 - 1919 azul.svg",
    "1920 - 1939 azul": "./images/1920 - 1939 azul.svg",
    "1940 - 1959 azul": "./images/1940 - 1959 azul.svg",
    "1960 - 1979 azul": "./images/1960 - 1979 azul.svg",
    "1980 - 1999 azul": "./images/1980 - 1999 azul.svg",

    "1870 - 1889 ver": "./images/1870 - 1889 ver.svg",
    "1890 - 1899 ver": "./images/1890 - 1899 ver.svg",
    "1900 - 1919 ver": "./images/1900 - 1919 ver.svg",
    "1920 - 1939 ver": "./images/1920 - 1939 ver.svg",
    "1940 - 1959 ver": "./images/1940 - 1959 ver.svg",
    "1960 - 1979 ver": "./images/1960 - 1979 ver.svg",
    "1980 - 1999 ver": "./images/1980 - 1999 ver.svg",

    "1870 - 1889 ama": "./images/1870 - 1889 ama.svg",
    "1890 - 1899 ama": "./images/1890 - 1899 ama.svg",
    "1900 - 1919 ama": "./images/1900 - 1919 ama.svg",
    "1920 - 1939 ama": "./images/1920 - 1939 ama.svg",
    "1940 - 1959 ama": "./images/1940 - 1959 ama.svg",
    "1960 - 1979 ama": "./images/1960 - 1979 ama.svg",
    "1980 - 1999 ama": "./images/1980 - 1999 ama.svg"
};


  // Escala para ajustar tamaños de los cuadros basados en "Cantidad de obras"
  const maxObras = d3.max(diseñadoras, (d) => d["Cantidad de obras"]);
  const squareSizeScale = d3.scaleLinear()
    .domain([0, maxObras])
    .range([150, 300]); // Tamaños mínimos y máximos para los cuadros e imágenes

// Función para calcular el tamaño basado en la cantidad de obras
function getSize(cantidadObras) {
    return squareSizeScale(cantidadObras);
  }

 // Función para obtener el rango de años basado en el "Anio de nacimiento"
 function getYearRange(anio) {
    if (anio >= 1870 && anio <= 1889) return "1870 - 1889";
    if (anio >= 1890 && anio <= 1899) return "1890 - 1899";
    if (anio >= 1900 && anio <= 1919) return "1900 - 1919";
    if (anio >= 1920 && anio <= 1939) return "1920 - 1939";
    if (anio >= 1940 && anio <= 1959) return "1940 - 1959";
    if (anio >= 1960 && anio <= 1979) return "1960 - 1979";
    if (anio >= 1980 && anio <= 1999) return "1980 - 1999";
  
  }

  

  // Función para obtener el color basado en el "Tipo de diseno"
  function getColorPorTipoDiseño(type) {
    switch (type) {
      case "Industrial":
        return "rojo";
      case "Grafico":
        return "rosa";
      case "Mobiliario":
        return "azul";
      case "Textil":
        return "ama";
      case "Interiores":
        return "ver";
    }
  }

  // Función para obtener la imagen del año basado en el tipo de diseño y el año de consagración
  function getImageAños(diseñadora) {
    const yearRange = getYearRange(diseñadora["Anio de nacimiento"]);
    const designTypeColor = getColorPorTipoDiseño(diseñadora["Tipo de diseno"]);
    const key = `${yearRange} ${designTypeColor}`;
    return imagesaños[key] 
  }


</script>

<arriba class="header-imagen">
  <img src="./images/header.svg" alt="Imagen Header">
</arriba>

<header> 
  <div class="titulo" >
<h1>Diseñadoras Consagradas </h1>
<p class="bajada">A través de un mosaico visual, se destacan las trayectorias y contribuciones de mujeres que han transformado el mundo del diseño, desde la arquitectura y el mobiliario hasta la moda y el arte industrial. Cada fragmento del mosaico cuenta una historia de innovación, creatividad y la influencia que estas visionarias han dejado en la historia del arte y el diseño contemporáneo.</p>

  </div></header>

  <h4> ( Fatima Pauluk & Zoe Gaspar )</h4>
<main>
 
  <div class="referencias">
    <p class="tituloref">REFERENCIAS</p>
    
    <!-- container para todas las secciones de las referencias -->
    <div class="grid-referencias">
      <!-- Fila 1: Nacionalidad y Educación -->
      <div class="row-container top-row">
        <!-- Nacionalidad -->
        <div class="ref-section nacionalidad">
          <h3 class="ref-title">Nacionalidad</h3>
          <div class="ref-icons">
            <div class="icon-item">
              <img src="./images/latinoamerica.svg" alt="Latinoamérica" />
              <span>Latinoamérica</span>
            </div>
            <div class="icon-item">
              <img src="./images/americadelnorte.svg" alt="América del Norte" />
              <span>América del Norte</span>
            </div>
            <div class="icon-item">
              <img src="./images/medioriente.svg" alt="Medio Oriente" />
              <span>Medio Oriente</span>
            </div>
            <div class="icon-item">
              <img src="./images/europa.svg" alt="Europa" />
              <span>Europa</span>
            </div>
          </div>
        </div>
  
        <!-- Educación -->
        <div class="ref-section educacion">
          <h3 class="ref-title">Educación</h3>
          <div class="ref-icons">
            <div class="icon-item">
              <img src="./images/tecnica.svg" alt="Técnica" />
              <span>Técnica</span>
            </div>
            <div class="icon-item">
              <img src="./images/escuela.svg" alt="Escuela de diseño" />
              <span>Escuela de diseño</span>
            </div>
            <div class="icon-item">
              <img src="./images/universitaria.svg" alt="Universitaria" />
              <span>Universitaria</span>
            </div>
            <div class="icon-item">
              <img src="./images/autodidacta.svg" alt="Autodidacta" />
              <span>Autodidacta</span>
            </div>
          </div>
        </div>
      </div>
  
      <!-- Fila 2: Año de nacimiento -->
      <div class="row-container middle-row">
        <div class="ref-section nacimiento">
          <h3 class="ref-title">Año de nacimiento</h3>
          <div class="birth-years-container">
            <div class="birth-year-grid">
              <img src="./images/añodenacimiento1.svg" alt="Año de nacimiento" />
              <span>1870 - 1889</span>
            </div>
            <div class="birth-year-grid">
              <img src="./images/añodenacimiento2.svg" alt="Año de nacimiento" />
              <span>1890 - 1899</span>
            </div>
            <div class="birth-year-grid">
              <img src="./images/añodenacimiento3.svg" alt="Año de nacimiento" />
              <span>1900 - 1919</span>
            </div>
            <div class="birth-year-grid">
              <img src="./images/añodenacimiento4.svg" alt="Año de nacimiento" />
              <span>1920 - 1939</span>
            </div>
            <div class="birth-year-grid">
              <img src="./images/añodenacimiento5.svg" alt="Año de nacimiento" />
              <span>1940 - 1959</span>
            </div>
            <div class="birth-year-grid">
              <img src="./images/añodenacimiento6.svg" alt="Año de nacimiento" />
              <span>1960 - 1979</span>
            </div>
            <div class="birth-year-grid">
              <img src="./images/añodenacimiento 7.svg" alt="Año de nacimiento" />
              <span>1980 - 1999</span>
            </div>
          </div>
        </div>
      </div>

  <!-- Fila 3: Tipo de diseño -->
  <div class="row-container middle-row">
    <div class="ref-section tipo-diseno">
      <h3 class="ref-title">Tipo de diseño</h3>
      <div class="design-type-container">
        <div class="color-box industrial">
          <span>Industrial</span>
        </div>
        <div class="color-box grafico">
          <span>Gráfico</span>
        </div>
        <div class="color-box mobiliario">
          <span>Mobiliario</span>
        </div>
        <div class="color-box textil">
          <span>Textil</span>
        </div>
        <div class="color-box interiores">
          <span>Interiores</span>
        </div>
      </div>
    </div>
  </div>
      <!-- Fila 4: Cantidad de obras y Marido -->
      <div class="row-container bottom-row">
        <div class="ref-section obras">
          <h3 class="ref-title">Cantidad de obras expuestas en el MoMa</h3>
          <div class="size-container">
            <img src="./images/referenciasobrasexpuestas.svg" alt="referencia tamaño" />
            <span class="size-description">A mayor tamaño, mayor cantidad de obras expuestas.</span>
          </div>
        </div>
  
        <div class="ref-section marido">
          <h3 class="ref-title">Marido que obtuvo más reconocimiento que ella</h3>
          <div class="marido-container">
            <img src="./images/estrella-grande.svg" alt="Marido con más reconocimiento" />
            <span class="marido-description">Este símbolo indica si su esposo obtuvo más reconocimiento en el campo del diseño a pesar de haber diseñado conjuntamente.</span>
          </div>
        </div>
      </div>
    </div>
  </div>
  



    <div class="timeline-container">
    <div class="timeline-header">
      <h1>Años en los que las diseñadoras <br>fueron consagradas en el MoMa</h1>
      <hr class="header-line">
    </div>


    {#each ordenIntervalos as intervalo}
    {#if diseñadorasAgrupadas.has(intervalo)}
      <div class="decade-group">
        <div class="decade-row">
          <h2 class="year-label">{intervalo}</h2>
          <div class="designers-row">
            {#each diseñadorasAgrupadas.get(intervalo) as diseñadora}
              <div class="mosaico" style="width: {getSize(diseñadora["Cantidad de obras"])}px; height: {getSize(diseñadora["Cantidad de obras"])}px;">
                <div class="tamaño" style="width: {getSize(diseñadora["Cantidad de obras"])}px; height: {getSize(diseñadora["Cantidad de obras"])}px;">
                  <img class="fondo" src={imagesacademicauno[diseñadora["Formacion academica uno"]]} alt="educacion uno" />
                  <img class="fondo" src={imagesacademicados[diseñadora["Formacion academica dos"]]} alt="educacion dos" />
                  <img class="fondo" src={imagesnacionalidaduno[diseñadora["Nacionalidad uno"]]} alt="nacionalidad uno" />
                  <img class="fondo" src={getImageAños(diseñadora)} alt="imagen por año y diseño" />
                  <img class="fondo" src={imagenesmarido[diseñadora["Marido famoso"]]} alt="maridos" />
                  <img class="fondo" src={imagesnacionalidaddos[diseñadora["Nacionalidad dos"]]} alt="nacionalidad dos" />
                </div>
                <p>{diseñadora.Nombre}</p>
              </div>
            {/each}
          </div>
        </div>
      </div>
    {/if}
  {/each}

</main>

<footer>
  <div class="footer">
  </div>
</footer>



<style>

@import url('https://fonts.googleapis.com/css2?family=Instrument+Sans:ital,wght@0,400..700;1,400..700&display=swap');

:global(body) {
  font-family: "Instrument Sans", sans-serif;
  }

main {
    background-color: #FCFDF7;
  margin-left: 80px;
             
}

.timeline-container {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  margin-left: 0px;
  position: relative;
  margin-bottom: 20px;
}


.timeline-header {
  text-align: center;
  margin-bottom: 70px;
  background-color: #FCFDF7;
  z-index: 2;

}

.timeline-header h1 {
  font-size: 20pt;
  font-weight: bold;
  color: #000000;
  margin-top: 100px;
}

.header-line {
  width: 100%;
  height: 2px;
  background-color: #000000;
 
}


.decade-group {
  display: flex;
  flex-direction: column;
  margin-bottom: 70px;
}

.decade-row {
  display: flex;
  align-items: top;  
  position: relative;
}

/* línea vertical */
.timeline-container::before {
  content: "";
  position: absolute;
  left: 67px; 
  top: 0;
  bottom: 0;
  width: 2.5px;
  height: 2600px;
  background-color: #000000;
 
}

.year-label {
  width: 150px;        
  font-size: 18pt;
  margin-right: 60px;   
  
  z-index:1;

  background-color: #FCFDF7;
  color: black;
  font-size: 20pt;
 
  border-radius: 20px;
  width: 280px;
  height: 60px;
  
  line-height: 30px;
  font-weight: bold;
  padding-top: 10px;
  
}

.designers-row {
  display: flex;
  flex-wrap: wrap;
  gap: 60px;            
}

.mosaico {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  position: relative;
}

.tamaño {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
}

.fondo {
  position: absolute;
  width: 100%;
  height: 100%;
  object-fit: contain; 
}

p {
  font-size: 16px;
  margin-top: 15px;
}

footer {
  width: 100%; 
  height: 250px; 
  background-image: url('./images/footer.svg'); 
  background-size: cover; 
  background-repeat: no-repeat; 
  background-position: center center; 
  margin-top: 100px;
}

.header-imagen {
  width: 100%; 
  height: auto; 
  overflow: hidden; 
}

.header-imagen img {
  width: 100%; 
  height: auto; 
  display: block; /* Elimina el espacio extra que los elementos inline podrían agregar */
}

.titulo {
  display: flex;
  align-items: center; 
  gap: 100px; 
  padding-right: 200px;
  padding-left: 200px;
  margin-top: 80px;
}

.titulo h1 {
  font-size: 60pt;
  line-height: 80px; /* interlineado */
  font-weight: bold;
  color: #000000;
}

.bajada {
  font-size: 12pt;
  color: #333;
}


h2 {
  font-size: 20pt; 
  color: #000000;
  margin-top: 10px;
  font-weight: bold;
  margin-bottom: 50px;
  
}

h4 {
  font-size: 18pt; 
  color: #000000;
  margin-top: 10px;
  font-weight: bold;
  margin-bottom: 50px;
  text-align: center;
  margin-top: 30px;
  margin-bottom: 80px;
  margin-left: 80px;
}






/*referencias*/
.referencias {
  width: 1300px;
  height: 868px;
  border: 1px solid black;
  border-radius: 20px;
  margin: 50px auto;
  position: relative;
  padding: 40px;
}

.tituloref {
  background-color: #FCFDF7;
  color: black;
  font-size: 20pt;
  border: 1px solid black;
  border-radius: 20px;
  width: 280px;
  height: 50px;
  text-align: center;
  line-height: 30px;
  font-weight: bold;
  position: absolute;
  top: -35px;
  left: 50%;
  transform: translateX(-50%);
  padding-top: 10px;
}

.grid-referencias {
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.row-container {
  display: flex;
  justify-content: space-between;
  gap: 40px;
}

.ref-section {
  flex: 1;
}

.ref-title {
  font-size: 16px;
  margin-bottom: 20px;
  border-bottom: 1px solid black;
  padding-bottom: 10px;
  font-weight: bold;
  text-align: center;
}

/* Estilos específicos para la primera fila */
.top-row .ref-icons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 30px;
}

.top-row .icon-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

.top-row img {
  width: 80px;
  height: 80px;
}
.ref-section.nacimiento {
  width: 100%;
}

.birth-years-container {
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  gap: 30px; 
  padding: 10px 0;
}


.birth-year-grid {
  display: flex;
  flex-direction: column; 
  align-items: center;
  text-align: center;
  gap: 15px; /* Espacio entre imagen y texto */
}

.birth-year-grid img {
  width: 80px;
  height: 80px;
}

.birth-year-grid span {
  font-size: 14px;
  white-space: nowrap;
  display: block; /* para que el texto quede en su propia línea */
}


.icon-item span{
  font-size: 14px;
  white-space: nowrap;
  display: block; 
  margin-top: 10px;
}


/* Ajuste del container de la fila del medio */
.row-container.middle-row {
  flex-direction: column;
  gap: 20px;
}


.design-type-container {
  display: flex;
  gap: 20px;
  justify-content: flex-start;
}

.color-box {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px; 
}

/* El cuadrado de color */
.color-box::before {
  content: '';
  display: block;
  width: 80px;
  height: 80px;
  border-radius: 8px;
}

.color-box span {
  font-size: 14px;
  text-align: center;
  margin-top: 5px;
  color: black;
}

/* Colores para cada tipo de diseño */
.industrial::before { background-color: #C10B43; }
.grafico::before { background-color: #F6CCC4; }
.mobiliario::before { background-color: #A8D7F5; }
.textil::before { background-color: #EDC666; }
.interiores::before { background-color: #CCD65B; }

/* Estilos para la sección de obras */
.size-container {
  display: flex;
  align-items: center;
  gap: 30px;
}

.size-description{
  font-size: 14px;
  width:250px ;
  height: 83px;
  
}

.size-container img {
  width: 185px;
  height: 100px;
}
.size-description,
.marido-description {
  font-size: 14px;
  max-width: 300px;
}

/* Estilos para la sección de marido */
.marido-container {
  display: flex;
  align-items: center;
  gap: 20px;
}

.marido-container img {
  width: 100px;
  height: 100px;
}


/* Para centrar el contenido de cada contenedor de referencia */
.ref-section {
  display: flex;
  flex-direction: column;
  align-items: center; 
  justify-content: center; 
  padding: 10px;
}

.ref-icons, .birth-years-container, .design-type-container {
  display: flex;
  justify-content: center; 
  flex-wrap: wrap; 
  gap: 50px; 
}



</style>
