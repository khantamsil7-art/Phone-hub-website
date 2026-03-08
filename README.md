<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>PHONE HUB - be upgraded</title>

<style>

body{
margin:0;
font-family:Arial, Helvetica, sans-serif;
background:#f5f5f5;
}

/* HEADER */

header{
background:#000;
color:white;
padding:15px;
text-align:center;
}

header h1{
margin:0;
font-size:28px;
}

header p{
margin:3px;
color:#ccc;
}

/* HERO */

.hero{
background:url("https://i.ibb.co/ZprRNHGZ/shop-with-we-are-open-sign-23-2148557016.jpg") center/cover;
height:85vh;
display:flex;
align-items:center;
justify-content:center;
text-align:center;
color:white;
}

.hero h2{
font-size:40px;
background:rgba(0,0,0,0.5);
padding:20px;
border-radius:10px;
}

.shop-btn{
display:inline-block;
margin-top:15px;
padding:12px 25px;
background:#ff6600;
color:white;
border-radius:5px;
text-decoration:none;
}

/* PRODUCTS */

.products{
padding:30px;
}

.carousel{
display:flex;
overflow-x:auto;
gap:20px;
}

.card{
background:white;
border-radius:10px;
min-width:220px;
padding:15px;
box-shadow:0 3px 10px rgba(0,0,0,0.1);
text-align:center;
}

.card img{
width:100%;
border-radius:8px;
}

.card button{
background:#28a745;
border:none;
color:white;
padding:10px;
margin-top:8px;
border-radius:5px;
cursor:pointer;
}

/* CART ICON */

.cart-icon{
position:fixed;
right:20px;
bottom:90px;
background:#000;
color:white;
padding:15px;
border-radius:50%;
font-size:20px;
cursor:pointer;
}

.cart-count{
background:red;
padding:3px 7px;
border-radius:50%;
font-size:12px;
position:absolute;
top:-5px;
right:-5px;
}

/* CART DRAWER */

.cart{
position:fixed;
right:-350px;
top:0;
width:300px;
height:100%;
background:white;
box-shadow:-3px 0 10px rgba(0,0,0,0.2);
padding:20px;
transition:0.3s;
overflow:auto;
}

.cart.active{
right:0;
}

.cart h3{
margin-top:0;
}

.cart-item{
font-size:14px;
margin:5px 0;
}

input{
width:100%;
padding:8px;
margin:5px 0;
}

.send-btn{
background:#ff6600;
color:white;
border:none;
padding:10px;
width:100%;
margin-top:10px;
}

/* WHATSAPP */

.whatsapp{
position:fixed;
bottom:20px;
right:20px;
background:#25D366;
color:white;
padding:15px;
border-radius:50%;
font-size:22px;
text-decoration:none;
}

</style>
</head>

<body>

<header>
<h1>PHONE HUB</h1>
<p>be upgraded</p>
</header>

<section class="hero">
<div>
<h2>Upgrade Your Phone Today</h2>
<a href="#products" class="shop-btn">Shop Now</a>
</div>
</section>

<section class="products" id="products">
<h2>Our Products</h2>

<div class="carousel">

<div class="card">
<img src="https://i.ibb.co/DfKX5RxS/20260131-224619.jpg">
<h4>Mobile Phone</h4>
<p>₹12,999</p>
<button onclick="addToCart('Mobile Phone',12999)">Add to Cart</button>
</div>

<div class="card">
<img src="https://i.ibb.co/DfKX5RxS/20260131-224619.jpg">
<h4>Smartphone</h4>
<p>₹14,999</p>
<button onclick="addToCart('Smartphone',14999)">Add to Cart</button>
</div>

<div class="card">
<img src="https://i.ibb.co/DfKX5RxS/20260131-224619.jpg">
<h4>Mobile Accessories</h4>
<p>₹499</p>
<button onclick="addToCart('Accessories',499)">Add to Cart</button>
</div>

</div>
</section>

<!-- CART ICON -->

<div class="cart-icon" onclick="toggleCart()">
🛒
<span class="cart-count" id="count">0</span>
</div>

<!-- CART DRAWER -->

<div class="cart" id="cart">

<h3>Your Cart</h3>

<div id="cart-items"></div>

<h4>Customer Details</h4>

<input id="name" placeholder="Your Name">
<input id="phone" placeholder="Phone Number">

<button class="send-btn" onclick="sendOrder()">Send Order</button>

</div>

<!-- WHATSAPP -->

<a class="whatsapp" href="https://wa.me//9504476868
">💬</a>

<script src="https://cdn.jsdelivr.net/npm/emailjs-com@3/dist/email.min.js"></script>

<script>

emailjs.init("YOUR_PUBLIC_KEY");

let cart=[];

function addToCart(name,price){

cart.push({name,price});

document.getElementById("count").innerText=cart.length;

renderCart();

}

function renderCart(){

let list=document.getElementById("cart-items");

list.innerHTML="";

cart.forEach(item=>{
let div=document.createElement("div");
div.className="cart-item";
div.innerText=item.name+" - ₹"+item.price;
list.appendChild(div);
});

}

function toggleCart(){

document.getElementById("cart").classList.toggle("active");

}

function sendOrder(){

let name=document.getElementById("name").value;
let phone=document.getElementById("phone").value;

let items=cart.map(i=>i.name+" ₹"+i.price).join(", ");

let params={
customer_name:name,
phone:phone,
order_items:items
};

emailjs.send("YOUR_SERVICE_ID","YOUR_TEMPLATE_ID",params)
.then(()=>{
alert("Order sent successfully!");
cart=[];
renderCart();
document.getElementById("count").innerText=0;
});

}

</script>

</body>
</html>
