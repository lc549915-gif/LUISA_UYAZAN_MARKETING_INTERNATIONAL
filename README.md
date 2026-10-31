<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Luisa Uyazan _ Marl International</title>
  <style>
     body {
      font-family: system-ui, Arial, sans-serif;
      background-color: #f4f4f4;
      color: #333;
      padding: 20px;
      margin: 0;
      text-align: center;
    }

    h1 {
      color: #222;
      margin-bottom: 8px;
    }

    .slogan {
      color: #666;
      font-size: 17px;
      margin-top: 0;
      margin-bottom: 25px;
    }

    /* Beneficios de la tienda */

    .beneficios {
      display: flex;
      justify-content: center;
      gap: 30px;
      flex-wrap: wrap;

      background-color: #222;
      color: white;

      padding: 14px;
      margin-bottom: 30px;
    }

    .beneficios span {
      font-size: 14px;
    }

    /* Catálogo */

    #productos {
      display: flex;
      justify-content: center;
      flex-wrap: wrap;
      gap: 15px;
    }

    .producto {
      border: 1px solid #ccc;
      background: white;
      border-radius: 8px;
      padding: 10px;
      width: 220px;
      vertical-align: top;
    }

    .producto img {
      width: 100%;
      height: 140px;
      object-fit: cover;
      border-radius: 4px;
    }

    .producto h3 {
      margin-bottom: 8px;
    }

    .descripcion {
      font-size: 14px;
      color: #666;
      min-height: 42px;
    }

    .precio {
      font-size: 18px;
      font-weight: bold;
      color: #222;
    }

    /* Botones */

    .producto button {
      background-color: #28a745;
      border: none;
      color: white;
      padding: 9px 12px;
      margin-top: 5px;
      border-radius: 4px;
      cursor: pointer;
    }

    .producto button:hover {
      opacity: 0.85;
    }

    /* Carrito */

    .carrito {
      margin-top: 35px;
      padding: 20px;
      background: white;
      border-radius: 8px;
      text-align: left;
      display: inline-block;
      min-width: 320px;
    }

    .carrito h2 {
      margin-top: 0;
    }

    #lista-carrito {
      padding-left: 20px;
    }

    #lista-carrito li {
      margin-bottom: 8px;
    }

    .resumen {
      border-top: 1px solid #ddd;
      margin-top: 15px;
      padding-top: 10px;
    }

    .total {
      font-size: 19px;
    }

    /* Botón vaciar */

    .vaciar {
      background-color: #dc3545;
      border: none;
      color: white;
      padding: 9px 12px;
      margin-top: 10px;
      border-radius: 4px;
      cursor: pointer;
    }

    /* Botón finalizar */

    .finalizar {
      background-color: #007bff;
      border: none;
      color: white;
      padding: 9px 12px;
      margin-top: 10px;
      margin-left: 5px;
      border-radius: 4px;
      cursor: pointer;
    }

    .vaciar:hover,
    .finalizar:hover {
      opacity: 0.85;
    }
  </style>
