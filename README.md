<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>🕷️ Tarántula Goliat | El mundo de las Arañas</title> 
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&family=Roboto+Condensed:wght@400;700&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <!-- Leaflet CSS -->
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
  <style>
    :root {
      --primary: #6D4C41;
      --primary-dark: #4E342E;
      --primary-light: #A1887F;
      --secondary: #8D6E63;
      --dark: #0F0F0F;
      --darker: #080808;
      --light: #F8F9FA;
      --gray: #495057;
    }

    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      margin: 0;
      background: linear-gradient(135deg, var(--darker), var(--dark));
      color: var(--light);
      font-family: 'Poppins', sans-serif;
      min-height: 100vh;
      overflow-x: hidden;
    }

    /* Efecto de telaraña de fondo */
    .web-background {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-image: url("data:image/svg+xml,%3Csvg width='100' height='100' viewBox='0 0 100 100' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M50 0 L100 50 L50 100 L0 50 Z' stroke='rgba(109,76,65,0.05)' stroke-width='0.5' fill='none'/%3E%3C/svg%3E");
      z-index: -1;
      opacity: 0.3;
    }

    /* Header con efecto */
    header {
      background: linear-gradient(135deg, rgba(15, 15, 15, 0.95), rgba(30, 30, 30, 0.98));
      padding: 4rem 1rem 3rem;
      text-align: center;
      position: relative;
      overflow: hidden;
      backdrop-filter: blur(5px);
      border-bottom: 1px solid rgba(109, 76, 65, 0.3);
      box-shadow: 0 5px 30px rgba(78, 52, 46, 0.3);
    }

    header::before {
      content: '';
      position: absolute;
      bottom: 0;
      left: 50%;
      transform: translateX(-50%);
      width: 300px;
      height: 300px;
      background: radial-gradient(circle, rgba(109, 76, 65, 0.2), transparent 70%);
      z-index: -1;
    }

    header h1 {
      font-size: 3.5rem;
      font-family: 'Roboto Condensed', sans-serif;
      color: var(--primary);
      margin: 0;
      text-shadow: 0 0 15px var(--primary), 0 0 30px rgba(109, 76, 65, 0.5);
      letter-spacing: 2px;
      position: relative;
      display: inline-block;
    }

    header h1::after {
      content: '🕷️';
      position: absolute;
      right: -40px;
      top: -15px;
      font-size: 2rem;
      animation: spiderFloat 3s ease-in-out infinite;
    }

    @keyframes spiderFloat {
      0%, 100% { transform: translateY(0) rotate(0deg); }
      50% { transform: translateY(-10px) rotate(5deg); }
    }

    .scientific-name {
      font-style: italic;
      color: var(--primary-light);
      font-size: 1.8rem;
      margin-top: 0.5rem;
      text-shadow: 0 0 8px rgba(161, 136, 127, 0.5);
    }

    .danger-label {
      display: inline-block;
      background: var(--primary-dark);
      color: white;
      padding: 0.5rem 1.5rem;
      border-radius: 50px;
      font-weight: bold;
      margin-top: 1rem;
      box-shadow: 0 0 15px rgba(78, 52, 46, 0.5);
      animation: pulse 2s infinite;
    }

    @keyframes pulse {
      0% { box-shadow: 0 0 15px rgba(78, 52, 46, 0.5); }
      50% { box-shadow: 0 0 25px rgba(78, 52, 46, 0.8); }
      100% { box-shadow: 0 0 15px rgba(78, 52, 46, 0.5); }
    }

    /* Contenedor principal */
    .main-container {
      max-width: 1200px;
      margin: 3rem auto;
      padding: 0 2rem;
      display: grid;
      grid-template-columns: 1fr;
      gap: 3rem;
    }

    @media (min-width: 992px) {
      .main-container {
        grid-template-columns: 1fr 1fr;
      }
    }

    /* Sección de información */
    .info-section {
      background: linear-gradient(145deg, rgba(30, 30, 30, 0.9), rgba(20, 20, 20, 0.95));
      border-radius: 20px;
      padding: 2rem;
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
      border: 1px solid rgba(109, 76, 65, 0.2);
      position: relative;
      overflow: hidden;
    }

    .info-section::before {
      content: '';
      position: absolute;
      top: -50%;
      left: -50%;
      width: 200%;
      height: 200%;
      background: radial-gradient(circle, rgba(109, 76, 65, 0.05), transparent 60%);
      z-index: -1;
    }

    .section-title {
      color: var(--primary);
      font-size: 2rem;
      margin-bottom: 1.5rem;
      position: relative;
      display: inline-block;
    }

    .section-title::after {
      content: '';
      position: absolute;
      bottom: -8px;
      left: 0;
      width: 60px;
      height: 3px;
      background: var(--primary);
      border-radius: 3px;
    }

    .info-section p {
      margin-bottom: 1.5rem;
      line-height: 1.8;
      color: rgba(255, 255, 255, 0.9);
    }

    .info-section ul {
      margin-left: 1.5rem;
      margin-bottom: 1.5rem;
    }

    .info-section li {
      margin-bottom: 0.8rem;
      position: relative;
      padding-left: 1.5rem;
      color: rgba(255, 255, 255, 0.8);
    }

    .info-section li::before {
      content: '🕷️';
      position: absolute;
      left: 0;
      top: 0;
      font-size: 0.8rem;
    }

    /* Galería de imágenes */
    .gallery {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 1.5rem;
      margin-top: 2rem;
    }

    .gallery-item {
      border-radius: 15px;
      overflow: hidden;
      position: relative;
      border: 2px solid rgba(109, 76, 65, 0.3);
      transition: all 0.3s ease;
      aspect-ratio: 1/1;
    }

    .gallery-item:hover {
      transform: translateY(-5px);
      box-shadow: 0 10px 20px rgba(109, 76, 65, 0.3);
      border-color: var(--primary);
    }

    .gallery-item img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      transition: transform 0.5s ease;
    }

    .gallery-item:hover img {
      transform: scale(1.1);
    }

    .gallery-caption {
      position: absolute;
      bottom: 0;
      left: 0;
      right: 0;
      background: linear-gradient(to top, rgba(0, 0, 0, 0.8), transparent);
      padding: 1rem;
      color: white;
      transform: translateY(100%);
      transition: transform 0.3s ease;
    }

    .gallery-item:hover .gallery-caption {
      transform: translateY(0);
    }

    /* Sección de datos científicos */
    .data-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 1.5rem;
      margin-top: 2rem;
    }

    .data-card {
      background: rgba(15, 15, 15, 0.5);
      border-radius: 15px;
      padding: 1.5rem;
      border-left: 4px solid var(--primary);
      transition: all 0.3s ease;
    }

    .data-card:hover {
      background: rgba(109, 76, 65, 0.1);
      transform: translateY(-5px);
    }

    .data-card h3 {
      color: var(--primary-light);
      font-size: 1rem;
      margin-bottom: 0.5rem;
      font-weight: 600;
    }

    .data-card p {
      font-size: 1.2rem;
      font-weight: bold;
      color: white;
      margin: 0;
    }

    /* Sección de veneno */
    .venom-section {
      background: linear-gradient(to right, rgba(78, 52, 46, 0.1), rgba(15, 15, 15, 0.7));
      border-radius: 20px;
      padding: 2rem;
      margin-top: 3rem;
      position: relative;
      overflow: hidden;
      border: 1px solid rgba(78, 52, 46, 0.3);
    }

    .venom-section::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: url("data:image/svg+xml,%3Csvg width='100' height='100' viewBox='0 0 100 100' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M0 0 L100 100 M0 100 L100 0' stroke='rgba(78,52,46,0.05)' stroke-width='1'/%3E%3C/svg%3E");
      z-index: -1;
    }

    .venom-stats {
      display: flex;
      flex-wrap: wrap;
      gap: 1.5rem;
      margin-top: 1.5rem;
    }

    .venom-stat {
      flex: 1;
      min-width: 150px;
      text-align: center;
      padding: 1rem;
      background: rgba(78, 52, 46, 0.2);
      border-radius: 10px;
      border: 1px solid rgba(78, 52, 46, 0.3);
    }

    .venom-stat h4 {
      color: var(--primary-light);
      margin-bottom: 0.5rem;
      font-size: 0.9rem;
    }

    .venom-stat p {
      font-size: 1.5rem;
      font-weight: bold;
      color: white;
      margin: 0;
    }

    /* Sección de distribución */
    .map-container {
      height: 400px;
      background: rgba(15, 15, 15, 0.5);
      border-radius: 15px;
      margin-top: 1.5rem;
      position: relative;
      overflow: hidden;
      border: 1px solid rgba(109, 76, 65, 0.3);
    }

    #distribution-map {
      width: 100%;
      height: 100%;
      background: var(--darker);
    }

    .map-legend {
      position: absolute;
      bottom: 20px;
      right: 20px;
      background: rgba(0, 0, 0, 0.7);
      padding: 0.5rem 1rem;
      border-radius: 5px;
      color: white;
      font-size: 0.8rem;
      z-index: 1000;
    }

    .legend-color {
      display: inline-block;
      width: 12px;
      height: 12px;
      margin-right: 5px;
      background: var(--primary);
      border-radius: 2px;
    }

    /* Footer */
    footer {
      background: linear-gradient(to bottom, rgba(15, 15, 15, 0.9), rgba(8, 8, 8, 0.95));
      color: var(--light);
      padding: 4rem 1rem 2rem;
      text-align: center;
      position: relative;
      margin-top: 5rem;
    }

    footer::before {
      content: '';
      position: absolute;
      top: -50px;
      left: 0;
      width: 100%;
      height: 50px;
      background: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 1200 120' preserveAspectRatio='none'%3E%3Cpath d='M0,0V46.29c47.79,22.2,103.59,32.17,158,28,70.36-5.37,136.33-33.31,206.8-37.5C438.64,32.43,512.34,53.67,583,72.05c69.27,18,138.3,24.88,209.4,13.08,36.15-6,69.85-17.84,104.45-29.34C989.49,25,1113-14.29,1200,52.47V0Z' opacity='.25' fill='%236D4C41'/%3E%3Cpath d='M0,0V15.81C13,36.92,27.64,56.86,47.69,72.05,99.41,111.27,165,111,224.58,91.58c31.15-10.15,60.09-26.07,89.67-39.8,40.92-19,84.73-46,130.83-49.67,36.26-2.85,70.9,9.42,98.6,31.56,31.77,25.39,62.32,62,103.63,73,40.44,10.79,81.35-6.69,119.13-24.28s75.16-39,116.92-43.05c59.73-5.85,113.28,22.88,168.9,38.84,30.2,8.66,59,6.17,87.09-7.5,22.43-10.89,48-26.93,60.65-49.24V0Z' opacity='.5' fill='%236D4C41'/%3E%3Cpath d='M0,0V5.63C149.93,59,314.09,71.32,475.83,42.57c43-7.64,84.23-20.12,127.61-26.46,59-8.63,112.48,12.24,165.56,35.4C827.93,77.22,886,95.24,951.2,90c86.53-7,172.46-45.71,233.88-58.29,119.39-18.62,182.79-49.13,248.8-84.81C1206.43,29.34,1200,0,1200,0Z' fill='%236D4C41'/%3E%3C/svg%3E");
      background-size: cover;
      background-repeat: no-repeat;
    }

    .back-button {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      margin-bottom: 2rem;
      padding: 0.8rem 1.8rem;
      background: rgba(255, 255, 255, 0.1);
      color: white;
      border-radius: 50px;
      font-weight: 600;
      text-decoration: none;
      transition: all 0.3s ease;
      border: 1px solid rgba(255, 255, 255, 0.2);
    }

    .back-button:hover {
      background: var(--primary);
      transform: translateY(-3px);
      box-shadow: 0 5px 15px rgba(109, 76, 65, 0.5);
    }

    .back-button i {
      margin-right: 8px;
      transition: transform 0.3s ease;
    }

    .back-button:hover i {
      transform: translateX(-5px);
    }

    .footer-bottom {
      margin-top: 2rem;
      font-size: 0.9rem;
      color: rgba(255, 255, 255, 0.6);
      padding-top: 1.5rem;
      border-top: 1px solid rgba(255, 255, 255, 0.1);
    }

    /* Estilos para la sección de documental */
    .documentary-button {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      padding: 1rem 2rem;
      background: #FF0000;
      color: white;
      border-radius: 50px;
      font-weight: 600;
      text-decoration: none;
      transition: all 0.3s ease;
      border: 1px solid #CC0000;
      margin-top: 1rem;
      box-shadow: 0 4px 15px rgba(255, 0, 0, 0.3);
    }

    .documentary-button:hover {
      background: #CC0000;
      transform: translateY(-3px);
      box-shadow: 0 7px 20px rgba(255, 0, 0, 0.4);
    }

    .documentary-button i {
      margin-right: 10px;
      font-size: 1.2rem;
    }

    /* Responsive */
    @media (max-width: 768px) {
      header h1 {
        font-size: 2.5rem;
      }
      
      .scientific-name {
        font-size: 1.3rem;
      }
      
      .main-container {
        padding: 0 1rem;
        grid-template-columns: 1fr;
      }
      
      .data-grid {
        grid-template-columns: 1fr 1fr;
      }

      .map-container {
        height: 300px;
      }
    }

    @media (max-width: 480px) {
      header {
        padding: 3rem 1rem 2rem;
      }
      
      header h1 {
        font-size: 2rem;
      }
      
      .data-grid {
        grid-template-columns: 1fr;
      }

      .venom-stats {
        flex-direction: column;
      }
    }
  </style>
