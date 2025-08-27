v<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>E-Shop - Votre marketplace en ligne</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .animate-fadeIn {
            animation: fadeIn 0.5s ease-out forwards;
        }
        
        .customer-section {
            background: linear-gradient(135deg, rgba(255,165,0,0.9) 0%, rgba(255,140,0,0.9) 100%);
            backdrop-filter: blur(10px);
        }
        
        .seller-section {
            background: linear-gradient(135deg, rgba(0,128,0,0.9) 0%, rgba(34,139,34,0.9) 100%);
            backdrop-filter: blur(10px);
        }
        
        .logo-3d {
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3),
                         4px 4px 6px rgba(0,0,0,0.2),
                         6px 6px 8px rgba(0,0,0,0.1);
            transform: perspective(500px) rotateX(10deg);
        }
        
        .product-card {
            transition: all 0.3s ease;
            transform-style: preserve-3d;
        }
        
        .product-card:hover {
            transform: translateY(-5px) rotateX(5deg);
            box-shadow: 0 10px 25px rgba(0,0,0,0.15);
        }
        
        .cart-item {
            transition: all 0.3s ease;
        }
        
        .cart-item:hover {
            background-color: rgba(255, 255, 255, 0.1);
            transform: translateX(5px);
        }
        
        .floating-btn {
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
            transition: all 0.3s ease;
        }
        
        .floating-btn:hover {
            transform: translateY(-3px) scale(1.05);
            box-shadow: 0 8px 20px rgba(0,0,0,0.25);
        }
        
        .modal-enter {
            opacity: 0;
            transform: scale(0.95);
        }
        
        .modal-enter-active {
            opacity: 1;
            transform: scale(1);
            transition: all 0.2s ease;
        }
        
        .modal-exit {
            opacity: 1;
            transform: scale(1);
        }
        
        .modal-exit-active {
            opacity: 0;
            transform: scale(0.95);
            transition: all 0.2s ease;
        }
        
        .sidebar-enter {
            transform: translateX(100%);
        }
        
        .sidebar-enter-active {
            transform: translateX(0);
            transition: transform 0.3s ease-out;
        }
        
        .sidebar-exit {
            transform: translateX(0);
        }
        
        .sidebar-exit-active {
            transform: translateX(100%);
            transition: transform 0.3s ease-in;
        }
        
        .scrollbar-hide::-webkit-scrollbar {
            display: none;
        }
        
        .scrollbar-hide {
            -ms-overflow-style: none;
            scrollbar-width: none;
        }
    </style>
