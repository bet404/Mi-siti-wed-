<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Tienda de PANEL Y MACRO 👹 - Inicio y Comprar Separado</title>
  <script src="https://js.stripe.com/v3/"></script>
  <style>
    /* Reset */
    * {
      box-sizing: border-box;
    }
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      margin: 0;
      padding: 0;
      background-image: url('https://cdn.discordapp.com/attachments/1373129746979880990/1374250224423538809/IMG_20250519_225905.jpg?ex=682d5dc1&is=682c0c41&hm=ef1722a74f86d917fc3069fc601fd070cbf3f5713a5c1fc01740de7e4f16a285&');
      background-size: cover;
      background-position: center;
      background-repeat: no-repeat;
      color: #333;
      min-height: 100vh;
    }
    header {
      background: rgba(74, 60, 140, 0.8);
      color: #f0f0f0;
      padding: 15px 30px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      flex-wrap: wrap;
      box-shadow: 0 4px 10px rgba(0,0,0,0.2);
    }
    header h1 {
      margin: 0;
      font-weight: 900;
    }
    nav {
      display: flex;
      gap: 15px;
    }
    nav button {
      background: transparent;
      border: 2px solid #f0f0f0;
      color: #f0f0f0;
      padding: 8px 18px;
      border-radius: 22px;
      cursor: pointer;
      font-weight: 700;
      font-size: 1rem;
      transition: background-color 0.3s ease;
    }
    nav button:hover, nav button.active {
      background-color: #f0f0f0;
      color: #4a3c8c;
    }
    main {
      max-width: 1200px;
      margin: 25px auto;
      padding: 0 20px 60px;
      background: rgba(255, 255, 255, 0.8);
      border-radius: 18px;
      box-shadow: 0 12px 30px rgba(0,0,0,0.15);
    }
    section {
      display: none;
      padding: 25px 0;
    }
    section.active {
      display: block;
    }
    h2 {
      color: #4a3c8c;
      font-weight: 900;
      margin-bottom: 20px;
    }
    /* Inicio */
    #inicio p {
      font-size: 1.2rem;
      line-height: 1.5;
      max-width: 700px;
      margin-bottom: 20px;
    }
    /* Buscador con IA */
    #buscadorContainer {
      display: flex;
      gap: 10px;
      margin-bottom: 25px;
    }
    #buscar {
      flex-grow: 1;
      padding: 12px 15px;
      font-size: 1.1rem;
      border-radius: 25px;
      border: 2px solid #4a3c8c;
      outline: none;
      transition: border-color 0.3s ease;
    }
    #buscar:focus {
      border-color: #667eea;
    }
    #btnVoz {
      background: #4a3c8c;
      color: white;
      border: none;
      padding: 0 15px;
      font-size: 1.3rem;
      border-radius: 25px;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      transition: background-color 0.3s ease;
    }
    #btnVoz:hover {
      background: #667eea;
    }
    /* Productos */
    #productosLista {
      display: grid;
      grid-template-columns: repeat(auto-fill,minmax(250px,1fr));
      gap: 25px;
    }
    .producto {
      border: 2px solid #4a3c8c;
      border-radius: 18px;
      overflow: hidden;
      display: flex;
      flex-direction: column;
      background: rgba(255, 255, 255, 0.8);
      box-shadow: 0 8px 20px rgba(0,0,0,0.1);
      transition: transform 0.3s ease;
    }
    .producto:hover {
      transform: translateY(-8px);
      box-shadow: 0 14px 32px rgba(0,0,0,0.25);
    }
    .producto img {
      width: 100%;
      height: 160px;
      object-fit: cover;
    }
    .producto-info {
      padding: 18px;
      flex-grow: 1;
      display: flex;
      flex-direction: column;
    }
    .producto-info h3 {
      margin: 0 0 10px;
      font-weight: 900;
      color: #4a3c8c;
    }
    .producto-info p.precio {
      font-weight: 700;
      font-size: 1.2rem;
      color: #667eea;
      margin-bottom: 15px;
    }
    .producto-info button {
      margin-top: auto;
      background: #4a3c8c;
      border: none;
      color: white;
      padding: 10px 0;
      border-radius: 15px;
      cursor: pointer;
      font-weight: 700;
      font-size: 1rem;
      transition: background-color 0.3s ease;
    }
    .producto-info button:hover {
      background: #667eea;
    }
    /* Carrito */
    #carrito {
      max-width: 1200px;
      margin: 25px auto;
      padding: 20px;
      background: rgba(255, 255, 255, 0.8);
      border-radius: 18px;
      box-shadow: 0 12px 30px rgba(0,0,0,0.15);
    }
    #carrito h3 {
      margin: 0 0 20px 0;
      color: #4a3c8c;
      font-weight: 900;
    }
    #carritoLista {
      flex-grow: 1;
      overflow-y: auto;
    }
    .itemCarrito {
      display: flex;
      justify-content: space-between;
      margin-bottom: 14px;
      font-weight: 600;
      color: #333;
    }
    .itemCarrito span {
      flex-grow: 1;
    }
    .itemCarrito button {
      background: transparent;
      border: none;
      color: #e76f51;
      font-weight: 700;
      font-size: 1.2rem;
      cursor: pointer;
    }
    .itemCarrito button:hover {
      color: #cf4f31;
    }
    #totalCarrito {
      font-weight: 900;
      font-size: 1.3rem;
      margin-top: 15px;
      text-align: right;
      color: #667eea;
    }
    #btnVaciarCarrito {
      background: #e76f51;
      border: none;
      padding: 12px 0;
      border-radius: 15px;
      margin-top: 15px;
      font-weight: 900;
      color: white;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }
    #btnVaciarCarrito:hover {
      background: #cf4f31;
    }
    #btnPagar {
      background: #4a3c8c;
      border: none;
      padding: 12px 0;
      border-radius: 15px;
      margin-top: 15px;
      font-weight: 900;
      color: white;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }
    #btnPagar:hover {
      background: #667eea;
    }

    /* Payment Form */
    #paymentForm {
      display: flex;
      flex-direction: column;
      gap: 10px;
    }
    #paymentForm div {
      margin-bottom: 10px;
    }
    #paymentForm label {
      display: block;
      margin-bottom: 5px;
    }
    #paymentForm input, #paymentForm select {
      width: 100%;
      padding: 8px;
      margin-bottom: 10px;
      border: 1px solid #ccc;
      border-radius: 4px;
    }
    #paymentForm button {
      padding: 10px;
      background-color: #4a3c8c;
      color: white;
      border: none;
      border-radius: 4px;
      cursor: pointer;
    }
    #paymentForm button:hover {
      background-color: #667eea;
    }
    #card-element {
      padding: 10px;
      border: 1px solid #ccc;
      border-radius: 4px;
      margin-bottom: 10px;
    }

    /* Responsive */
    @media(max-width: 768px) {
      nav {
        width: 100%;
        justify-content: center;
        flex-wrap: wrap;
        gap: 8px;
      }
    }
  </style>
