from pathlib import Path
from zipfile import ZipFile

# HTML content from the updated document
html_content = """<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Viaje de Sabores</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background-color: #fff8f0;
      color: #333;
    }
    header {
      background-color: #d94f30;
      color: white;
      padding: 20px;
      text-align: center;
    }
    nav {
      background-color: #f3d3b1;
      padding: 10px;
      text-align: center;
    }
    nav a {
      margin: 0 15px;
      text-decoration: none;
      color: #333;
      font-weight: bold;
    }
    section {
      padding: 20px;
    }
    .continente {
      margin-bottom: 30px;
    }
    .receta {
      background-color: #fff;
      border: 1px solid #ddd;
      border-radius: 10px;
      padding: 15px;
      margin: 10px 0;
    }
    .receta img {
      max-width: 100%;
      border-radius: 10px;
    }
    .receta h3 {
      margin-top: 0;
    }
    #buscador {
      margin: 20px auto;
      text-align: center;
    }
    #buscador input {
      width: 60%;
      padding: 10px;
      border-radius: 5px;
      border: 1px solid #ccc;
    }
    footer {
      background-color: #d94f30;
      color: white;
      text-align: center;
      padding: 15px;
    }
  </style>
  <script>
    function buscarReceta() {
      const input = document.getElementById('input-busqueda').value.toLowerCase();
      const recetas = document.querySelectorAll('.receta');
      recetas.forEach(receta => {
        const texto = receta.innerText.toLowerCase();
        receta.style.display = texto.includes(input) ? 'block' : 'none';
      });
    }
  </script>
</head>
<body>
  <header>
    <h1>Viaje de Sabores</h1>
    <p>Explora la gastronomía mundial desde un solo lugar</p>
  </header>

  <nav>
    <a href="#africa">África</a>
    <a href="#asia">Asia</a>
    <a href="#europa">Europa</a>
    <a href="#america">América</a>
    <a href="#oceania">Oceanía</a>
  </nav>

  <div id="buscador">
    <input type="text" id="input-busqueda" placeholder="Buscar receta por país o ingrediente..." oninput="buscarReceta()">
  </div>

  <section id="africa" class="continente">
    <h2>África</h2>
    <div class="receta">
      <h3>Cuscús - Marruecos</h3>
      <img src="https://via.placeholder.com/400x200?text=Cuscús" alt="Cuscús">
      <p>Ingredientes: sémola, verduras, garbanzos, especias.</p>
      <p>Preparación: Cocina al vapor la sémola y mezcla con un guiso de verduras.</p>
    </div>
  </section>

  <section id="asia" class="continente">
    <h2>Asia</h2>
    <div class="receta">
      <h3>Sushi - Japón</h3>
      <img src="https://via.placeholder.com/400x200?text=Sushi" alt="Sushi">
      <p>Ingredientes: arroz, alga nori, pescado crudo, vinagre.</p>
      <p>Preparación: Enrolla el arroz con el pescado y el alga nori usando una esterilla.</p>
    </div>
  </section>

  <section id="europa" class="continente">
    <h2>Europa</h2>
    <div class="receta">
      <h3>Paella - España</h3>
      <img src="https://via.placeholder.com/400x200?text=Paella" alt="Paella">
      <p>Ingredientes: arroz, mariscos, pollo, azafrán, verduras.</p>
      <p>Preparación: Sofríe los ingredientes, añade el arroz y cocina a fuego lento.</p>
    </div>
  </section>

  <section id="america" class="continente">
    <h2>América</h2>
    <div class="receta">
      <h3>Tacos - México</h3>
      <img src="https://via.placeholder.com/400x200?text=Tacos" alt="Tacos">
      <p>Ingredientes: tortillas de maíz, carne, cebolla, cilantro.</p>
      <p>Preparación: Calienta las tortillas y rellénalas con carne y condimentos.</p>
    </div>
  </section>

  <section id="oceania" class="continente">
    <h2>Oceanía</h2>
    <div class="receta">
      <h3>Meat Pie - Australia</h3>
      <img src="https://via.placeholder.com/400x200?text=Meat+Pie" alt="Meat Pie">
      <p>Ingredientes: carne molida, masa de hojaldre, cebolla, salsa.</p>
      <p>Preparación: Cocina la carne con salsa y hornea en una base de hojaldre.</p>
    </div>
  </section>

  <footer>
    <p>&copy; 2025 Viaje de Sabores | Todos los derechos reservados</p>
  </footer>
</body>
</html>
"""

# Save the file
output_dir = Path("/mnt/data/viaje_de_sabores")
output_dir.mkdir(parents=True, exist_ok=True)
html_file = output_dir / "index.html"
html_file.write_text(html_content, encoding="utf-8")

# Zip the folder
zip_path = Path("/mnt/data/viaje_de_sabores.zip")
with ZipFile(zip_path, 'w') as zipf:
    zipf.write(html_file, arcname="index.html")

zip_path.name  # Return the name for download link