</head>
<body>
  <h1>🍽️ Quimbaya: A Sweet Taste of Colombia</h1>

  <p class="slogan">
   Un dulce pedacito de Colombia❤️
  </p>

  <div class="beneficios">
    <span>🚚 Envíos en Bogotá</span>
    <span>🔒 Compra segura</span>
    <span>📦 Seguimiento de pedido</span>
  </div>

  <div id="productos"></div>

  <div class="carrito">
    <h2>🧾 Carrito de Compras</h2>

    <ul id="lista-carrito"></ul>

    <div class="resumen">
      <p>
        Envío: <strong>Gratis</strong>
      </p>

      <p class="total">
        Total: $<span id="total">0</span>
      </p>
    </div>

    <button class="vaciar" onclick="vaciarCarrito()">
      🧼 Vaciar Carrito
    </button>

    <button class="finalizar" onclick="finalizarCompra()">
      ✅ Finalizar Compra
    </button>
  </div>

  <script>
    const productos = [
      {
        id: 1,
        nombre: "Quimbayas Original",
        descripcion: "Disfruta el auténtico sabor colombiano en cada galleta, con una tradición que conquista paladares.",
        precio: 25000,
        imagen: "https://farmawebonline.com/wp-content/uploads/2024/01/D_747699-MCO43145572981_082020-F-1-711x711.jpg"
      },
      {
        id: 2,
        nombre: "Quimbayas Mini",
        descripcion: "Pequeñas en tamaño, grandes en sabor. Perfectas para disfrutar en cualquier momento.",
        precio: 18000,
        imagen: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQKicXbmjbP8K0YVIqgQL3P82iQIm_jvhATmt605Pr46cu31CbDB_znXcJ0&s=10"
      },
      {
        id: 3,
        nombre: "Quimbayas Premium",
        descripcion: "Una presentación especial que combina tradición colombiana, calidad y un sabor irresistible..",
        precio: 30000,
        imagen: "https://lagolosineria.com.co/wp-content/uploads/2024/02/Quimbaya-x-18-und.jpg"
      },
      {
        id: 4,
        nombre: "Quimbayas Familiar",
        descripcion: "Comparte momentos especiales con el delicioso sabor de las tradicionales galletas Quimbayas.",
        precio: 18000,
        imagen: "https://acdn-us.mitiendanube.com/stores/006/648/928/products/2-2d919a3a160c2339b117597904847875-1024-1024.webp"
      },
      {
        id: 5,
        nombre: "Quimbayas Snack Pack",
        descripcion: "Llévalas contigo a todas partes y disfruta un pedacito de Colombia donde quieras. 🇨🇴❤️.",
        precio: 22000,
        imagen: "https://ideaspapeleria.com/images/002852/large/2362_0.png"
      }
    ];


    /* ==============================
       CARRITO
    ================================ */

    const carrito = [];

    const contenedorProductos = document.getElementById("productos");
    const listaCarrito = document.getElementById("lista-carrito");
    const totalCarrito = document.getElementById("total");


    /* ==============================
       MOSTRAR PRODUCTOS
    ================================ */

    function mostrarProductos() {

      contenedorProductos.innerHTML = "";

      productos.forEach(prod => {

        const div = document.createElement("div");

        div.className = "producto";

        div.innerHTML = `
          <img src="${prod.imagen}" alt="${prod.nombre}">

          <h3>${prod.nombre}</h3>

          <p class="descripcion">
            ${prod.descripcion}
          </p>

          <p class="precio">
            ${prod.precio.toLocaleString("es-CO", {
              style: "currency",
              currency: "COP",
              minimumFractionDigits: 0
            })}
          </p>

          <button onclick="agregarAlCarrito(${prod.id})">
            Agregar al carrito
          </button>
        `;

        contenedorProductos.appendChild(div);

      });

    }


    /* ==============================
       AGREGAR AL CARRITO
    ================================ */

    function agregarAlCarrito(id) {

      const productoExistente =
        carrito.find(p => p.id === id);

      if (productoExistente) {

        productoExistente.cantidad++;

      } else {

        const producto =
          productos.find(p => p.id === id);

        carrito.push({
          ...producto,
          cantidad: 1
        });

      }

      actualizarCarrito();

    }


    /* ==============================
       ACTUALIZAR CARRITO
    ================================ */

    function actualizarCarrito() {

      listaCarrito.innerHTML = "";

      let total = 0;
      let totalItems = 0;

      carrito.forEach(item => {

        const li =
          document.createElement("li");

        const subtotal =
          item.precio * item.cantidad;

        li.textContent =
          `${item.nombre} x${item.cantidad} — ` +
          subtotal.toLocaleString("es-CO", {
            style: "currency",
            currency: "COP",
            minimumFractionDigits: 0
          });

        listaCarrito.appendChild(li);

        total += subtotal;
        totalItems += item.cantidad;

      });

      totalCarrito.textContent =
        total.toLocaleString("es-CO");

      actualizarTituloCarrito(totalItems);

    }


    /* ==============================
       CONTADOR DEL CARRITO
    ================================ */

    function actualizarTituloCarrito(cantidad) {

      const titulo =
        document.querySelector(".carrito h2");

      titulo.textContent =
        `🧾 Carrito de Compras (${cantidad})`;

    }


    /* ==============================
       VACIAR CARRITO
    ================================ */

    function vaciarCarrito() {

      if (carrito.length === 0) {

        alert("🛒 El carrito ya está vacío.");

        return;

      }

      if (
        confirm(
          "¿Estás seguro de que quieres vaciar el carrito?"
        )
      ) {

        carrito.length = 0;

        actualizarCarrito();

      }

    }


    /* ==============================
       FINALIZAR COMPRA
    ================================ */

    function finalizarCompra() {

      if (carrito.length === 0) {

        alert(
          "🛒 Tu carrito está vacío. Agrega productos antes de finalizar la compra."
        );

        return;

      }

      alert(
        "🎉 ¡Pedido simulado confirmado!\n\n" +
        "En un eCommerce real, ahora entrarían en acción " +
        "el backend, la pasarela de pago y la logística."
      );

      carrito.length = 0;

      actualizarCarrito();

    }


    /* ==============================
       INICIAR TIENDA
    ================================ */

    mostrarProductos();
  </script>
</body>
</html>
