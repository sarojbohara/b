
<html>
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>TasteHeaven - Food Ordering</title>

  <style>
    :root {
      --primary-color: #ff5722;
      --background-light: #f4f4f4;
      --background-dark: #121212;
      --text-light: #ffffff;
      --text-dark: #222222;
      --sidebar-width: 100px;
      --transition-speed: 0.4s;
    }

    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      scroll-behavior: smooth;
    }

    body {
      background-color: var(--background-light);
      color: var(--text-dark);
      transition: background-color var(--transition-speed), color var(--transition-speed);
    }

    header {
      width: 100%;
      background-color: var(--primary-color);
      color: var(--text-light);
      padding: 20px;
      text-align: center;
      font-size: 30px;
      font-weight: bold;
      letter-spacing: 1px;
    }

    .sidebar {
      position: fixed;
      top: 80px;
      left: 0;
      width: var(--sidebar-width);
      height: calc(100vh - 80px);
      background-color: #333;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding-top: 20px;
      transition: width var(--transition-speed);
    }

    .sidebar a {
      color: var(--text-light);
      text-decoration: none;
      margin: 15px 0;
      font-size: 14px;
      text-align: center;
      padding: 10px 5px;
      width: 100%;
      transition: background 0.3s, font-size 0.3s;
    }

    .sidebar a:hover, .sidebar a.active {
      background-color: #444;
      font-size: 16px;
    }

    .main-content {
      margin-left: var(--sidebar-width);
      padding: 30px;
      transition: margin-left var(--transition-speed);
    }

    .page {
      display: none;
      min-height: calc(100vh - 80px);
      background-size: cover;
      background-position: center;
      padding: 30px;
      opacity: 0;
      transform: translateY(20px);
      transition: opacity 0.5s, transform 0.5s;
    }

    .page.active {
      display: block;
      opacity: 1;
      transform: translateY(0);
    }

    .home {
      background-image: url('https://images.unsplash.com/photo-1600891963932-c6c9d712b5b5?auto=format&fit=crop&w=1470&q=80');
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      text-align: center;
      color: var(--text-light);
      text-shadow: 2px 2px 8px rgba(0,0,0,0.7);
    }

    .home h1 {
      font-size: 4rem;
      margin-bottom: 30px;
    }

    .home button {
      background-color: var(--primary-color);
      color: var(--text-light);
      padding: 15px 30px;
      font-size: 20px;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      transition: background-color 0.3s;
    }

    .home button:hover {
      background-color: #e64a19;
    }

    .menu {
      background-color: var(--background-light);
    }

    .menu h2 {
      text-align: center;
      font-size: 36px;
      margin-bottom: 30px;
      color: var(--primary-color);
    }

    .food-item {
      display: flex;
      background-color: white;
      border-radius: 10px;
      overflow: hidden;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
      margin: 20px auto;
      max-width: 800px;
      transition: transform 0.3s;
    }

    .food-item:hover {
      transform: scale(1.02);
    }

    .food-item img {
      width: 150px;
      height: 150px;
      object-fit: cover;
    }

    .food-details {
      padding: 20px;
      flex: 1;
    }

    .food-details h3 {
      margin-bottom: 10px;
      font-size: 24px;
      color: #333;
    }

    .food-details p {
      margin-bottom: 10px;
      font-size: 18px;
      color: #666;
    }

    .food-controls {
      display: flex;
      align-items: center;
      gap: 10px;
      margin-top: 10px;
    }

    .food-controls input {
      width: 60px;
      padding: 8px;
      text-align: center;
      font-size: 16px;
    }

    .total-price {
      text-align: center;
      font-size: 24px;
      margin-top: 20px;
      color: #333;
    }

    .submit-btn {
      display: block;
      margin: 40px auto;
      padding: 15px 40px;
      background-color: var(--primary-color);
      color: white;
      font-size: 20px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      transition: background-color 0.3s;
    }

    .submit-btn:hover {
      background-color: #e64a19;
    }

    .end {
      background-color: var(--background-light);
      display: flex;
      flex-direction: column;
      align-items: center;
      text-align: center;
      padding-top: 100px;
    }

    .end h2 {
      font-size: 40px;
      color: var(--primary-color);
      margin-bottom: 20px;
    }

    .thank-you {
      font-size: 24px;
      color: #555;
      margin-bottom: 40px;
    }

    .ads img {
      margin: 10px;
      width: 280px;
      border-radius: 10px;
      box-shadow: 0 4px 8px rgba(0,0,0,0.2);
    }

    footer {
      background-color: #333;
      color: white;
      text-align: center;
      padding: 20px;
      font-size: 16px;
    }

    .loading-screen {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0,0,0,0.7);
      color: #fff;
      display: none;
      justify-content: center;
      align-items: center;
      font-size: 32px;
      z-index: 9999;
      animation: fadeIn 0.5s;
    }

    @keyframes fadeIn {
      from {opacity: 0;}
      to {opacity: 1;}
    }
  </style>
