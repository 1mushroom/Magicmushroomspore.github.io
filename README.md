# Magicmushroomspore.github.io
Discover our premium Magic Mushroom Spore Collection, intended strictly for microscopy and research purposes. We offer a wide variety of high-quality spore prints and liquid cultures — perfect for serious researchers, hobby mycologists, and collectors.
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Magic Mushroom Spore Shop</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="https://cdn.jsdelivr.net/npm/@emailjs/browser@4/dist/email.min.js"></script>
  <script>
    emailjs.init("URqJZPMZaU2aw0dyD");
  </script>
</head>
<body class="bg-gray-100 text-gray-900">
  <header class="bg-white shadow p-4">
    <div class="container mx-auto flex justify-between items-center">
      <h1 class="text-2xl font-bold">🍄 Magic Mushroom Spore</h1>
    </div>
  </header>

  <main class="container mx-auto p-6">
    <!-- Cart and Products -->
    <section class="grid md:grid-cols-2 gap-8">
      <div>
        <h2 class="text-xl font-semibold mb-4">Products</h2>
        <div id="product-list" class="space-y-4">
          <!-- Product Items -->
        </div>
      </div>

      <div>
        <h2 class="text-xl font-semibold mb-4">Cart</h2>
        <ul id="cart" class="mb-4 space-y-2"></ul>
        <p><strong>Shipping:</strong> 12€</p>
        <p class="mb-4"><strong>Total:</strong> <span id="total">0€</span></p>
        
        <form id="checkout-form" class="space-y-2">
          <input type="text" name="name" placeholder="Your Name" class="w-full p-2 border" required>
          <input type="email" name="email" placeholder="Your Email" class="w-full p-2 border" required>
          <textarea name="address" placeholder="Your Shipping Address" class="w-full p-2 border" required></textarea>
          <button type="submit" class="bg-blue-500 text-white px-4 py-2 rounded">Pay</button>
        </form>

        <div id="payment-info" class="mt-4 hidden">
          <h3 class="text-lg font-semibold">Send Payment To:</h3>
          <p><strong>USDT:</strong> 0xF948676E24195c0e45D9EFbE8D1a0E674ef0Cc9C</p>
          <p><strong>Bitcoin:</strong> bc1q5fmlraj36xefdh2ge8pj6rfl3dsf9kwmpq34q8</p>
          <p><strong>Litecoin:</strong> ltc1q4kp2wv6kq4dgn08lfh8039jvc6kfjcr0tk9ruk</p>
        </div>

        <p id="thank-you" class="mt-4 font-bold text-green-600 hidden">Thank you! We will ship your order soon. 🍄</p>
      </div>
    </section>
  </main>

  <script>
    const products = [
      { name: "Golden Teacher Spore Print", price: 20 },
      { name: "Golden Teacher Spore Liquid", price: 25 },
      { name: "High Spore Print", price: 20 },
      { name: "High Spore Liquid", price: 20 },
      { name: "Golden Teacher with Grain", price: 48 },
      { name: "High Spore with Grain", price: 48 }
    ];

    const productList = document.getElementById('product-list');
    const cart = [];

    function updateCart() {
      const cartEl = document.getElementById('cart');
      const totalEl = document.getElementById('total');
      cartEl.innerHTML = '';
      let subtotal = 0;

      cart.forEach((item, i) => {
        subtotal += item.price;
        const li = document.createElement('li');
        li.textContent = `${item.name} - ${item.price}€`;
        cartEl.appendChild(li);
      });

      const total = subtotal + 12;
      totalEl.textContent = `${total}€`;
    }

    products.forEach(product => {
      const div = document.createElement('div');
      div.className = 'bg-white p-4 shadow rounded';
      div.innerHTML = `
        <h3 class="font-bold">${product.name}</h3>
        <p>${product.price}€</p>
        <button class="mt-2 bg-blue-500 text-white px-3 py-1 rounded" onclick='addToCart(${JSON.stringify(product)})'>Add to Cart</button>
      `;
      productList.appendChild(div);
    });

    function addToCart(product) {
      cart.push(product);
      updateCart();
    }

    document.getElementById('checkout-form').addEventListener('submit', function (e) {
      e.preventDefault();

      const form = this;
      const data = {
        name: form.name.value,
        email: form.email.value,
        address: form.address.value,
        cart: cart.map(item => `${item.name} - ${item.price}€`).join(', '),
        total: document.getElementById('total').textContent
      };

      emailjs.send("service_jhhl9mg", "template_o44dsbl", data)
        .then(() => {
          document.getElementById('payment-info').classList.remove('hidden');
          document.getElementById('thank-you').classList.remove('hidden');
          form.reset();
          cart.length = 0;
          updateCart();
        })
        .catch(err => alert("Something went wrong."));
    });
  </script>
</body>
</html>
