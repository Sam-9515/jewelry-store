import React, { useState } from "react"; import Link from "next/link";

const products = [ { id: 1, name: "Gold Ring", price: 299, image: "/ring.jpg" }, { id: 2, name: "Silver Necklace", price: 199, image: "/necklace.jpg" }, { id: 3, name: "Diamond Earrings", price: 499, image: "/earrings.jpg" }, ];

export default function Home() { const [cart, setCart] = useState([]);

const addToCart = (product) => { setCart([...cart, product]); };

const removeFromCart = (index) => { setCart(cart.filter((_, i) => i !== index)); };

return ( <div className="min-h-screen bg-gradient-to-br from-gray-100 to-gray-300 flex flex-col items-center"> <header className="w-full bg-white shadow-md py-4 px-6 flex justify-between items-center sticky top-0 z-10"> <h1 className="text-2xl font-bold text-gray-800">Jewelry Store</h1> <nav className="space-x-6"> <Link href="/shop" className="text-gray-700 hover:text-black transition">Shop</Link> <Link href="/cart" className="text-gray-700 hover:text-black transition">Cart ({cart.length})</Link> </nav> </header>

<main className="flex flex-col items-center py-16 text-center">
    <h2 className="text-4xl font-bold text-gray-800 mb-4">Exclusive Jewelry Collection</h2>
    <p className="text-gray-600 max-w-md">Discover the finest selection of handcrafted jewelry, perfect for every occasion.</p>
    <Link href="/shop" className="mt-6 px-8 py-3 bg-black text-white rounded-lg text-lg shadow-md hover:bg-gray-800 transition">Shop Now</Link>
    
    <div className="grid grid-cols-1 md:grid-cols-3 gap-10 mt-12">
      {products.map((product) => (
        <div key={product.id} className="bg-white p-6 shadow-lg rounded-xl text-center transform hover:scale-105 transition">
          <img src={product.image} alt={product.name} className="w-full h-48 object-cover mb-4 rounded-md" />
          <h3 className="text-xl font-semibold text-gray-800">{product.name}</h3>
          <p className="text-gray-600 text-lg">${product.price}</p>
          <button onClick={() => addToCart(product)} className="mt-4 px-6 py-2 bg-black text-white rounded-lg shadow-md hover:bg-gray-800 transition">Add to Cart</button>
        </div>
      ))}
    </div>
  </main>
  
  {/* Cart Section */}
  <section className="w-full max-w-2xl bg-white p-8 mt-12 shadow-lg rounded-lg">
    <h2 className="text-2xl font-bold text-gray-800 mb-4">Shopping Cart</h2>
    {cart.length === 0 ? (
      <p className="text-gray-600">Your cart is empty.</p>
    ) : (
      <ul className="space-y-4">
        {cart.map((item, index) => (
          <li key={index} className="flex justify-between items-center p-4 border-b">
            <span className="text-lg text-gray-800">{item.name} - ${item.price}</span>
            <button onClick={() => removeFromCart(index)} className="text-red-500 hover:text-red-700 transition">Remove</button>
          </li>
        ))}
      </ul>
    )}
    {cart.length > 0 && (
      <button className="mt-6 px-8 py-3 bg-green-500 text-white text-lg rounded-lg shadow-md hover:bg-green-700 transition">Proceed to Checkout</button>
    )}
  </section>
</div>

); }