</head>
<body>

<header>
  <h1>Tienda en venta por diamantes 👹👹</h1>
  <nav aria-label="Menú principal">
    <button class="nav-btn active" data-section="inicio" aria-current="page">Inicio</button>
    <button class="nav-btn" data-section="comprar">Comprar</button>
    <button class="nav-btn" data-section="carrito">Carrito</button>
    <button class="nav-btn" data-section="pago">Pago</button>
  </nav>
</header>

<main>
  <!-- Inicio -->
  <section id="inicio" class="active" tabindex="0" aria-label="Sección inicio">
    <h2>por 500 diamantes paso el código de la tienda totalmente 👾 </h2>
    <p>Explora una amplia variedad de productos de alta calidad con precios justos.</p>
    <p>Usa el apartado "Comprar" para buscar, filtrar y añadir productos a tu carrito.</p>
  </section>

  <!-- Comprar -->
  <section id="comprar" tabindex="0" aria-label="Sección para comprar productos">
    <h2>Comprar Productos</h2>
    <div id="buscadorContainer">
      <input type="search" id="buscar" placeholder="Buscar productos..." aria-label="Buscar productos" autocomplete="off" />
      <button id="btnVoz" aria-label="Buscar por voz" title="Buscar por voz">🎙️</button>
    </div>
    <div id="productosLista" role="list" aria-live="polite" aria-atomic="true"></div>
  </section>

  <!-- Carrito -->
  <section id="carrito" tabindex="0" aria-label="Sección del carrito de compras">
    <h2>Carrito de Compras</h2>
    <div id="carritoLista" role="list"></div>
    <div id="totalCarrito">Total: $0.00</div>
    <button id="btnVaciarCarrito" aria-label="Vaciar carrito">Vaciar carrito</button>
    <button id="btnPagar" aria-label="Ir a métodos de pago">Pagar</button>
  </section>

  <!-- Payment -->
  <section id="pago" tabindex="0" aria-label="Sección de métodos de pago">
    <h2>Métodos de Pago</h2>
    <form id="paymentForm">
      <div>
        <label for="paymentMethod">Seleccione un método de pago:</label>
        <select id="paymentMethod" required>
          <option value="">--Seleccione--</option>
          <option value="creditCard">Tarjeta de Crédito</option>
          <option value="paypal">PayPal</option>
          <option value="bankTransfer">Transferencia Bancaria</option>
        </select>
      </div>
      <div id="creditCardDetails" style="display: none;">
        <label for="cardNumber">Número de Tarjeta:</label>
        <div id="card-element"></div>
        <div id="totalPago">Total a pagar: $0.00</div>
        <button type="submit" id="btnPagar">Pagar</button>
      </div>
      <div id="paypalDetails" style="display: none;">
        <p>Será redirigido a PayPal para completar el pago.</p>
        <div id="totalPago">Total a pagar: $0.00</div>
        <button type="button" id="btnPagarPayPal">Pagar</button>
      </div>
      <div id="bankTransferDetails" style="display: none;">
        <p>Por favor, realice la transferencia a la siguiente cuenta bancaria:</p>
        <p>Banco: XYZ Bank</p>
        <p>Número de Cuenta: 123456789</p>
        <div id="totalPago">Total a pagar: $0.00</div>
        <button type="button" id="btnPagarTransferencia">Pagar</button>
      </div>
    </form>
  </section>
