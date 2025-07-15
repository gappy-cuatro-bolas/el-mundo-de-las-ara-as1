
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>🕷️ El mundo de las Arañas</title> 
  <script src="https://kit.fontawesome.com/yourkitcode.js" crossorigin="anonymous"></script>
  <style>
    body {
      margin: 0;
      background: linear-gradient(to bottom, #0f0f0f, #1c1c1c);
      color: #e0e0e0;
      font-family: 'Segoe UI', Tahoma, sans-serif;
    }

    header {
      background: linear-gradient(135deg, #2a2a2a, #1a1a1a);
      padding: 3rem 1rem 2rem;
      text-align: center;
      box-shadow: 0 3px 15px rgba(255, 23, 68, 0.6);
    }

    header h1 {
      font-size: 2.8rem;
      color: #ff1744;
      margin: 0;
      text-shadow: 0 0 12px #ff1744;
    }

    header p {
      font-size: 1.4rem;
      color: #fce4ec;
      margin-top: 1rem;
      text-shadow: 0 0 8px #ff6f91;
    }

    #filtros {
      max-width: 600px;
      margin: 2rem auto;
      display: flex;
      flex-wrap: wrap;
      gap: 1rem;
      justify-content: center;
      padding: 0 1rem;
    }

    #filtros input,
    #filtros select {
      padding: 0.75rem 1rem;
      border-radius: 30px;
      border: 2px solid #333;
      background: #262626;
      color: #e0e0e0;
      font-size: 1rem;
      flex: 1 1 220px;
      outline: none;
      transition: border-color 0.3s, box-shadow 0.3s;
    }

    #filtros input:focus,
    #filtros select:focus {
      border-color: #ff1744;
      box-shadow: 0 0 10px rgba(255, 23, 68, 0.5);
    }

    #arañas-db {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 2rem;
      max-width: 1100px;
      margin: 2rem auto;
      padding: 0 1rem;
    }

    .tarjeta {
      background: #1e1e1e;
      border-radius: 16px;
      overflow: hidden;
      box-shadow: 0 4px 20px rgba(255, 23, 68, 0.2);
      display: flex;
      flex-direction: column;
      transition: transform 0.3s ease, box-shadow 0.3s ease;
    }

    .tarjeta:hover {
      transform: translateY(-6px);
      box-shadow: 0 6px 25px rgba(255, 23, 68, 0.35);
    }

    .tarjeta img {
      width: 100%;
      height: 180px;
      object-fit: cover;
    }

    .tarjeta-content {
      padding: 1rem;
    }

    .tarjeta h3 {
      color: #ff1744;
      margin: 0.5rem 0;
    }

    .tarjeta h4 {
      font-style: italic;
      color: #ff6f91;
      margin-bottom: 0.8rem;
    }

    .tarjeta p {
      font-size: 0.95rem;
    }

    .btn-ver {
      display: inline-block;
      margin-top: 1rem;
      padding: 0.5rem 1rem;
      background: #ff1744;
      color: #fff;
      border-radius: 30px;
      font-weight: bold;
      text-decoration: none;
      transition: background 0.3s;
    }

    .btn-ver:hover {
      background: #ff5252;
    }

    footer {
      background: #121212;
      color: #ccc;
      padding: 3rem 1rem 2rem;
      text-align: center;
      box-shadow: 0 -2px 10px rgba(255, 23, 68, 0.2);
    }

    footer h2 {
      color: #ff1744;
      margin-bottom: 1rem;
    }

    .social-icons a {
      margin: 0 0.5rem;
      color: #ff6f91;
      font-size: 1.8rem;
      transition: color 0.3s;
    }

    .social-icons a:hover {
      color: #ff1744;
    }

    .footer-bottom {
      margin-top: 2rem;
      font-size: 0.85rem;
      color: #888;
    }
  </style>
