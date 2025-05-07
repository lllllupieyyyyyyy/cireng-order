<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no" />
<title>Cireng Bu Yati - Pemesanan</title>
<style>
  /* Reset and base */
  * {
    box-sizing: border-box;
  }
  body {
    margin: 0;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background: linear-gradient(135deg, #fceabb, #f8b500);
    color: #333;
    max-width: 350px;
    height: 600px;
    overflow: hidden;
    display: flex;
    flex-direction: column;
  }
  header {
    background: #f8b500;
    color: #fff;
    text-align: center;
    padding: 1rem;
    font-weight: 700;
    font-size: 1.5rem;
    letter-spacing: 2px;
    box-shadow: 0 2px 6px rgb(0 0 0 / 0.15);
  }
  .banner-image {
    width: 100%;
    max-height: 120px;
    object-fit: cover;
    border-radius: 0 0 20px 20px;
    box-shadow: 0 4px 8px rgb(0 0 0 / 0.15);
    margin-bottom: 0.75rem;
  }
  main {
    flex: 1;
    overflow-y: auto;
    padding: 0 1rem 1rem;
  }
  .product-list {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }
  .product {
    display: flex;
    background: #fff;
    border-radius: 12px;
    box-shadow: 0 6px 10px rgb(0 0 0 / 0.12);
    overflow: hidden;
    cursor: pointer;
    user-select: none;
    transition: background-color 0.2s ease;
  }
  .product:hover, .product:focus-within {
    background-color: #fcf3cc;
  }
  .product img {
    width: 120px;
    height: 120px;
    object-fit: cover;
    border-radius: 12px 0 0 12px;
    pointer-events: none;
    box-shadow: inset 0 0 10px rgba(248, 92, 0, 0.4);
    transition: transform 0.3s ease;
  }
  .product:hover img {
    transform: scale(1.07);
  }
  .product-details {
    padding: 0.5rem 1rem;
    flex: 1;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }
  .product-title {
    font-weight: 700;
    font-size: 1.1rem;
    margin: 0;
    color: #f85c00;
  }
  .product-desc {
    font-size: 0.85rem;
    color: #666;
    margin: 0.25rem 0 0.5rem;
  }
  .product-price {
    font-weight: 700;
    color: #f8b500;
  }
  .quantity-controls {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    justify-content: flex-start;
  }
  .quantity-controls button {
    background: #f8b500;
    border: none;
    color: #fff;
    padding: 0.25rem 0.6rem;
    font-weight: 700;
    font-size: 1.2rem;
    border-radius: 50%;
    cursor: pointer;
    flex-shrink: 0;
    user-select: none;
    transition: background-color 0.3s ease;
  }
  .quantity-controls button:active {
    background-color: #d9a200;
  }
  .quantity-controls input {
    width: 40px;
    text-align: center;
    font-size: 1rem;
    padding: 0.1rem;
    border-radius: 6px;
    border: 1px solid #ccc;
    -moz-appearance: textfield;
  }
  /* Remove number input arrows */
  input[type=number]::-webkit-inner-spin-button, 
  input[type=number]::-webkit-outer-spin-button { 
    -webkit-appearance: none; 
    margin: 0; 
  }
  .order-summary {
    margin-top: 1rem;
    background: #fff;
    padding: 1rem;
    border-radius: 12px;
    box-shadow: 0 4px 8px rgb(0 0 0 / 0.1);
  }
  .order-summary h2 {
    margin: 0 0 0.5rem;
    font-size: 1.25rem;
    text-align: center;
    color: #f8b500;
  }
  .order-summary-list {
    max-height: 120px;
    overflow-y: auto;
    font-size: 0.95rem;
    margin-bottom: 1rem;
    color: #555;
  }
  .order-summary-list p {
    margin: 0.2rem 0;
  }
  .total-price {
    font-weight: 700;
    font-size: 1.1rem;
    text-align: right;
    color: #f85c00;
  }
  form label {
    display: block;
    margin-top: 0.75rem;
    font-weight: 600;
    color: #444;
  }
  form input, form textarea, form select {
    width: 100%;
    padding: 0.4rem 0.6rem;
    margin-top: 0.25rem;
    font-size: 1rem;
    border-radius: 6px;
    border: 1.5px solid #ccc;
    resize: vertical;
    font-family: inherit;
  }
  form textarea {
    min-height: 60px;
  }
  button.submit-btn {
    margin-top: 1rem;
    width: 100%;
    padding: 0.75rem;
    background-color: #f85c00;
    color: white;
    font-weight: 700;
    font-size: 1.1rem;
    border: none;
    border-radius: 12px;
    cursor: pointer;
    box-shadow: 0 4px 6px rgb(248 92 0 / 0.7);
    transition: background-color 0.3s ease;
  }
  button.submit-btn:active {
    background-color: #c34800;
  }
  .thank-you-message {
    background: #dff7e0;
    border: 2px solid #4CAF50;
    border-radius: 12px;
    padding: 1rem;
    margin-top: 1rem;
    color: #2e7d32;
    font-weight: 700;
    font-size: 1.2rem;
    text-align: center;
    display: none;
  }
  /* Scrollbar styling for order summary */
  .order-summary-list::-webkit-scrollbar {
    width: 6px;
  }
  .order-summary-list::-webkit-scrollbar-thumb {
    background-color: #f8b500;
    border-radius: 3px;
  }
  /* Responsive footer spacing */
  @media (max-width: 400px) {
    main {
      padding-bottom: 1.5rem;
    }
  }
</style>
</head>
<body>
<header>
  Cireng Bu Yati
</header>
<img class="banner-image" src="https://images.unsplash.com/photo-1625622125155-65de78004dc5?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&q=80&w=600" alt="Banner Cireng Bu Yati" />
<main>
  <section class="product-list" aria-label="Daftar produk cireng">
    <article class="product" data-id="1" data-price="2000" tabindex="0" aria-label="Cireng ayam suwir 3 buah">
      <img src="https://upload.wikimedia.org/wikipedia/commons/6/6d/Cireng.JPG" alt="Cireng ayam suwir 3 buah" />
      <div class="product-details">
        <h3 class="product-title">Cireng Ayam Suwir</h3>
        <p class="product-desc">Isi 3 buah, rasa gurih ayam suwir.</p>
        <p class="product-price">Rp 2.000 / 3 buah</p>
        <div class="quantity-controls" tabindex="-1">
          <button type="button" aria-label="Kurangi jumlah ayam suwir" class="qty-decrease">−</button>
          <input type="number" min="0" max="99" value="0" aria-live="polite" aria-label="Jumlah ayam suwir" />
          <button type="button" aria-label="Tambah jumlah ayam suwir" class="qty-increase">+</button>
        </div>
      </div>
    </article>
    <article class="product" data-id="2" data-price="2000" tabindex="0" aria-label="Cireng isi keju 3 buah">
      <img src="https://upload.wikimedia.org/wikipedia/commons/6/6d/Cireng.JPG" alt="Cireng isi keju 3 buah" />
      <div class="product-details">
        <h3 class="product-title">Cireng Isi Keju</h3>
        <p class="product-desc">Isi 3 buah, keju meleleh gurih.</p>
        <p class="product-price">Rp 2.000 / 3 buah</p>
        <div class="quantity-controls" tabindex="-1">
          <button type="button" aria-label="Kurangi jumlah keju" class="qty-decrease">−</button>
          <input type="number" min="0" max="99" value="0" aria-live="polite" aria-label="Jumlah keju" />
          <button type="button" aria-label="Tambah jumlah keju" class="qty-increase">+</button>
        </div>
      </div>
    </article>
  </section>
  <section class="order-summary" aria-label="Ringkasan pesanan">
    <h2>Ringkasan Pesanan</h2>
    <div class="order-summary-list" aria-live="polite" aria-atomic="true"></div>
    <p class="total-price" aria-label="Total harga pesanan">Total: Rp 0</p>
    <form id="order-form" aria-label="Formulir pemesanan cireng">
      <label for="name">Nama Pemesan</label>
      <input type="text" id="name" name="name" placeholder="Masukkan nama Anda" required autocomplete="name" />
      <label for="phone">Nomor Telepon</label>
      <input type="tel" id="phone" name="phone" placeholder="Contoh: 081234567890" pattern="[0-9+\- ]+" required autocomplete="tel" />
      <label for="address">Alamat Pengiriman</label>
      <textarea id="address" name="address" placeholder="Masukkan alamat lengkap pengiriman" required></textarea>
      <label for="payment">Metode Pembayaran</label>
      <select id="payment" name="payment" required>
        <option value="" disabled selected>Pilih metode pembayaran</option>
        <option value="tunai">Tunai</option>
      </select>
      <label for="delivery">Metode Pengiriman</label>
      <select id="delivery" name="delivery" required>
        <option value="" disabled selected>Pilih metode pengiriman</option>
        <option value="pick_up">Pick Up</option>
      </select>
      <button type="submit" class="submit-btn">Pesan Sekarang</button>
    </form>
    <div class="thank-you-message" role="alert" aria-live="assertive" tabindex="0">
      Terima kasih atas pesanan Anda! 🙏
    </div>
  </section>
</main>
<script>
  (() => {
    const products = Array.from(document.querySelectorAll('.product'));
    const orderSummaryList = document.querySelector('.order-summary-list');
    const totalPriceEl = document.querySelector('.total-price');
    const form = document.getElementById('order-form');
    const thankYouMessage = document.querySelector('.thank-you-message');

    function updateSummary() {
      let total = 0;
      let items = [];
      products.forEach(product => {
        const qtyInput = product.querySelector('input[type="number"]');
        const qty = parseInt(qtyInput.value) || 0;
        if (qty > 0) {
          const title = product.querySelector('.product-title').textContent;
          const price = parseInt(product.dataset.price) || 0;
          const subtotal = qty * price;
          total += subtotal;
          items.push(`${qty} x ${title} = Rp ${subtotal.toLocaleString('id-ID')}`);
        }
      });
      orderSummaryList.innerHTML = items.length > 0 ? items.map(i => '<p>' + i + '</p>').join('') : '<p>Belum ada pesanan.</p>';
      totalPriceEl.textContent = 'Total: Rp ' + total.toLocaleString('id-ID');
      return total;
    }

    // Increase quantity by 1
    function increaseQuantity(input) {
      let val = parseInt(input.value) || 0;
      if (val < 99) {
        input.value = val + 1;
      }
    }

    products.forEach(product => {
      const btnDecrease = product.querySelector('.qty-decrease');
      const btnIncrease = product.querySelector('.qty-increase');
      const qtyInput = product.querySelector('input[type="number"]');

      btnDecrease.addEventListener('click', (e) => {
        e.stopPropagation();
        let val = parseInt(qtyInput.value) || 0;
        if (val > 0) {
          qtyInput.value = val - 1;
          updateSummary();
        }
      });
      btnIncrease.addEventListener('click', (e) => {
        e.stopPropagation();
        increaseQuantity(qtyInput);
        updateSummary();
      });
      qtyInput.addEventListener('input', () => {
        let val = parseInt(qtyInput.value);
        if (isNaN(val) || val < 0) {
          qtyInput.value = 0;
        } else if (val > 99) {
          qtyInput.value = 99;
        }
        updateSummary();
      });

      // Clicking the product (excluding buttons/inputs) increases the quantity by 1
      product.addEventListener('click', (e) => {
        if (e.target.closest('.qty-decrease') || e.target.closest('.qty-increase') || e.target.closest('input[type="number"]')) {
          return;
        }
        increaseQuantity(qtyInput);
        updateSummary();
      });
    });

    form.addEventListener('submit', e => {
      e.preventDefault();
      updateSummary();
      const totalText = totalPriceEl.textContent.replace(/[^\d]/g, '');
      const total = parseInt(totalText) || 0;
      if (total === 0) {
        alert('Silakan pilih produk cireng terlebih dahulu sebelum memesan.');
        return;
      }
      const name = form.name.value.trim();
      const phone = form.phone.value.trim();
      const address = form.address.value.trim();
      const payment = form.payment.value;
      const delivery = form.delivery.value;
      if (!name || !phone || !address || !payment || !delivery) {
        alert('Mohon lengkapi semua data pemesanan.');
        return;
      }
      // Hide form and summary, show thank you message
      form.style.display = 'none';
      orderSummaryList.style.display = 'none';
      totalPriceEl.style.display = 'none';
      thankYouMessage.style.display = 'block';
      thankYouMessage.focus();
    });

    updateSummary();
  })();
</script>
</body>
</html>
</content>
</create_file>