</head>

<body>

<div class="loading-screen" id="loadingScreen">
  Processing Your Order...
</div>

<header>
  TasteHeaven Restaurant
</header>

<div class="sidebar">
  <a href="#" onclick="navigateTo('homePage')" id="homeLink">🏠</a>
  <a href="#" onclick="navigateTo('menuPage')" id="menuLink">🍔</a>
  <a href="#" onclick="navigateTo('endPage')" id="endLink">✅</a>
</div>

<div class="main-content">

  <section class="page home active" id="homePage">
    <h1>Welcome to TasteHeaven</h1>
    <button onclick="navigateTo('menuPage')">Order Now</button>
  </section>

  <section class="page menu" id="menuPage">
    <h2>Our Delicious Menu</h2>

    <div class="food-item">
      <img src="https://images.unsplash.com/photo-1568901346375-23c9450c58cd?auto=format&fit=crop&w=800&q=80" alt="Cheese Burger">
      <div class="food-details">
        <h3>Cheese Burger</h3>
        <p>Price: $5.99</p>
        <div class="food-controls">
          <label>Qty: </label><input type="number" id="burgerQty" min="0" value="0" onchange="updateTotal()">
        </div>
      </div>
    </div>

    <div class="food-item">
      <img src="https://images.unsplash.com/photo-1550547660-d9450f859349?auto=format&fit=crop&w=800&q=80" alt="Pizza">
      <div class="food-details">
        <h3>Margherita Pizza</h3>
        <p>Price: $8.49</p>
        <div class="food-controls">
          <label>Qty: </label><input type="number" id="pizzaQty" min="0" value="0" onchange="updateTotal()">
        </div>
      </div>
    </div>

    <div class="total-price" id="totalPrice">
      Total: $0.00
    </div>

    <button class="submit-btn" onclick="submitOrder()">Submit Order</button>
  </section>

  <section class="page end" id="endPage">
    <h2>Order Placed Successfully!</h2>
    <p class="thank-you">Thank you for ordering at TasteHeaven! Your food is being prepared.</p>

    <div class="ads">
      <img src="https://via.placeholder.com/280x150?text=Special+Offer+1" alt="Special Offer 1">
      <img src="https://via.placeholder.com/280x150?text=Special+Offer+2" alt="Special Offer 2">
      <img src="https://via.placeholder.com/280x150?text=Special+Offer+3" alt="Special Offer 3">
    </div>
  </section>

</div>

<footer>
  &copy; 2025 TasteHeaven. All Rights Reserved.
</footer>

<script>
  function navigateTo(pageId) {
    const pages = document.querySelectorAll('.page');
    const links = document.querySelectorAll('.sidebar a');

    pages.forEach(p => p.classList.remove('active'));
    links.forEach(l => l.classList.remove('active'));

    document.getElementById(pageId).classList.add('active');
    if (pageId === 'homePage') document.getElementById('homeLink').classList.add('active');
    else if (pageId === 'menuPage') document.getElementById('menuLink').classList.add('active');
    else if (pageId === 'endPage') document.getElementById('endLink').classList.add('active');
  }

  function updateTotal() {
    const burgerQty = parseInt(document.getElementById('burgerQty').value) || 0;
    const pizzaQty = parseInt(document.getElementById('pizzaQty').value) || 0;

    const total = (burgerQty * 5.99) + (pizzaQty * 8.49);

    document.getElementById('totalPrice').innerText = `Total: $${total.toFixed(2)}`;
  }

  function submitOrder() {
    const total = document.getElementById('totalPrice').innerText;
    if (total === "Total: $0.00") {
      alert("Please order at least one item!");
      return;
    }

    document.getElementById('loadingScreen').style.display = 'flex';

    setTimeout(() => {
      document.getElementById('loadingScreen').style.display = 'none';
      navigateTo('endPage');
    }, 2000);
  }
</script>

</body>
</html>