</head>
<body>
  <!-- Fondo de telaraña -->
  <div class="web-background"></div>

  <header>
    <h1>Tarántula Goliat</h1>
    <div class="scientific-name">Theraphosa blondi</div>
    <div class="danger-label">Peligrosidad: Baja</div>
  </header>

  <div class="main-container">
    <div class="info-section">
      <h2 class="section-title">Descripción</h2>
      <p>La Tarántula Goliat (<em>Theraphosa blondi</em>) es la araña más grande del mundo por masa corporal, con una envergadura de patas que puede alcanzar los 30 cm. Es una especie impresionante pero generalmente inofensiva para los humanos.</p>
      
      <p>Su cuerpo está cubierto de pelos rojizos-marrones que le dan un aspecto intimidante. A pesar de su tamaño, es una criatura tímida que prefiere huir antes que confrontar. Cuando se siente amenazada, puede frotar sus patas traseras contra su abdomen, liberando una nube de pelos urticantes.</p>
      
      <h3 class="section-title" style="margin-top: 2rem;">Características clave</h3>
      <ul>
        <li>Tamaño: Hasta 30 cm de envergadura</li>
        <li>Peso: Hasta 170 gramos</li>
        <li>Color: Marrón rojizo con pelos claros</li>
        <li>Hábitat: Selvas tropicales húmedas</li>
        <li>Distribución: Norte de Sudamérica</li>
        <li>Dieta: Insectos, pequeños vertebrados</li>
      </ul>
    </div>

    <div class="info-section">
      <h2 class="section-title">Galería</h2>
      <div class="gallery">
        <div class="gallery-item">
          <img src="https://www.reptilmadrid.com/wp-content/uploads/2022/09/como-cuidar-una-tarantula.jpg" alt="Tarántula Goliat adulta">
          <div class="gallery-caption">Ejemplar adulto</div>
        </div>
        <div class="gallery-item">
          <img src="https://static.nationalgeographicla.com/files/styles/image_3200/public/nationalgeographic2204210.jpg?w=1900&h=1265" alt="Primer plano de la tarántula">
          <div class="gallery-caption">Detalle de los pelos y patas</div>
        </div>
        <div class="gallery-item">
          <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRCQfSAYshteGswbk7ypAfJsenubt5hJDaHag&s" alt="Tarántula Goliat en la mano">
          <div class="gallery-caption">Comparación de tamaño</div>
        </div>
        <div class="gallery-item">
          <img src="https://amazoniaperu.org/wp-content/uploads/2022/12/donde-vive-la-tarantula-goliat-1024x690.jpg" alt="Tarántula comiendo">
          <div class="gallery-caption">Alimentándose</div>
        </div>
      </div>
    </div>

    <div class="info-section">
      <h2 class="section-title">Datos Científicos</h2>
      <div class="data-grid">
        <div class="data-card">
          <h3>Reino</h3>
          <p>Animalia</p>
        </div>
        <div class="data-card">
          <h3>Filo</h3>
          <p>Arthropoda</p>
        </div>
        <div class="data-card">
          <h3>Clase</h3>
          <p>Arachnida</p>
        </div>
        <div class="data-card">
          <h3>Orden</h3>
          <p>Araneae</p>
        </div>
        <div class="data-card">
          <h3>Familia</h3>
          <p>Theraphosidae</p>
        </div>
        <div class="data-card">
          <h3>Género</h3>
          <p>Theraphosa</p>
        </div>
      </div>
    </div>

    <div class="info-section">
      <h2 class="section-title">Distribución Geográfica</h2>
      <p>La Tarántula Goliat es nativa de las selvas tropicales del norte de Sudamérica, principalmente en Venezuela, Guyana, Surinam, Guayana Francesa y norte de Brasil. Prefiere áreas húmedas con suelos blandos donde puede excavar sus madrigueras.</p>
      
      <div class="map-container">
        <div id="distribution-map"></div>
        <div class="map-legend">
          <span class="legend-color"></span> Área de distribución
        </div>
      </div>
    </div>

    <div class="venom-section">
      <h2 class="section-title">Veneno y Defensas</h2>
      <p>Aunque su nombre científico incluye "blondi" en honor al explorador que la descubrió, su mordedura no es mortal para los humanos. Su veneno es comparable al de una avispa y solo causa dolor localizado.</p>
      
      <div class="venom-stats">
        <div class="venom-stat">
          <h4>Tipo de veneno</h4>
          <p>Neurotóxico leve</p>
        </div>
        <div class="venom-stat">
          <h4>Defensa principal</h4>
          <p>Pelos urticantes</p>
        </div>
        <div class="venom-stat">
          <h4>Efecto en humanos</h4>
          <p>Dolor moderado</p>
        </div>
        <div class="venom-stat">
          <h4>Comportamiento</h4>
          <p>No agresiva</p>
        </div>
      </div>
    </div>

    <div class="info-section">
      <h2 class="section-title">Comportamiento</h2>
      <p>La Tarántula Goliat es principalmente nocturna, pasando el día en su madriguera que excava en el suelo o aprovecha huecos naturales. A pesar de su nombre común ("comepájaros"), raramente se alimenta de aves, prefiriendo insectos, gusanos y ocasionalmente pequeños vertebrados.</p>
      
      <p>Cuando se siente amenazada, produce un sonido silbante frotando sus patas (estridulación) y puede lanzar sus pelos urticantes que causan irritación en la piel y mucosas.</p>
    </div>

    <div class="info-section">
      <h2 class="section-title">Curiosidades</h2>
      <ul>
        <li>Puede vivir hasta 25 años en cautiverio (las hembras)</li>
        <li>Los machos mueren poco después de alcanzar la madurez sexual</li>
        <li>Sus colmillos pueden alcanzar 2 cm de longitud</li>
        <li>No teje telarañas para cazar, es una cazadora activa</li>
        <li>Es popular en el comercio de mascotas exóticas</li>
        <li>En algunas culturas indígenas se consume como alimento</li>
      </ul>
    </div>

    <div class="info-section">
      <h2 class="section-title">Documental</h2>
      <p>Descubre más sobre esta fascinante araña gigante en este documental especializado:</p>
      
      <div style="text-align: center; margin-top: 2rem;">
        <a href="https://www.youtube.com/watch?v=AXCrwb9ECNM" 
           target="_blank" 
           class="documentary-button">
          <i class="fab fa-youtube"></i> Ver Documental en YouTube
        </a>
        <p style="margin-top: 1rem; font-size: 0.9rem; color: rgba(255,255,255,0.7);">
          Documental "Gigantes de la Selva: La Tarántula Goliat" (25 min)
        </p>
      </div>
    </div>
  </div>

  <footer>
    <a href="https://gappy-cuatro-bolas.github.io/el-mundo-de-las-arallas/" class="back-button">
      <i class="fas fa-arrow-left"></i> Volver al Mundo de las Arañas
    </a>
    <div class="footer-bottom">
      &copy; 2025 El mundo de las Arañas. Todos los derechos reservados. | Especial Tarántula Goliat
    </div>
  </footer>

  <!-- Leaflet JS -->
  <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
  <script>
    // Efecto de movimiento para el fondo de telaraña
    document.addEventListener('mousemove', (e) => {
      const web = document.querySelector('.web-background');
      const x = e.clientX / window.innerWidth;
      const y = e.clientY / window.innerHeight;
      web.style.transform = `translate(${x * 20}px, ${y * 20}px)`;
    });

    // Efecto de revelado al hacer scroll
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          entry.target.style.opacity = 1;
          entry.target.style.transform = 'translateY(0)';
        }
      });
    }, { threshold: 0.1 });

    document.querySelectorAll('.info-section, .venom-section').forEach(section => {
      section.style.opacity = 0;
      section.style.transform = 'translateY(30px)';
      section.style.transition = 'all 0.6s ease';
      observer.observe(section);
    });

    // Mapa de distribución
    document.addEventListener('DOMContentLoaded', () => {
      const map = L.map('distribution-map').setView([2, -56], 4);
      
      // Capa base oscura
      L.tileLayer('https://{s}.basemaps.cartocdn.com/dark_all/{z}/{x}/{y}{r}.png', {
        attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
      }).addTo(map);

      // Área de distribución aproximada (Norte de Sudamérica)
      const distributionCoords = [
        [12, -72], [8, -62], [5, -58], [2, -55], 
        [-1, -52], [-4, -50], [-4, -60], [2, -68], 
        [8, -72], [12, -72]
      ];

      const distributionArea = L.polygon(distributionCoords, {
        color: '#6D4C41',
        fillColor: '#6D4C41',
        fillOpacity: 0.3,
        weight: 1
      }).addTo(map);

      // Puntos de presencia confirmada
      const locations = [
        { lat: 6.4238, lng: -66.5897, name: 'Venezuela' },
        { lat: 4.8604, lng: -58.9302, name: 'Guyana' },
        { lat: 3.9193, lng: -56.0278, name: 'Surinam' },
        { lat: 3.9339, lng: -53.1258, name: 'Guayana Francesa' },
        { lat: 1.6508, lng: -61.6389, name: 'Norte de Brasil' },
        { lat: 5.0676, lng: -60.5577, name: 'Monte Roraima' }
      ];

      locations.forEach(loc => {
        L.circleMarker([loc.lat, loc.lng], {
          radius: 6,
          color: '#4E342E',
          fillColor: '#A1887F',
          fillOpacity: 0.8,
          weight: 1
        }).addTo(map).bindPopup(`<b>${loc.name}</b><br>Presencia confirmada`);
      });

      // Ajustar el zoom para mostrar toda el área
      map.fitBounds(distributionArea.getBounds());
    });
  </script>
</body>
</html>
