# E-shop-<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>E-Shop</title>
    <style>
        body {
            margin: 0;
            font-family: Arial, sans-serif;
            background: orange;
            color: #333;
        }

        header {
            text-align: center;
            padding: 50px 20px;
            color: white;
            background: linear-gradient(to bottom, orange, #ff8000);
            position: relative;
            overflow: hidden;
        }

        /* Effet "wave" animé */
        header::after {
            content: "";
            position: absolute;
            bottom: 0;
            left: 0;
            width: 200%;
            height: 100px;
            background: rgba(255,255,255,0.5);
            border-radius: 100% 50%;
            animation: wave 5s infinite linear;
        }
        @keyframes wave {
            from { transform: translateX(0); }
            to { transform: translateX(-50%); }
        }

        nav {
            background: #ff6600;
            text-align: center;
            padding: 15px;
        }
        nav a {
            margin: 0 20px;
            color: white;
            text-decoration: none;
            font-weight: bold;
        }

        section {
            padding: 20px;
        }

        .products, .vendor-products {
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
        }

        .card {
            background: white;
            padding: 15px;
            border-radius: 10px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.2);
            width: 200px;
            text-align: center;
        }

        .card button {
            background: orange;
            border: none;
            padding: 10px;
            margin-top: 10px;
            color: white;
            border-radius: 5px;
            cursor: pointer;
        }

        #cart {
            background: #fff4e6;
            padding: 15px;
            border-radius: 8px;
            margin-top: 20px;
        }
    </style>
</head>
<body>

    <!-- Page d'accueil -->
    <header>
        <h1>Bienvenue sur E-Shop</h1>
        <p>Un espace pour clients et vendeurs</p>
    </header>

    <!-- Menu -->
    <nav>
        <a href="#client">Espace Client</a>
        <a href="#vendeur">Espace Vendeur</a>
    </nav>

    <!-- Espace Client -->
    <section id="client">
        <h2>Espace Client</h2>
        <p>Découvrez nos produits et ajoutez-les à votre panier.</p>
        <div class="products" id="product-list">
            <div class="card">
                <h3>Produit A</h3>
                <p>Prix: 5000 FCFA</p>
                <button onclick="addToCart('Produit A', 5000)">Ajouter au panier</button>
            </div>
            <div class="card">
                <h3>Produit B</h3>
                <p>Prix: 7500 FCFA</p>
                <button onclick="addToCart('Produit B', 7500)">Ajouter au panier</button>
            </div>
        </div>

        <div id="cart">
            <h3>🛒 Panier</h3>
            <ul id="cart-items"></ul>
            <p><strong>Total:</strong> <span id="cart-total">0</span> FCFA</p>
        </div>
    </section>

    <!-- Espace Vendeur -->
    <section id="vendeur">
        <h2>Espace Vendeur</h2>
        <p>Publiez vos produits :</p>
        <form id="vendor-form">
            <input type="text" id="vendor-product-name" placeholder="Nom du produit" required>
            <input type="number" id="vendor-product-price" placeholder="Prix (FCFA)" required>
            <button type="submit">Publier</button>
        </form>

        <h3>Mes Produits :</h3>
        <div class="vendor-products" id="vendor-products"></div>
    </section>

    <script>
        // Panier client
        let cart = [];
        function addToCart(product, price) {
            cart.push({product, price});
            updateCart();
        }
        function updateCart() {
            let cartList = document.getElementById('cart-items');
            cartList.innerHTML = "";
            let total = 0;
            cart.forEach(item => {
                let li = document.createElement('li');
                li.textContent = item.product + " - " + item.price + " FCFA";
                cartList.appendChild(li);
                total += item.price;
            });
            document.getElementById('cart-total').textContent = total;
        }

        // Espace vendeur
        document.getElementById("vendor-form").addEventListener("submit", function(e){
            e.preventDefault();
            let name = document.getElementById("vendor-product-name").value;
            let price = document.getElementById("vendor-product-price").value;

            let div = document.createElement("div");
            div.classList.add("card");
            div.innerHTML = `<h3>${name}</h3><p>Prix: ${price} FCFA</p>
                             <button onclick="addToCart('${name}', ${price})">Ajouter au panier</button>`;
            
            document.getElementById("vendor-products").appendChild(div);
            document.getElementById("vendor-form").reset();
        });
    </script>

</body>
</html>