</head>
<body class="bg-gray-100 min-h-screen font-sans">
    <!-- Header -->
    <header class="bg-white shadow-lg sticky top-0 z-40">
        <div class="container mx-auto px-4 py-3 flex flex-col md:flex-row items-center justify-between">
            <div class="flex items-center mb-4 md:mb-0">
                <div class="logo-3d text-4xl font-bold text-orange-500 mr-2">
                    <i class="fas fa-shopping-bag"></i>
                </div>
                <h1 class="logo-3d text-3xl font-bold text-gray-800">E-Shop</h1>
            </div>
            
            <nav class="flex space-x-6">
                <a href="#customer" class="text-orange-500 font-semibold hover:text-orange-700 transition-colors duration-300">
                    <i class="fas fa-user mr-1"></i> Espace Client
                </a>
                <a href="#seller" class="text-green-600 font-semibold hover:text-green-800 transition-colors duration-300">
                    <i class="fas fa-store mr-1"></i> Espace Vendeur
                </a>
                <a href="#contact" class="text-gray-600 hover:text-gray-800 transition-colors duration-300">
                    <i class="fas fa-envelope mr-1"></i> Contact
                </a>
            </nav>
        </div>
    </header>

    <main class="container mx-auto px-4 py-8">
        <!-- Customer Section -->
        <section id="customer" class="customer-section rounded-xl p-6 mb-8 shadow-lg animate-fadeIn">
            <div class="flex justify-between items-center mb-6">
                <h2 class="text-3xl font-bold text-white">
                    <i class="fas fa-shopping-basket mr-2"></i> Espace Client
                </h2>
                <div class="relative">
                    <div id="notificationBell" class="text-white text-2xl cursor-pointer relative">
                        <i class="fas fa-bell"></i>
                        <span class="absolute -top-1 -right-1 bg-red-500 text-white text-xs rounded-full h-5 w-5 flex items-center justify-center">3</span>
                    </div>
                    <div id="notificationDropdown" class="hidden absolute right-0 mt-2 w-64 bg-white rounded-md shadow-lg z-50 p-2">
                        <div class="text-sm text-gray-700 p-2 border-b">
                            <i class="fas fa-shipping-fast text-orange-500 mr-2"></i>
                            Votre commande #1234 a été expédiée
                        </div>
                        <div class="text-sm text-gray-700 p-2 border-b">
                            <i class="fas fa-tag text-green-500 mr-2"></i>
                            Nouvelle réduction sur les smartphones
                        </div>
                        <div class="text-sm text-gray-700 p-2">
                            <i class="fas fa-star text-yellow-500 mr-2"></i>
                            Évaluez votre dernière commande
                        </div>
                    </div>
                </div>
            </div>

            <!-- Product Filter -->
            <div class="bg-white bg-opacity-90 rounded-xl p-4 mb-6 shadow-md">
                <div class="flex flex-wrap items-center justify-between gap-4">
                    <div class="flex-1 min-w-[200px]">
                        <label for="category" class="block text-sm font-medium text-gray-700 mb-1">Catégorie</label>
                        <div class="relative">
                            <select id="category" class="appearance-none block w-full pl-3 pr-10 py-2 text-base border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-orange-500 focus:border-orange-500 sm:text-sm bg-white">
                                <option>Tous</option>
                                <option>Électronique</option>
                                <option>Mode</option>
                                <option>Maison</option>
                                <option>Beauté</option>
                            </select>
                            <div class="absolute inset-y-0 right-0 flex items-center pr-2 pointer-events-none">
                                <i class="fas fa-chevron-down text-gray-400"></i>
                            </div>
                        </div>
                    </div>
                    
                    <div class="flex-1 min-w-[200px]">
                        <label for="sort" class="block text-sm font-medium text-gray-700 mb-1">Trier par</label>
                        <div class="relative">
                            <select id="sort" class="appearance-none block w-full pl-3 pr-10 py-2 text-base border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-orange-500 focus:border-orange-500 sm:text-sm bg-white">
                                <option>Pertinence</option>
                                <option>Prix croissant</option>
                                <option>Prix décroissant</option>
                                <option>Nouveautés</option>
                            </select>
                            <div class="absolute inset-y-0 right-0 flex items-center pr-2 pointer-events-none">
                                <i class="fas fa-chevron-down text-gray-400"></i>
                            </div>
                        </div>
                    </div>
                    
                    <div class="flex-1 min-w-[250px]">
                        <label class="block text-sm font-medium text-gray-700 mb-1">Rechercher</label>
                        <div class="relative">
                            <input type="text" placeholder="Rechercher un produit..." class="block w-full pl-10 pr-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-orange-500 focus:border-orange-500">
                            <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
                                <i class="fas fa-search text-gray-400"></i>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Special Offers -->
            <div class="mb-8">
                <h3 class="text-xl font-bold text-white mb-4 flex items-center">
                    <i class="fas fa-percentage mr-2"></i> Offres spéciales
                </h3>
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                    <div class="bg-white bg-opacity-90 rounded-xl p-4 shadow-md flex items-center">
                        <div class="bg-orange-100 p-3 rounded-lg mr-4">
                            <i class="fas fa-tag text-orange-500 text-2xl"></i>
                        </div>
                        <div>
                            <h4 class="font-bold">Réduction de 20%</h4>
                            <p class="text-sm text-gray-600">Sur tous les smartphones ce weekend</p>
                        </div>
                    </div>
                    <div class="bg-white bg-opacity-90 rounded-xl p-4 shadow-md flex items-center">
                        <div class="bg-green-100 p-3 rounded-lg mr-4">
                            <i class="fas fa-shipping-fast text-green-500 text-2xl"></i>
                        </div>
                        <div>
                            <h4 class="font-bold">Livraison gratuite</h4>
                            <p class="text-sm text-gray-600">Pour les commandes supérieures à 50,000 XAF</p>
                        </div>
                    </div>
                    <div class="bg-white bg-opacity-90 rounded-xl p-4 shadow-md flex items-center">
                        <div class="bg-blue-100 p-3 rounded-lg mr-4">
                            <i class="fas fa-gift text-blue-500 text-2xl"></i>
                        </div>
                        <div>
                            <h4 class="font-bold">Cadeau surprise</h4>
                            <p class="text-sm text-gray-600">Pour les 10 premières commandes aujourd'hui</p>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Product Grid -->
            <h3 class="text-xl font-bold text-white mb-4 flex items-center">
                <i class="fas fa-box-open mr-2"></i> Nos produits
            </h3>
            <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6" id="productGrid">
                <!-- Products will be loaded here dynamically -->
            </div>

            <!-- Product Modal -->
            <div id="productModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 hidden">
                <div class="bg-white rounded-xl w-full max-w-4xl max-h-[90vh] overflow-y-auto scrollbar-hide">
                    <div class="p-6">
                        <div class="flex justify-between items-start">
                            <h3 id="modalProductName" class="text-2xl font-bold"></h3>
                            <button id="closeModal" class="text-gray-500 hover:text-gray-700 transition-colors duration-300">
                                <i class="fas fa-times text-xl"></i>
                            </button>
                        </div>
                        
                        <div class="mt-4 grid grid-cols-1 md:grid-cols-2 gap-6">
                            <div>
                                <div class="relative">
                                    <img id="modalProductImage" src="" alt="" class="w-full h-64 md:h-80 object-contain rounded-lg bg-gray-100">
                                    <div class="absolute top-2 left-2 bg-orange-500 text-white text-xs font-bold px-2 py-1 rounded">
                                        <i class="fas fa-tag mr-1"></i> PROMO
                                    </div>
                                </div>
                                <div class="mt-4 flex space-x-2 overflow-x-auto pb-2">
                                    <!-- Thumbnails will be added here -->
                                </div>
                            </div>
                            
                            <div>
                                <div class="flex items-center mb-2">
                                    <div class="flex items-center">
                                        <i class="fas fa-star text-yellow-400"></i>
                                        <span class="ml-1 text-gray-700">4.8</span>
                                        <span class="mx-2 text-gray-300">|</span>
                                        <span class="text-gray-700">128 avis</span>
                                    </div>
                                    <span class="ml-4 text-sm text-green-600 font-medium">
                                        <i class="fas fa-check-circle mr-1"></i> En stock
                                    </span>
                                </div>
                                
                                <div class="flex items-center mb-4">
                                    <span id="modalProductPrice" class="text-3xl font-bold text-orange-600"></span>
                                    <span class="ml-2 text-sm text-gray-500">FCFA</span>
                                    <span class="ml-4 text-sm line-through text-gray-400">150,000 FCFA</span>
                                </div>
                                
                                <p id="modalProductDescription" class="text-gray-700 mb-6"></p>
                                
                                <div class="mb-6">
                                    <h4 class="font-medium mb-2">Options disponibles</h4>
                                    <div class="flex flex-wrap gap-2">
                                        <button class="px-3 py-1 border border-gray-300 rounded-full text-sm hover:bg-gray-100 transition-colors duration-300">
                                            64GB
                                        </button>
                                        <button class="px-3 py-1 border border-gray-300 rounded-full text-sm hover:bg-gray-100 transition-colors duration-300">
                                            128GB
                                        </button>
                                        <button class="px-3 py-1 border border-gray-300 rounded-full text-sm hover:bg-gray-100 transition-colors duration-300">
                                            256GB
                                        </button>
                                        <button class="px-3 py-1 border border-gray-300 rounded-full text-sm hover:bg-gray-100 transition-colors duration-300">
                                            Noir
                                        </button>
                                        <button class="px-3 py-1 border border-gray-300 rounded-full text-sm hover:bg-gray-100 transition-colors duration-300">
                                            Bleu
                                        </button>
                                    </div>
                                </div>
                                
                                <div class="flex items-center mb-6">
                                    <button id="decreaseQty" class="bg-gray-200 px-3 py-1 rounded-l-md hover:bg-gray-300 transition-colors duration-300">
                                        <i class="fas fa-minus"></i>
                                    </button>
                                    <span id="productQty" class="bg-gray-100 px-4 py-1 border-t border-b border-gray-200">1</span>
                                    <button id="increaseQty" class="bg-gray-200 px-3 py-1 rounded-r-md hover:bg-gray-300 transition-colors duration-300">
                                        <i class="fas fa-plus"></i>
                                    </button>
                                    <span class="ml-4 text-sm text-gray-500">
                                        Disponible: <span id="modalProductStock" class="font-medium"></span>
                                    </span>
                                </div>
                                
                                <div class="flex flex-col sm:flex-row gap-4">
                                    <button id="addToCartFromModal" class="flex-1 bg-orange-500 hover:bg-orange-600 text-white px-6 py-3 rounded-md flex items-center justify-center transition-colors duration-300">
                                        <i class="fas fa-shopping-cart mr-2"></i> Ajouter au panier
                                    </button>
                                    <button class="flex-1 border border-orange-500 text-orange-500 hover:bg-orange-50 px-6 py-3 rounded-md flex items-center justify-center transition-colors duration-300">
                                        <i class="far fa-heart mr-2"></i> Favoris
                                    </button>
                                </div>
                                
                                <div class="mt-6 pt-6 border-t border-gray-200">
                                    <h4 class="font-medium mb-2">Livraison et retours</h4>
                                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4 text-sm">
                                        <div class="flex items-start">
                                            <i class="fas fa-truck text-gray-500 mt-1 mr-2"></i>
                                            <div>
                                                <p class="font-medium">Livraison standard</p>
                                                <p class="text-gray-600">2,000 FCFA - Livré dans 3-5 jours ouvrables</p>
                                            </div>
                                        </div>
                                        <div class="flex items-start">
                                            <i class="fas fa-undo-alt text-gray-500 mt-1 mr-2"></i>
                                            <div>
                                                <p class="font-medium">Retours faciles</p>
                                                <p class="text-gray-600">Retours gratuits sous 14 jours</p>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Cart Sidebar -->
            <div id="cartSidebar" class="fixed top-0 right-0 h-full w-full md:w-96 bg-white shadow-lg transform translate-x-full transition-transform duration-300 ease-in-out z-50 overflow-y-auto scrollbar-hide">
                <div class="p-6">
                    <div class="flex justify-between items-center mb-6">
                        <h3 class="text-2xl font-bold flex items-center">
                            <i class="fas fa-shopping-cart mr-2 text-orange-500"></i> Votre Panier
                        </h3>
                        <button id="closeCart" class="text-gray-500 hover:text-gray-700 transition-colors duration-300">
                            <i class="fas fa-times text-xl"></i>
                        </button>
                    </div>
                    
                    <div id="cartItems" class="mb-6">
                        <!-- Cart items will be added here -->
                        <div class="text-center py-12 text-gray-500">
                            <i class="fas fa-shopping-cart text-4xl mb-4 opacity-30"></i>
                            <p class="text-lg">Votre panier est vide</p>
                            <p class="text-sm mt-2">Commencez à ajouter des produits</p>
                            <button id="continueShopping" class="mt-4 bg-orange-500 hover:bg-orange-600 text-white px-6 py-2 rounded-md transition-colors duration-300">
                                <i class="fas fa-store mr-2"></i> Continuer vos achats
                            </button>
                        </div>
                    </div>
                    
                    <div id="cartSummary" class="border-t border-gray-200 pt-4 hidden">
                        <div class="flex justify-between mb-2">
                            <span class="text-gray-600">Sous-total</span>
                            <span id="cartSubtotal" class="font-medium">0 FCFA</span>
                        </div>
                        <div class="flex justify-between mb-2">
                            <span class="text-gray-600">Livraison</span>
                            <span class="font-medium">Calculé à l'étape suivante</span>
                        </div>
                        <div class="flex justify-between text-lg font-bold mt-4 mb-2">
                            <span>Total</span>
                            <span id="cartTotal" class="text-orange-600">0 FCFA</span>
                        </div>
                        <p class="text-xs text-gray-500 mb-4">
                            <i class="fas fa-info-circle mr-1"></i> Taxes incluses le cas échéant
                        </p>
                        
                        <button id="checkoutBtn" class="w-full bg-orange-500 hover:bg-orange-600 text-white py-3 rounded-md shadow-md transition-colors duration-300">
                            <i class="fas fa-credit-card mr-2"></i> Passer la commande
                        </button>
                        
                        <div class="mt-4 flex justify-center">
                            <img src="https://via.placeholder.com/200x30?text=Payment+Methods" alt="Méthodes de paiement" class="h-8 opacity-70">
                        </div>
                    </div>
                </div>
            </div>

            <!-- Cart Button -->
            <div class="fixed bottom-6 right-6 z-40">
                <button id="openCart" class="floating-btn bg-orange-500 hover:bg-orange-600 text-white p-4 rounded-full shadow-lg flex items-center transition-all duration-300">
                    <i class="fas fa-shopping-cart text-xl"></i>
                    <span id="cartCount" class="ml-2 bg-white text-orange-500 rounded-full w-6 h-6 flex items-center justify-center text-sm font-bold">0</span>
                </button>
            </div>
        </section>

        <!-- Seller Section -->
        <section id="seller" class="seller-section rounded-xl p-6 shadow-lg animate-fadeIn">
            <h2 class="text-3xl font-bold text-white mb-6">
                <i class="fas fa-store-alt mr-2"></i> Espace Vendeur
            </h2>

            <!-- Stats Cards -->
            <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-6">
                <div class="bg-white bg-opacity-90 rounded-xl p-4 shadow-md">
                    <div class="flex justify-between items-center">
                        <div>
                            <p class="text-sm text-gray-500">Ventes ce mois</p>
                            <p class="text-2xl font-bold">245,000 XAF</p>
                        </div>
                        <div class="bg-green-100 p-3 rounded-lg">
                            <i class="fas fa-chart-line text-green-500 text-xl"></i>
                        </div>
                    </div>
                    <p class="text-xs text-green-600 mt-2">
                        <i class="fas fa-arrow-up mr-1"></i> 12% par rapport au mois dernier
                    </p>
                </div>
                
                <div class="bg-white bg-opacity-90 rounded-xl p-4 shadow-md">
                    <div class="flex justify-between items-center">
                        <div>
                            <p class="text-sm text-gray-500">Commandes en cours</p>
                            <p class="text-2xl font-bold">8</p>
                        </div>
                        <div class="bg-blue-100 p-3 rounded-lg">
                            <i class="fas fa-shopping-bag text-blue-500 text-xl"></i>
                        </div>
                    </div>
                    <p class="text-xs text-blue-600 mt-2">
                        <i class="fas fa-clock mr-1"></i> 2 nécessitent votre attention
                    </p>
                </div>
                
                <div class="bg-white bg-opacity-90 rounded-xl p-4 shadow-md">
                    <div class="flex justify-between items-center">
                        <div>
                            <p class="text-sm text-gray-500">Évaluations</p>
                            <p class="text-2xl font-bold">4.7/5</p>
                        </div>
                        <div class="bg-yellow-100 p-3 rounded-lg">
                            <i class="fas fa-star text-yellow-500 text-xl"></i>
                        </div>
                    </div>
                    <p class="text-xs text-gray-600 mt-2">
                        <i class="fas fa-comment-alt mr-1"></i> 32 nouveaux avis
                    </p>
                </div>
            </div>

            <!-- Subscription Info -->
            <div class="bg-white bg-opacity-90 rounded-xl p-4 mb-6 shadow-md">
                <div class="flex flex-col md:flex-row justify-between items-center">
                    <div class="mb-4 md:mb-0">
                        <h3 class="font-bold text-lg flex items-center">
                            <i class="fas fa-crown text-yellow-500 mr-2"></i> Abonnement Vendeur
                        </h3>
                        <p class="text-gray-700">
                            <i class="fas fa-gift text-green-500 mr-1"></i> Premier mois gratuit, puis 15,000 XAF/mois
                        </p>
                        <p id="subscriptionStatus" class="text-sm text-green-600 mt-1">
                            <i class="fas fa-clock mr-1"></i> Vous êtes en période d'essai gratuit (expire dans 25 jours)
                        </p>
                    </div>
                    <button id="subscribeBtn" class="bg-green-600 hover:bg-green-700 text-white px-6 py-2 rounded-md shadow-md transition-colors duration-300">
                        <i class="fas fa-rocket mr-2"></i> S'abonner maintenant
                    </button>
                </div>
            </div>

            <!-- Quick Actions -->
            <div class="mb-6">
                <h3 class="text-xl font-bold text-white mb-4">
                    <i class="fas fa-bolt mr-2"></i> Actions rapides
                </h3>
                <div class="grid grid-cols-2 sm:grid-cols-4 gap-4">
                    <button class="bg-white bg-opacity-90 hover:bg-opacity-100 rounded-lg p-3 shadow-md flex flex-col items-center transition-all duration-300">
                        <div class="bg-blue-100 p-3 rounded-full mb-2">
                            <i class="fas fa-plus text-blue-500"></i>
                        </div>
                        <span class="text-sm font-medium">Ajouter produit</span>
                    </button>
                    <button class="bg-white bg-opacity-90 hover:bg-opacity-100 rounded-lg p-3 shadow-md flex flex-col items-center transition-all duration-300">
                        <div class="bg-green-100 p-3 rounded-full mb-2">
                            <i class="fas fa-truck text-green-500"></i>
                        </div>
                        <span class="text-sm font-medium">Expédier commandes</span>
                    </button>
                    <button class="bg-white bg-opacity-90 hover:bg-opacity-100 rounded-lg p-3 shadow-md flex flex-col items-center transition-all duration-300">
                        <div class="bg-purple-100 p-3 rounded-full mb-2">
                            <i class="fas fa-chart-pie text-purple-500"></i>
                        </div>
                        <span class="text-sm font-medium">Statistiques</span>
                    </button>
                    <button class="bg-white bg-opacity-90 hover:bg-opacity-100 rounded-lg p-3 shadow-md flex flex-col items-center transition-all duration-300">
                        <div class="bg-orange-100 p-3 rounded-full mb-2">
                            <i class="fas fa-tag text-orange-500"></i>
                        </div>
                        <span class="text-sm font-medium">Promotions</span>
                    </button>
                </div>
            </div>

            <!-- Add Product Form -->
            <div class="bg-white bg-opacity-90 rounded-xl p-6 mb-6 shadow-md">
                <h3 class="font-bold text-lg mb-4 flex items-center">
                    <i class="fas fa-plus-circle text-green-500 mr-2"></i> Ajouter un nouveau produit
                </h3>
                <form id="productForm" class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <div>
                        <label for="productName" class="block text-sm font-medium text-gray-700 mb-1">Nom du produit*</label>
                        <input type="text" id="productName" class="mt-1 block w-full border border-gray-300 rounded-md shadow-sm focus:border-green-500 focus:ring-green-500 p-2">
                    </div>
                    <div>
                        <label for="productPrice" class="block text-sm font-medium text-gray-700 mb-1">Prix (XAF)*</label>
                        <input type="number" id="productPrice" class="mt-1 block w-full border border-gray-300 rounded-md shadow-sm focus:border-green-500 focus:ring-green-500 p-2">
                    </div>
                    <div>
                        <label for="productCategory" class="block text-sm font-medium text-gray-700 mb-1">Catégorie*</label>
                        <select id="productCategory" class="mt-1 block w-full border border-gray-300 rounded-md shadow-sm focus:border-green-500 focus:ring-green-500 p-2">
                            <option>Électronique</option>
                            <option>Mode</option>
                            <option>Maison</option>
                            <option>Beauté</option>
                            <option>Autre</option>
                        </select>
                    </div>
                    <div>
                        <label for="productStock" class="block text-sm font-medium text-gray-700 mb-1">Quantité disponible*</label>
                        <input type="number" id="productStock" class="mt-1 block w-full border border-gray-300 rounded-md shadow-sm focus:border-green-500 focus:ring-green-500 p-2">
                    </div>
                    <div class="md:col-span-2">
                        <label for="productDescription" class="block text-sm font-medium text-gray-700 mb-1">Description*</label>
                        <textarea id="productDescription" rows="3" class="mt-1 block w-full border border-gray-300 rounded-md shadow-sm focus:border-green-500 focus:ring-green-500 p-2"></textarea>
                    </div>
                    <div class="md:col-span-2">
                        <label class="block text-sm font-medium text-gray-700 mb-1">Images du produit*</label>
                        <div class="mt-1 flex justify-center px-6 pt-5 pb-6 border-2 border-gray-300 border-dashed rounded-md hover:border-green-500 transition-colors duration-300">
                            <div class="space-y-1 text-center">
                                <div class="flex text-sm text-gray-600 justify-center">
                                    <label for="productImages" class="relative cursor-pointer bg-white rounded-md font-medium text-green-600 hover:text-green-500 focus-within:outline-none">
                                        <span>Télécharger des fichiers</span>
                                        <input id="productImages" type="file" multiple class="sr-only">
                                    </label>
                                    <p class="pl-1">ou glisser-déposer</p>
                                </div>
                                <p class="text-xs text-gray-500">
                                    PNG, JPG, GIF jusqu'à 10MB
                                </p>
                            </div>
                        </div>
                        <div id="imagePreviews" class="mt-2 grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 gap-2">
                            <!-- Image previews will appear here -->
                        </div>
                    </div>
                    <div class="md:col-span-2 flex justify-end space-x-4">
                        <button type="reset" class="px-4 py-2 border border-gray-300 rounded-md shadow-sm text-sm font-medium text-gray-700 bg-white hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-green-500">
                            Annuler
                        </button>
                        <button type="submit" class="px-4 py-2 border border-transparent rounded-md shadow-sm text-sm font-medium text-white bg-green-600 hover:bg-green-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-green-500">
                            <i class="fas fa-save mr-2"></i> Enregistrer le produit
                        </button>
                    </div>
                </form>
            </div>

            <!-- Seller's Products -->
            <div class="bg-white bg-opacity-90 rounded-xl p-6 shadow-md">
                <div class="flex justify-between items-center mb-4">
                    <h3 class="font-bold text-lg flex items-center">
                        <i class="fas fa-boxes mr-2"></i> Vos produits
                    </h3>
                    <div class="relative">
                        <input type="text" placeholder="Rechercher un produit..." class="pl-8 pr-4 py-1 border border-gray-300 rounded-md text-sm focus:outline-none focus:ring-2 focus:ring-green-500 focus:border-green-500">
                        <i class="fas fa-search absolute left-2 top-2 text-gray-400"></i>
                    </div>
                </div>
                
                <div class="overflow-x-auto">
                    <table class="min-w-full divide-y divide-gray-200">
                        <thead class="bg-gray-50">
                            <tr>
                                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Produit</th>
                                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Prix</th>
                                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Stock</th>
                                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Statut</th>
                                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Actions</th>
                            </tr>
                        </thead>
                        <tbody id="sellerProducts" class="bg-white divide-y divide-gray-200">
                            <!-- Seller's products will be listed here -->
                            <tr>
                                <td colspan="5" class="px-6 py-4 text-center text-gray-500">
                                    <i class="fas fa-box-open text-3xl mb-2 opacity-30"></i>
                                    <p>Aucun produit ajouté</p>
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
                
                <div class="mt-4 flex justify-between items-center">
                    <div class="text-sm text-gray-500">
                        Affichage de <span class="font-medium">0</span> à <span class="font-medium">0</span> sur <span class="font-medium">0</span> produits
                    </div>
                    <div class="flex space-x-2">
                        <button class="px-3 py-1 border border-gray-300 rounded-md text-sm font-medium text-gray-700 bg-white hover:bg-gray-50">
                            Précédent
                        </button>
                        <button class="px-3 py-1 border border-gray-300 rounded-md text-sm font-medium text-gray-700 bg-white hover:bg-gray-50">
                            Suivant
                        </button>
                    </div>
                </div>
            </div>
        </section>

        <!-- Checkout Modal -->
        <div id="checkoutModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 hidden">
            <div class="bg-white rounded-xl max-w-md w-full max-h-[90vh] overflow-y-auto scrollbar-hide">
                <div class="p-6">
                    <div class="flex justify-between items-start mb-6">
                        <h3 class="text-2xl font-bold flex items-center">
                            <i class="fas fa-credit-card mr-2 text-orange-500"></i> Finaliser votre commande
                        </h3>
                        <button id="closeCheckoutModal" class="text-gray-500 hover:text-gray-700 transition-colors duration-300">
                            <i class="fas fa-times text-xl"></i>
                        </button>
                    </div>
                    
                    <div class="mb-6">
                        <h4 class="font-medium mb-2 flex items-center">
                            <i class="fas fa-map-marker-alt mr-2 text-orange-500"></i> Adresse de livraison
                        </h4>
                        <div class="border border-gray-200 rounded-md p-4">
                            <div class="flex items-center mb-3">
                                <i class="fas fa-user mr-2 text-gray-500"></i>
                                <input type="text" placeholder="Nom complet*" class="w-full border-b border-gray-200 pb-1 focus:outline-none focus:border-orange-500">
                            </div>
                            <div class="flex items-center mb-3">
                                <i class="fas fa-phone mr-2 text-gray-500"></i>
                                <input type="tel" placeholder="Téléphone*" class="w-full border-b border-gray-200 pb-1 focus:outline-none focus:border-orange-500">
                            </div>
                            <div class="flex items-center mb-3">
                                <i class="fas fa-map-marker-alt mr-2 text-gray-500"></i>
                                <textarea placeholder="Adresse complète*" rows="2" class="w-full border-b border-gray-200 pb-1 focus:outline-none focus:border-orange-500"></textarea>
                            </div>
                            <div class="flex items-center">
                                <i class="fas fa-city mr-2 text-gray-500"></i>
                                <input type="text" placeholder="Ville*" class="w-full border-b border-gray-200 pb-1 focus:outline-none focus:border-orange-500">
                            </div>
                        </div>
                    </div>
                    
                    <div class="mb-6">
                        <h4 class="font-medium mb-2 flex items-center">
                            <i class="fas fa-money-bill-wave mr-2 text-orange-500"></i> Méthode de paiement
                        </h4>
                        <div class="space-y-3">
                            <div class="flex items-center p-3 border border-gray-200 rounded-md hover:border-orange-500 transition-colors duration-300">
                                <input type="radio" id="mobileMoney" name="payment" class="h-4 w-4 text-orange-600 focus:ring-orange-500">
                                <label for="mobileMoney" class="ml-3 flex items-center">
                                    <i class="fas fa-mobile-alt mr-2 text-purple-500"></i>
                                    <span>Mobile Money (MTN, Orange)</span>
                                </label>
                            </div>
                            <div class="flex items-center p-3 border border-gray-200 rounded-md hover:border-orange-500 transition-colors duration-300">
                                <input type="radio" id="bankTransfer" name="payment" class="h-4 w-4 text-orange-600 focus:ring-orange-500">
                                <label for="bankTransfer" class="ml-3 flex items-center">
                                    <i class="fas fa-university mr-2 text-blue-500"></i>
                                    <span>Virement bancaire</span>
                                </label>
                            </div>
                            <div class="flex items-center p-3 border border-gray-200 rounded-md hover:border-orange-500 transition-colors duration-300">
                                <input type="radio" id="cashOnDelivery" name="payment" class="h-4 w-4 text-orange-600 focus:ring-orange-500">
                                <label for="cashOnDelivery" class="ml-3 flex items-center">
                                    <i class="fas fa-money-bill-wave mr-2 text-green-500"></i>
                                    <span>Paiement à la livraison</span>
                                </label>
                            </div>
                        </div>
                    </div>
                    
                    <div class="border-t border-gray-200 pt-4">
                        <div class="flex justify-between mb-2">
                            <span class="text-gray-600">Sous-total</span>
                            <span id="checkoutSubtotal" class="font-medium">0 FCFA</span>
                        </div>
                        <div class="flex justify-between mb-2">
                            <span class="text-gray-600">Livraison</span>
                            <span class="font-medium">2,000 FCFA</span>
                        </div>
                        <div class="flex justify-between text-lg font-bold mt-4 mb-2">
                            <span>Total</span>
                            <span id="checkoutTotal" class="text-orange-600">0 FCFA</span>
                        </div>
                        
                        <button id="confirmOrder" class="w-full bg-orange-500 hover:bg-orange-600 text-white py-3 rounded-md shadow-md transition-colors duration-300 mt-4">
                            <i class="fas fa-check-circle mr-2"></i> Confirmer la commande
                        </button>
                        
                        <p class="text-xs text-gray-500 mt-3 text-center">
                            En passant commande, vous acceptez nos <a href="#" class="text-orange-500 hover:underline">Conditions générales</a>
                        </p>
                    </div>
                </div>
            </div>
        </div>

        <!-- Subscription Modal -->
        <div id="subscriptionModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 hidden">
            <div class="bg-white rounded-xl max-w-md w-full max-h-[90vh] overflow-y-auto scrollbar-hide">
                <div class="p-6">
                    <div class="flex justify-between items-start mb-6">
                        <h3 class="text-2xl font-bold flex items-center">
                            <i class="fas fa-crown text-yellow-500 mr-2"></i> Abonnement Vendeur
                        </h3>
                        <button id="closeSubscriptionModal" class="text-gray-500 hover:text-gray-700 transition-colors duration-300">
                            <i class="fas fa-times text-xl"></i>
                        </button>
                    </div>
                    
                    <div class="mb-6">
                        <p class="text-gray-700 mb-4">
                            Abonnez-vous pour continuer à vendre sur E-Shop après votre période d'essai gratuit.
                        </p>
                        
                        <div class="bg-green-50 border-l-4 border-green-500 p-4 mb-4">
                            <div class="flex">
                                <div class="flex-shrink-0">
                                    <i class="fas fa-info-circle text-green-500"></i>
                                </div>
                                <div class="ml-3">
                                    <p class="text-sm text-green-700">
                                        Vous serez averti 5 jours avant la fin de votre abonnement.
                                    </p>
                                </div>
                            </div>
                        </div>
                        
                        <div class="border border-gray-200 rounded-md p-4 mb-2">
                            <div class="flex justify-between items-center mb-2">
                                <span class="font-medium">Abonnement mensuel</span>
                                <span class="text-green-600 font-bold">15,000 FCFA/mois</span>
                            </div>
                            <div class="text-sm text-gray-500">
                                <p>Facturé mensuellement. Annulation possible à tout moment.</p>
                            </div>
                        </div>
                        
                        <div class="flex items-center text-sm text-gray-500">
                            <i class="fas fa-check-circle text-green-500 mr-2"></i>
                            <span>Accès à toutes les fonctionnalités vendeur</span>
                        </div>
                        <div class="flex items-center text-sm text-gray-500 mt-1">
                            <i class="fas fa-check-circle text-green-500 mr-2"></i>
                            <span>Support prioritaire</span>
                        </div>
                        <div class="flex items-center text-sm text-gray-500 mt-1">
                            <i class="fas fa-check-circle text-green-500 mr-2"></i>
                            <span>Statistiques avancées</span>
                        </div>
                    </div>
                    
                    <div class="mb-6">
                        <h4 class="font-medium mb-2 flex items-center">
                            <i class="fas fa-credit-card mr-2 text-green-500"></i> Méthode de paiement
                        </h4>
                        <div class="space-y-3">
                            <div class="flex items-center p-3 border border-gray-200 rounded-md hover:border-green-500 transition-colors duration-300">
                                <input type="radio" id="subMobileMoney" name="subPayment" class="h-4 w-4 text-green-600 focus:ring-green-500">
                                <label for="subMobileMoney" class="ml-3 flex items-center">
                                    <i class="fas fa-mobile-alt mr-2 text-purple-500"></i>
                                    <span>Mobile Money (MTN, Orange)</span>
                                </label>
                            </div>
                            <div class="flex items-center p-3 border border-gray-200 rounded-md hover:border-green-500 transition-colors duration-300">
                                <input type="radio" id="subBankTransfer" name="subPayment" class="h-4 w-4 text-green-600 focus:ring-green-500">
                                <label for="subBankTransfer" class="ml-3 flex items-center">
                                    <i class="fas fa-university mr-2 text-blue-500"></i>
                                    <span>Virement bancaire</span>
                                </label>
                            </div>
                        </div>
                    </div>
                    
                    <button id="confirmSubscription" class="w-full bg-green-600 hover:bg-green-700 text-white py-3 rounded-md shadow-md transition-colors duration-300">
                        <i class="fas fa-check mr-2"></i> Confirmer l'abonnement
                    </button>
                    
                    <p class="text-xs text-gray-500 mt-3 text-center">
                        En vous abonnant, vous acceptez nos <a href="#" class="text-green-600 hover:underline">Conditions d'utilisation</a>
                    </p>
                </div>
            </div>
        </div>
    </main>

    <!-- Contact Section -->
    <footer id="contact" class="bg-gray-800 text-white py-12">
        <div class="container mx-auto px-4">
            <div class="grid grid-cols-1 md:grid-cols-4 gap-8">
                <div>
                    <h3 class="text-xl font-bold mb-4 flex items-center">
                        <div class="logo-3d text-2xl font-bold text-orange-500 mr-2">
                            <i class="fas fa-shopping-bag"></i>
                        </div>
                        E-Shop
                    </h3>
                    <p class="text-gray-300">
                        Votre marketplace en ligne pour acheter et vendre en toute simplicité.
                    </p>
                    <div class="mt-4">
                        <img src="https://via.placeholder.com/150x50?text=App+Store+Google+Play" alt="Télécharger l'application" class="h-10">
                    </div>
                </div>
                
                <div>
                    <h3 class="text-xl font-bold mb-4">Liens utiles</h3>
                    <ul class="space-y-2">
                        <li><a href="#" class="text-gray-300 hover:text-orange-400 transition-colors duration-300">Accueil</a></li>
                        <li><a href="#customer" class="text-gray-300 hover:text-orange-400 transition-colors duration-300">Espace Client</a></li>
                        <li><a href="#seller" class="text-gray-300 hover:text-orange-400 transition-colors duration-300">Espace Vendeur</a></li>
                        <li><a href="#" class="text-gray-300 hover:text-orange-400 transition-colors duration-300">À propos</a></li>
                        <li><a href="#" class="text-gray-300 hover:text-orange-400 transition-colors duration-300">FAQ</a></li>
                    </ul>
                </div>
                
                <div>
                    <h3 class="text-xl font-bold mb-4">Contact</h3>
                    <ul class="space-y-3">
                        <li class="flex items-start">
                            <i class="fas fa-phone mt-1 mr-2 text-orange-500"></i>
                            <div>
                                <a href="tel:+2370719096914" class="hover:text-orange-400 transition-colors duration-300">071 90 96 914</a>
                                <p class="text-xs text-gray-400">Lun-Ven, 8h-18h</p>
                            </div>
                        </li>
                        <li class="flex items-start">
                            <i class="fas fa-envelope mt-1 mr-2 text-orange-500"></i>
                            <div>
                                <a href="mailto:contact@eshop.cm" class="hover:text-orange-400 transition-colors duration-300">contact@eshop.cm</a>
                                <p class="text-xs text-gray-400">Réponse sous 24h</p>
                            </div>
                        </li>
                        <li class="flex items-start">
                            <i class="fas fa-map-marker-alt mt-1 mr-2 text-orange-500"></i>
                            <div>
                                <span>Bonanjo, Douala</span>
                                <p class="text-xs text-gray-400">Cameroun</p>
                            </div>
                        </li>
                    </ul>
                </div>
                
                <div>
                    <h3 class="text-xl font-bold mb-4">Newsletter</h3>
                    <p class="text-gray-300 mb-3">
                        Abonnez-vous pour recevoir nos offres spéciales et actualités.
                    </p>
                    <div class="flex">
                        <input type="email" placeholder="Votre email" class="px-3 py-2 rounded-l-md focus:outline-none focus:ring-2 focus:ring-orange-500 text-gray-800 w-full">
                        <button class="bg-orange-500 hover:bg-orange-600 text-white px-4 py-2 rounded-r-md transition-colors duration-300">
                            <i class="fas fa-paper-plane"></i>
                        </button>
                    </div>
                    
                    <h4 class="text-lg font-medium mt-4 mb-2">Suivez-nous</h4>
                    <div class="flex space-x-3">
                        <a href="#" class="bg-gray-700 hover:bg-gray-600 w-10 h-10 rounded-full flex items-center justify-center transition-colors duration-300">
                            <i class="fab fa-facebook-f"></i>
                        </a>
                        <a href="#" class="bg-gray-700 hover:bg-gray-600 w-10 h-10 rounded-full flex items-center justify-center transition-colors duration-300">
                            <i class="fab fa-twitter"></i>
                        </a>
                        <a href="#" class="bg-gray-700 hover:bg-gray-600 w-10 h-10 rounded-full flex items-center justify-center transition-colors duration-300">
                            <i class="fab fa-instagram"></i>
                        </a>
                        <a href="#" class="bg-gray-700 hover:bg-gray-600 w-10 h-10 rounded-full flex items-center justify-center transition-colors duration-300">
                            <i class="fab fa-whatsapp"></i>
                        </a>
                    </div>
                </div>
            </div>
            
            <div class="border-t border-gray-700 mt-8 pt-8">
                <div class="flex flex-col md:flex-row justify-between items-center">
                    <p class="text-gray-400 text-sm">
                        &copy; 2023 E-Shop. Tous droits réservés.
                    </p>
                    <div class="flex space-x-4 mt-4 md:mt-0">
                        <a href="#" class="text-gray-400 hover:text-orange-400 text-sm transition-colors duration-300">Confidentialité</a>
                        <a href="#" class="text-gray-400 hover:text-orange-400 text-sm transition-colors duration-300">Conditions</a>
                        <a href="#" class="text-gray-400 hover:text-orange-400 text-sm transition-colors duration-300">Cookies</a>
                    </div>
                </div>
            </div>
        </div>
    </footer>

    <script>
        // Sample product data
        const sampleProducts = [
            {
                id: 1,
                name: "Smartphone X Pro",
                price: 120000,
                category: "Électronique",
                description: "Smartphone haut de gamme avec écran AMOLED 6.7 pouces, 128GB de stockage et triple caméra. Processeur rapide, batterie longue durée et design élégant.",
                stock: 15,
                images: [
                    "https://images.unsplash.com/photo-1601784551446-20c9e07cdbdb?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8Mnx8c21hcnRwaG9uZXxlbnwwfHwwfHx8MA%3D%3D&auto=format&fit=crop&w=500&q=60",
                    "https://images.unsplash.com/photo-1592899677977-9c10ca588bbd?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8NXx8c21hcnRwaG9uZXxlbnwwfHwwfHx8MA%3D%3D&auto=format&fit=crop&w=500&q=60",
                    "https://images.unsplash.com/photo-1580913428735-bd3c269d6a82?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTB8fHNtYXJ0cGhvbmV8ZW58MHx8MHx8fDA%3D&auto=format&fit=crop&w=500&q=60"
                ]
            },
            {
                id: 2,
                name: "Sac à dos élégant",
                price: 25000,
                category: "Mode",
                description: "Sac à dos en cuir synthétique résistant à l'eau avec compartiment pour ordinateur portable 15 pouces. Plusieurs poches organisatrices et sangles réglables pour un confort optimal.",
                stock: 8,
                images: [
                    "https://images.unsplash.com/photo-1553062407-98eeb64c6a62?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8Mnx8YmFja3BhY2t8ZW58MHx8MHx8fDA%3D&auto=format&fit=crop&w=500&q=60",
                    "https://images.unsplash.com/photo-1576566588028-4147f3842f27?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8M3x8YmFja3BhY2t8ZW58MHx8MHx8fDA%3D&auto=format&fit=crop&w=500&q=60"
                ]
            },
            {
                id: 3,
                name: "Mixeur professionnel",
                price: 35000,
                category: "Maison",
                description: "Mixeur puissant 1000W avec 5 vitesses et fonction pulse pour toutes vos préparations culinaires. Lames en acier inoxydable et bol en verre résistant. Facile à nettoyer.",
                stock: 5,
                images: [
                    "https://images.unsplash.com/photo-1574323347407-f5e1c5d0a370?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8Mnx8YmxlbmRlcnxlbnwwfHwwfHx8MA%3D%3D&auto=format&fit=crop&w=500&q=60",
                    "https://images.unsplash.com/photo-1585238342024-78d90f7fca38?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8NXx8YmxlbmRlcnxlbnwwfHwwfHx8MA%3D%3D&auto=format&fit=crop&w=500&q=60"
                ]
            },
            {
                id: 4,
                name: "Crème hydratante",
                price: 8000,
                category: "Beauté",
                description: "Crème hydratante quotidienne pour tous types de peau. 50ml. Sans parabènes, avec extraits naturels d'aloe vera et de vitamine E pour une peau douce et hydratée.",
                stock: 20,
                images: [
                    "https://images.unsplash.com/photo-1522337360788-8b13dee7a37e?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8NHx8bW9pc3R1cml6ZXJ8ZW58MHx8MHx8fDA%3D&auto=format&fit=crop&w=500&q=60",
                    "https://images.unsplash.com/photo-1596755094514-f87e34085b2c?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8Nnx8bW9pc3R1cml6ZXJ8ZW58MHx8MHx8fDA%3D&auto=format&fit=crop&w=500&q=60"
                ]
            },
            {
                id: 5,
                name: "Écouteurs sans fil",
                price: 45000,
                category: "Électronique",
                description: "Écouteurs Bluetooth avec réduction de bruit active. Jusqu'à 20 heures d'autonomie, qualité sonore HD et design ergonomique pour un confort prolongé.",
                stock: 12,
                images: [
                    "https://images.unsplash.com/photo-1590658268037-6bf12165a8df?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8Mnx8aGVhZHBob25lc3xlbnwwfHwwfHx8MA%3D%3D&auto=format&fit=crop&w=500&q=60",
                    "https://images.unsplash.com/photo-1593784991095-a205069470b6?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8NXx8aGVhZHBob25lc3xlbnwwfHwwfHx8MA%3D%3D&auto=format&fit=crop&w=500&q=60"
                ]
            },
            {
                id: 6,
                name: "Montre connectée",
                price: 60000,
                category: "Électronique",
                description: "Montre intelligente avec écran tactile, suivi d'activité, moniteur de fréquence cardiaque et notifications smartphone. Résistante à l'eau jusqu'à 50m.",
                stock: 7,
                images: [
                    "https://images.unsplash.com/photo-1523275335684-37898b6baf30?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8Mnx8d2F0Y2hlc3xlbnwwfHwwfHx8MA%3D%3D&auto=format&fit=crop&w=500&q=60",
                    "https://images.unsplash.com/photo-1546868871-7041f2a55e12?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8M3x8d2F0Y2hlc3xlbnwwfHwwfHx8MA%3D%3D&auto=format&fit=crop&w=500&q=60"
                ]
            },
            {
                id: 7,
                name: "T-shirt premium",
                price: 12000,
                category: "Mode",
                description: "T-shirt en coton bio de haute qualité. Coupe moderne, col rond et disponible en plusieurs coloris. Lavage en machine à 30°C.",
                stock: 25,
                images: [
                    "https://images.unsplash.com/photo-1521572163474-6864f9cf17ab?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8Mnx8dHNoaXJ0fGVufDB8fDB8fHww&auto=format&fit=crop&w=500&q=60",
                    "https://images.unsplash.com/photo-1527719327859-c6ce80353573?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8NXx8dHNoaXJ0fGVufDB8fDB8fHww&auto=format&fit=crop&w=500&q=60"
                ]
            },
            {
                id: 8,
                name: "Lampe de bureau LED",
                price: 18000,
                category: "Maison",
                description: "Lampe de bureau réglable avec technologie LED, 3 niveaux de luminosité et température de couleur ajustable. USB intégré pour charger vos appareils.",
                stock: 10,
                images: [
                    "https://images.unsplash.com/photo-1513506003901-1e6a229e2d15?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8Mnx8bGFtcHxlbnwwfHwwfHx8MA%3D%3D&auto=format&fit=crop&w=500&q=60",
                    "https://images.unsplash.com/photo-1526170375885-4d8ecf77b99f?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8NXx8bGFtcHxlbnwwfHwwfHx8MA%3D%3D&auto=format&fit=crop&w=500&q=60"
                ]
            }
        ];

        // Cart state
        let cart = [];
        
        // Seller's products
        let sellerProducts = [];
        
        // DOM elements
        const productGrid = document.getElementById('productGrid');
        const cartItems = document.getElementById('cartItems');
        const cartCount = document.getElementById('cartCount');
        const cartSubtotal = document.getElementById('cartSubtotal');
        const cartTotal = document.getElementById('cartTotal');
        const openCart = document.getElementById('openCart');
        const closeCart = document.getElementById('closeCart');
        const cartSidebar = document.getElementById('cartSidebar');
        const productModal = document.getElementById('productModal');
        const closeModal = document.getElementById('closeModal');
        const modalProductName = document.getElementById('modalProductName');
        const modalProductImage = document.getElementById('modalProductImage');
        const modalProductDescription = document.getElementById('modalProductDescription');
        const modalProductPrice = document.getElementById('modalProductPrice');
        const modalProductStock = document.getElementById('modalProductStock');
        const addToCartFromModal = document.getElementById('addToCartFromModal');
        const productQty = document.getElementById('productQty');
        const increaseQty = document.getElementById('increaseQty');
        const decreaseQty = document.getElementById('decreaseQty');
        const checkoutBtn = document.getElementById('checkoutBtn');
        const checkoutModal = document.getElementById('checkoutModal');
        const closeCheckoutModal = document.getElementById('closeCheckoutModal');
        const confirmOrder = document.getElementById('confirmOrder');
        const checkoutSubtotal = document.getElementById('checkoutSubtotal');
        const checkoutTotal = document.getElementById('checkoutTotal');
        const productForm = document.getElementById('productForm');
        const sellerProductsTable = document.getElementById('sellerProducts');
        const subscribeBtn = document.getElementById('subscribeBtn');
        const subscriptionModal = document.getElementById('subscriptionModal');
        const closeSubscriptionModal = document.getElementById('closeSubscriptionModal');
        const confirmSubscription = document.getElementById('confirmSubscription');
        const continueShopping = document.getElementById('continueShopping');
        const notificationBell = document.getElementById('notificationBell');
        const notificationDropdown = document.getElementById('notificationDropdown');
        const cartSummary = document.getElementById('cartSummary');

        // Current product in modal
        let currentProduct = null;
        let currentQty = 1;
        
        // Initialize the app
        function init() {
            renderProducts(sampleProducts);
            setupEventListeners();
        }
        
        // Set up event listeners
        function setupEventListeners() {
            // Cart interactions
            openCart.addEventListener('click', () => cartSidebar.classList.remove('translate-x-full'));
            closeCart.addEventListener('click', () => cartSidebar.classList.add('translate-x-full'));
            
            // Continue shopping button
            continueShopping.addEventListener('click', () => {
                cartSidebar.classList.add('translate-x-full');
                document.querySelector('#customer').scrollIntoView({ behavior: 'smooth' });
            });
            
            // Notification bell
            notificationBell.addEventListener('click', () => {
                notificationDropdown.classList.toggle('hidden');
            });
            
            // Close dropdown when clicking outside
            document.addEventListener('click', (e) => {
                if (!notificationBell.contains(e.target) && !notificationDropdown.contains(e.target)) {
                    notificationDropdown.classList.add('hidden');
                }
            });
            
            // Product modal interactions
            closeModal.addEventListener('click', () => productModal.classList.add('hidden'));
            
            // Quantity controls
            increaseQty.addEventListener('click', () => {
                if (currentProduct && currentQty < currentProduct.stock) {
                    currentQty++;
                    productQty.textContent = currentQty;
                }
            });
            
            decreaseQty.addEventListener('click', () => {
                if (currentQty > 1) {
                    currentQty--;
                    productQty.textContent = currentQty;
                }
            });
            
            // Checkout modal
            checkoutBtn.addEventListener('click', () => {
                if (cart.length > 0) {
                    checkoutSubtotal.textContent = `${calculateSubtotal().toLocaleString()} FCFA`;
                    checkoutTotal.textContent = `${(calculateSubtotal() + 2000).toLocaleString()} FCFA`;
                    checkoutModal.classList.remove('hidden');
                }
            });
            
            closeCheckoutModal.addEventListener('click', () => checkoutModal.classList.add('hidden'));
            
            confirmOrder.addEventListener('click', () => {
                alert('Commande passée avec succès! Nous vous contacterons pour la livraison.');
                cart = [];
                updateCart();
                checkoutModal.classList.add('hidden');
                cartSidebar.classList.add('translate-x-full');
            });
            
            // Seller form
            productForm.addEventListener('submit', (e) => {
                e.preventDefault();
                addSellerProduct();
            });
            
            // Subscription
            subscribeBtn.addEventListener('click', () => subscriptionModal.classList.remove('hidden'));
            closeSubscriptionModal.addEventListener('click', () => subscriptionModal.classList.add('hidden'));
            
            confirmSubscription.addEventListener('click', () => {
                alert('Abonnement confirmé! Vous pouvez continuer à vendre sur E-Shop.');
                document.getElementById('subscriptionStatus').textContent = 'Vous êtes abonné (renouvellement automatique)';
                document.getElementById('subscriptionStatus').classList.remove('text-green-600');
                document.getElementById('subscriptionStatus').classList.add('text-blue-600');
                subscriptionModal.classList.add('hidden');
            });
        }
        
        // Render products to the grid
        function renderProducts(products) {
            productGrid.innerHTML = '';
            
            if (products.length === 0) {
                productGrid.innerHTML = `
                    <div class="col-span-full text-center py-12 text-gray-500">
                        <i class="fas fa-box-open text-4xl mb-4 opacity-30"></i>
                        <p class="text-lg">Aucun produit disponible</p>
                    </div>
                `;
                return;
            }
            
            products.forEach(product => {
                const productCard = document.createElement('div');
                productCard.className = 'bg-white rounded-xl overflow-hidden shadow-md product-card transition-all duration-300 hover:shadow-lg';
                productCard.innerHTML = `
                    <div class="relative">
                        <img src="${product.images[0]}" alt="${product.name}" class="w-full h-48 object-cover">
                        <div class="absolute top-2 right-2 bg-orange-500 text-white text-xs font-bold px-2 py-1 rounded">
                            <i class="fas fa-tag mr-1"></i> PROMO
                        </div>
                    </div>
                    <div class="p-4">
                        <h3 class="font-bold text-lg mb-1 truncate">${product.name}</h3>
                        <p class="text-gray-600 text-sm mb-2
</body>
</html>