</main>

<script>
  // Datos ejemplo productos
  const productos = [
    { id: 1, nombre: "Placid 1", precio: 45.99, img: "https://cdn.discordapp.com/attachments/1373129627752468700/1373754798985183302/image.png?ex=682b905b&is=682a3edb&hm=aeb8c7460204531d76902f6155fe5c3d9c306c05b8012b607fef704437de5df3&" },
    { id: 2, nombre: "Placid 2", precio: 249.99, img: "https://cdn.discordapp.com/attachments/1373129627752468700/1373754798985183302/image.png?ex=682b905b&is=682a3edb&hm=aeb8c7460204531d76902f6155fe5c3d9c306c05b8012b607fef704437de5df3&" },
    { id: 3, nombre: "placid 3", precio: 149.49, img: "https://cdn.discordapp.com/attachments/1373129627752468700/1373754798985183302/image.png?ex=682b905b&is=682a3edb&hm=aeb8c7460204531d76902f6155fe5c3d9c306c05b8012b607fef704437de5df3&" },
    { id: 4, nombre: "placid 4", precio: 79.00, img: "https://cdn.discordapp.com/attachments/1373129627752468700/1373754798985183302/image.png?ex=682b905b&is=682a3edb&hm=aeb8c7460204531d76902f6155fe5c3d9c306c05b8012b607fef704437de5df3&" },
    { id: 5, nombre: "placid 5", precio: 1299.99, img: "https://cdn.discordapp.com/attachments/1373129627752468700/1373754798985183302/image.png?ex=682b905b&is=682a3edb&hm=aeb8c7460204531d76902f6155fe5c3d9c306c05b8012b607fef704437de5df3&" },
    { id: 6, nombre: "placid 6", precio: 39.95, img: "https://cdn.discordapp.com/attachments/1373129627752468700/1373754798985183302/image.png?ex=682b905b&is=682a3edb&hm=aeb8c7460204531d76902f6155fe5c3d9c306c05b8012b607fef704437de5df3&" }
  ];

  // Estado carrito
  let carrito = [];

  // Mostrar productos
  function mostrarProductos(lista) {
    const contenedor = document.getElementById('productosLista');
    contenedor.innerHTML = '';
    if (lista.length === 0) {
      contenedor.innerHTML = '<p>No se encontraron productos.</p>';
      return;
    }
    lista.forEach(prod => {
      const div = document.createElement('div');
      div.className = 'producto';
      div.setAttribute('role', 'listitem');
      div.innerHTML = `
        <img src="${prod.img}" alt="Foto de ${prod.nombre}" />
        <div class="producto-info">
          <h3>${prod.nombre}</h3>
          <p class="precio">$${prod.precio.toFixed(2)}</p>
          <button aria-label="Agregar ${prod.nombre} al carrito">Añadir al carrito</button>
        </div>
      `;
      div.querySelector('button').addEventListener('click', () => {
        agregarAlCarrito(prod.id);
      });
      contenedor.appendChild(div);
    });
  }

  // Añadir producto al carrito
  function agregarAlCarrito(id) {
    const prod = productos.find(p => p.id === id);
    if (prod) {
      carrito.push(prod);
      actualizarCarrito();
    }
  }

  // Actualizar carrito
  function actualizarCarrito() {
    const carritoLista = document.getElementById('carritoLista');
    const totalCarrito = document.getElementById('totalCarrito');
    carritoLista.innerHTML = '';
    let total = 0;

    carrito.forEach((item, index) => {
      const div = document.createElement('div');
      div.className = 'itemCarrito';
      div.setAttribute('role', 'listitem');
      div.innerHTML = `
        <span>${item.nombre} - $${item.precio.toFixed(2)}</span>
        <button aria-label="Eliminar ${item.nombre} del carrito" data-index="${index}">✕</button>
      `;
      div.querySelector('button').addEventListener('click', (e) => {
        const index = e.target.getAttribute('data-index');
        carrito.splice(index, 1);
        actualizarCarrito();
      });
      carritoLista.appendChild(div);
      total += item.precio;
    });

    totalCarrito.textContent = `Total: $${total.toFixed(2)}`;
    document.querySelectorAll('#totalPago').forEach(el => {
      el.textContent = `Total a pagar: $${total.toFixed(2)}`;
    });
  }

  // Vaciar carrito
  document.getElementById('btnVaciarCarrito').addEventListener('click', () => {
    carrito = [];
    actualizarCarrito();
  });

  // Cambiar secciones
  document.addEventListener('DOMContentLoaded', function() {
    const navButtons = document.querySelectorAll('.nav-btn');

    navButtons.forEach(button => {
      button.addEventListener('click', function() {
        navButtons.forEach(btn => btn.classList.remove('active'));
        document.querySelectorAll('section').forEach(section => section.classList.remove('active'));

        this.classList.add('active');
        const sectionId = this.getAttribute('data-section');
        document.getElementById(sectionId).classList.add('active');
      });
    });

    // Mostrar productos al cargar la página
    mostrarProductos(productos);
  });

  // Payment methods logic
  document.getElementById('paymentMethod').addEventListener('change', function() {
    const paymentMethod = this.value;
    document.getElementById('creditCardDetails').style.display = 'none';
    document.getElementById('paypalDetails').style.display = 'none';
    document.getElementById('bankTransferDetails').style.display = 'none';

    if (paymentMethod === 'creditCard') {
      document.getElementById('creditCardDetails').style.display = 'block';
    } else if (paymentMethod === 'paypal') {
      document.getElementById('paypalDetails').style.display = 'block';
    } else if (paymentMethod === 'bankTransfer') {
      document.getElementById('bankTransferDetails').style.display = 'block';
    }
  });

  // Stripe integration
  const stripe = Stripe('your-publishable-key');
  const elements = stripe.elements();
  const cardElement = elements.create('card');
  cardElement.mount('#card-element');

  const paymentForm = document.getElementById('paymentForm');
  paymentForm.addEventListener('submit', async (event) => {
    event.preventDefault();

    const paymentMethod = document.getElementById('paymentMethod').value;
    if (paymentMethod === 'creditCard') {
      const { paymentMethod, error } = await stripe.createPaymentMethod({
        type: 'card',
        card: cardElement,
      });

      if (error) {
        alert(error.message);
      } else {
        const total = carrito.reduce((sum, item) => sum + item.precio, 0);
        const response = await fetch('/create-payment-intent', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify({ amount: Math.round(total * 100), currency: 'usd' }),
        });
        const { clientSecret } = await response.json();

        const { error: confirmError, paymentIntent } = await stripe.confirmCardPayment(clientSecret, {
          payment_method: paymentMethod.id,
        });

        if (confirmError) {
          alert(confirmError.message);
        } else if (paymentIntent.status === 'succeeded') {
          alert('Pago procesado con éxito!');
        }
      }
    } else {
      alert('Pago procesado con éxito!');
    }
  });

  // PayPal and Bank Transfer buttons
  document.getElementById('btnPagarPayPal').addEventListener('click', () => {
    alert('Redirigiendo a PayPal para completar el pago.');
  });

  document.getElementById('btnPagarTransferencia').addEventListener('click', () => {
    alert('Transferencia bancaria procesada con éxito!');
  });

  // Add event listener for the "Pagar" button in the cart
  document.getElementById('btnPagar').addEventListener('click', () => {
    // Remove active class from all sections and buttons
    document.querySelectorAll('section').forEach(section => section.classList.remove('active'));
    document.querySelectorAll('.nav-btn').forEach(button => button.classList.remove('active'));

    // Add active class to the payment section and corresponding button
    document.getElementById('pago').classList.add('active');
    document.querySelector('.nav-btn[data-section="pago"]').classList.add('active');
  });
</script>

</body>
</html>