</head>
<body>
  <header>
    <h1>🕷️ El mundo de las Arañas</h1>
    <p>Descubre las especies más fascinantes y temidas del reino arácnido</p>
  </header>

  <div id="filtros">
    <input type="text" id="buscar" placeholder="Buscar por nombre o científico..." />
    <select id="familia">
      <option value="">Todas las familias</option>
    </select>
  </div>

  <div id="arañas-db"></div>

  <footer>
    <h2>Conéctate con nosotros</h2>
    <p>Síguenos para más contenido fascinante del mundo arácnido.</p>
    <div class="social-icons">
      <a href="https://facebook.com" target="_blank" aria-label="Facebook"><i class="fab fa-facebook-square"></i></a>
      <a href="https://twitter.com" target="_blank" aria-label="Twitter"><i class="fab fa-twitter-square"></i></a>
      <a href="https://instagram.com" target="_blank" aria-label="Instagram"><i class="fab fa-instagram-square"></i></a>
      <a href="mailto:info@aracnopedia.org" aria-label="Correo"><i class="fas fa-envelope-square"></i></a>
    </div>
    <div class="footer-bottom">
      &copy; 2025 El mundo de las Arañas. Todos los derechos reservados.
    </div>
  </footer>

  <script>
    const arañas = [
      { nombre: 'Viuda negra', nombreCientifico: 'Latrodectus mactans', familia: 'Theridiidae', descripcion: 'Famosa por su veneno neurotóxico, aunque suele evitar a humanos.', imagen: 'https://cdnwine.diario1.com/wp-content/uploads/2023/08/Viuda-Negra.jpg', enlace: 'proyectorelacionado1.html' },
      { nombre: 'Araña de rincón', nombreCientifico: 'Loxosceles laeta', familia: 'Loxosceles', descripcion: 'Pequeña y nocturna, su mordedura puede causar necrosis.', imagen: 'https://www.cuidomidespensa.com/hubfs/Imported_Blog_Media/loxosceles-g56d5a9b2f_1920-1.jpg', enlace: 'proyectorelacionado2.html' },
      { nombre: 'Tarántula', nombreCientifico: 'Theraphosidae', familia: 'Theraphosidae', descripcion: 'Grande y peluda, impresionante pero generalmente inofensiva.', imagen: 'https://www.reptilmadrid.com/wp-content/uploads/2022/09/como-cuidar-una-tarantula.jpg', enlace: 'proyectorelacionado.html' },
      { nombre: 'Araña saltarina', nombreCientifico: 'Phidippus audax', familia: 'Salticidae', descripcion: 'Conocida por su capacidad de salto y su vista aguda.', imagen: 'https://upload.wikimedia.org/wikipedia/commons/thumb/c/cb/Flickr_-_Lukjonis_-_Jumping_spider_-_Sitticus_floricola_%28set_of_pictures%29.jpg/960px-Flickr_-_Lukjonis_-_Jumping_spider_-_Sitticus_floricola_%28set_of_pictures%29.jpg', enlace: 'proyectorelacionado3.html' },
      { nombre: 'Araña lobo', nombreCientifico: 'Lycosidae', familia: 'Lycosidae', descripcion: 'Cazadora rápida y nocturna que no usa telarañas.', imagen: 'https://lahuertinadetoni.es/wp-content/uploads/2015/01/233-163-Copiar.jpg', enlace: 'proyectorelacionado4.html' },
      { nombre: 'Araña cangrejo', nombreCientifico: 'Misumena vatia', familia: 'Thomisidae', descripcion: 'Se camufla en flores, esperando a sus presas con paciencia.', imagen: 'https://inaturalist-open-data.s3.amazonaws.com/photos/38263287/original.jpeg', enlace: 'proyectorelacionado5.html' },
      { nombre: 'Araña bananera', nombreCientifico: 'Phoneutria nigriventer', familia: 'Ctenidae', descripcion: 'Altamente venenosa y agresiva, encontrada en Sudamérica.', imagen: 'https://cdn.dl.uy//solimg/894x503/8/8790.jpg', enlace: 'proyectorelacionado7.html' },
      { nombre: 'Araña camello', nombreCientifico: 'Solifugae', familia: 'Solifugae', descripcion: 'Aunque no es una araña real, es temida por su aspecto aterrador.', imagen: 'https://static.nationalgeographic.es/files/styles/image_3200/public/2266.600x450.jpg?w=1600', enlace: 'proyectorelacionado8.html' },
      { nombre: 'Araña pavo real', nombreCientifico: 'Maratus volans', familia: 'Salticidae', descripcion: 'Conocida por sus colores brillantes y danzas de cortejo.', imagen: 'https://static.nationalgeographic.es/files/styles/image_3200/public/02-peacock-spider-9678_9679_9680.webp?w=1190&h=911.jpg', enlace: 'proyectorelacionado6.html' },
      { nombre: 'Araña ermitaña marrón', nombreCientifico: 'Loxosceles reclusa', familia: 'Loxosceles', descripcion: 'Similar a la de rincón, pero nativa de EE.UU.', imagen: 'https://s3.animalia.bio/animals/photos/full/original/loxosceles-reclusa-290976310.jpg', enlace: 'proyectorelacionado9.html' },
      { nombre: 'Araña de seda dorada', nombreCientifico: 'Trichonephila clavipes', familia: 'Araneidae', descripcion: 'Tejedora de enormes telarañas doradas en zonas tropicales.', imagen: 'https://static.wikia.nocookie.net/reinoanimalia/images/3/36/Nephila-clavipes-15.jpg/revision/latest?cb=20181129173614&path-prefix=es', enlace: 'proyectorelacionado10.html' },
      { nombre: 'Araña cazadora gigante', nombreCientifico: 'Heteropoda maxima', familia: 'Sparassidae', descripcion: 'La araña más grande en extensión de patas.', imagen: 'https://cloudfront-us-east-1.images.arcpublishing.com/infobae/HP6S6VSSLRF6TFMGDGM4VNV56I.webp', enlace: 'proyectorelacionado11.html' },
      { nombre: 'Araña tejedora de orbes', nombreCientifico: 'Araneus diadematus', familia: 'Araneidae', descripcion: 'Común en jardines, famosa por su cruz blanca en el abdomen.', imagen: 'https://preview.redd.it/garden-orb-weaver-sydney-v0-aocjwbzu2vwe1.jpg?width=640&crop=smart&auto=webp&s=a5e65f24286c2747dcb4bfd2d9ee7d6481c84c61', enlace: 'proyectorelacionado12.html' }
    ];

    const dbContainer = document.getElementById('arañas-db');
    const inputBusqueda = document.getElementById('buscar');
    const selectFamilia = document.getElementById('familia');

    // Crear lista única de familias para el filtro:
    const familiasUnicas = Array.from(new Set(arañas.map(a => a.familia))).sort();
    familiasUnicas.forEach(fam => {
      const option = document.createElement('option');
      option.value = fam;
      option.textContent = fam;
      selectFamilia.appendChild(option);
    });

    function mostrarArañas(datos) {
      dbContainer.innerHTML = '';
      if (datos.length === 0) {
        dbContainer.innerHTML = '<p style="text-align:center; color:#ff6f91;">No se encontraron arañas.</p>';
        return;
      }
      datos.forEach((araña) => {
        const tarjeta = document.createElement('div');
        tarjeta.className = 'tarjeta';
        tarjeta.innerHTML = `
          <img src="${araña.imagen}" alt="${araña.nombre}" />
          <div class="tarjeta-content">
            <h3>${araña.nombre}</h3>
            <h4><em>${araña.nombreCientifico}</em></h4>
            <p>${araña.descripcion}</p>
            <p><strong>Familia:</strong> ${araña.familia}</p>
            <a class="btn-ver" href="${araña.enlace}" target="_blank" rel="noopener noreferrer">Ver más</a>
          </div>
        `;
        dbContainer.appendChild(tarjeta);
      });
    }

    function filtrarArañas() {
      const texto = inputBusqueda.value.toLowerCase();
      const familia = selectFamilia.value;

      const filtradas = arañas.filter((a) => {
        const coincideTexto =
          a.nombre.toLowerCase().includes(texto) ||
          a.nombreCientifico.toLowerCase().includes(texto);
        const coincideFamilia = familia === '' || a.familia === familia;
        return coincideTexto && coincideFamilia;
      });

      mostrarArañas(filtradas);
    }

    inputBusqueda.addEventListener('input', filtrarArañas);
    selectFamilia.addEventListener('change', filtrarArañas);

    mostrarArañas(arañas);
  </script>
</body>
</html>
