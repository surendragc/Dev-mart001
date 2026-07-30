<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>DEV MART</title>

<style>
body { margin:0; font-family: Arial; background: #f1f3f6; }
G
/* Header */

.header {
    display: flex;
    align-items: center;
    background: #2874f0;
    padding: 10px;
    color: white;
}
.logo { font-size: 22px; font-weight: bold; margin-right: 20px; }
.search-box { flex: 1; }
.search-box input { width: 100%; padding: 8px; border: none; }
button { margin-left: 10px; padding: 8px; border: none; cursor: pointer; }

/* Products */
.products { padding: 20px; display:flex; flex-wrap:wrap; justify-content:center; }
.product {
    background:white; width:180px; margin:10px; padding:10px; text-align:center; border-radius:5px;
    transition:0.3s;
}
.product img { width:100%; height:120px; object-fit:cover; }
.product:hover { transform: scale(1.2); z-index:2; }

/* Cart */
#cart-count { background:red; color:white; padding:3px 7px; border-radius:50%; }

/* Login */
.login-box {
    display:none; position:fixed; top:30%; left:40%; background:white; padding:20px; box-shadow:0 0 10px gray;
}
.login-box input { display:block; margin:10px 0; padding:8px; width:100%; }

/* Checkout */
.checkout { display:none; padding:20px; }
.checkout input, .checkout select { width:100%; padding:10px; margin:10px 0; }
/* WhatsApp Support Button */
.whatsapp-btn{
    position: fixed;
    bottom: 20px;
    right: 20px;
    width: 60px;
    height: 60px;
    background: #25D366;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    box-shadow: 0 4px 10px rgba(0,0,0,0.3);
    z-index: 9999;
    text-decoration: none;
}

.whatsapp-btn:hover{
    transform: scale(1.1);
}</style>
</head>
<body>
<!-- WhatsApp Support -->
<a href="https://wa.me/918107130027?text=Hi%20DEV%20MART,%20I%20need%20support."
   target="_blank"
   class="whatsapp-btn"
   title="Chat with Support">
    <img src="https://upload.wikimedia.org/wikipedia/commons/6/6b/WhatsApp.svg"
         alt="WhatsApp Support"
         width="40"
         height="40">
</a><div class="header">
    <div class="logo">DEV MART</div>
    <div class="search-box">
        <input type="text" id="searchInput" onkeyup="searchItems()" placeholder="Search for products...">
        
    </div>
    <button onclick="openLogin()">Login</button>
    <button>Cart <span id="cart-count">0</span></button>
</div>

<!-- Product Page -->
<div id="productPage" class="products"></div>

<!-- Login -->
<div class="login-box" id="loginBox">
    <h3>Login</h3>
    <input type="text" placeholder="Username">
    <input type="password" placeholder="Password">
    <button onclick="login()">Submit</button>
</div>

<!-- Checkout -->
<div class="checkout" id="checkoutPage">
    <h2>Checkout</h2>
    <p id="itemDetails"></p>
    <label>Full Address:</label>
    <input type="text" placeholder="Enter your address">
    <label>Phone Number:</label>
    <input type="number" placeholder="Enter phone number">
    <label>Payment Method:</label>
    <select>
        <option>Cash on Delivery</option>
        <option>UPI</option>
        <option>Credit Card</option>
    </select>
    <button onclick="placeOrder()">Place Order</button>
    <button onclick="goBack()">Back</button>
</div>

<script>
    
// Cart and Login
let cart = 0;
let selectedItem = "";

// Product Names
let itemNames = ["Phone","Laptop","Shoes","Watch","Headphones","T-shirt","Jeans","Bag","Camera","Tablet"];

// Generate 1000 products dynamically
let container = document.getElementById("productPage");
for(let i=1; i<=1000; i++){
    let name = itemNames[i % itemNames.length] + " " + i;
    let price = Math.floor(Math.random()*5000) + 500;
    let div = document.createElement("div");
    div.className = "product";
    div.innerHTML = `
        <img src="https://picsum.photos/200?random=${i}">
        <h3>${name}</h3>
        <p>₹${price}</p>
        <button onclick="addToCart()">Add to Cart</button>
        <button onclick="buyNow('${name}', ${price})">Buy Now</button>
    `;
    container.appendChild(div);
}

// Cart
function addToCart(){
    cart++;
    document.getElementById("cart-count").innerText = cart;
}

// Buy Now
function buyNow(name, price){
    selectedItem = name + " - ₹" + price;
    document.getElementById("productPage").style.display="none";
    document.getElementById("checkoutPage").style.display="block";
    document.getElementById("itemDetails").innerText = "Buying: " + selectedItem;
}

// Checkout
function placeOrder(){
    alert("Order Placed Successfully!");
}

// Back to product page
function goBack(){
    document.getElementById("productPage").style.display="flex";
    document.getElementById("checkoutPage").style.display="none";
}

// Login
function openLogin(){
    document.getElementById("loginBox").style.display="block";
}
function login(){
    alert("Login Successful!");
    document.getElementById("loginBox").style.display="none";
}

// Search
function searchItems(){
    let input = document.getElementById("searchInput").value.toLowerCase();
    let products = document.getElementsByClassName("product");
    for(let i=0;i<products.length;i++){
        let text = products[i].innerText.toLowerCase();
        products[i].style.display = text.includes(input) ? "inline-block" : "none";
    }
}
</script>

</body>
</html>
