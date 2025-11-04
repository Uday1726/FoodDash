import React, { useState } from 'react';
import { ShoppingCart, Search, MapPin, Clock, Star, Plus, Minus, X, CreditCard, User, Phone, Home } from 'lucide-react';

const FoodDeliveryApp = () => {
  const [cart, setCart] = useState([]);
  const [view, setView] = useState('restaurants');
  const [selectedRestaurant, setSelectedRestaurant] = useState(null);
  const [showCart, setShowCart] = useState(false);
  const [searchQuery, setSearchQuery] = useState('');

  const restaurants = [
    {
      id: 1,
      name: "Bella Italia",
      cuisine: "Italian",
      rating: 4.5,
      deliveryTime: "25-35 min",
      deliveryFee: 2.99,
      image: "🍝",
      menu: [
        { id: 101, name: "Margherita Pizza", price: 399, description: "Classic tomato and mozzarella", category: "Pizza" },
        { id: 102, name: "Carbonara Pasta", price: 449, description: "Creamy pasta with bacon", category: "Pasta" },
        { id: 103, name: "Tiramisu", price: 199, description: "Italian coffee dessert", category: "Desserts" },
        { id: 104, name: "Caesar Salad", price: 249, description: "Fresh romaine with parmesan", category: "Salads" }
      ]
    },
    {
      id: 2,
      name: "Sushi Master",
      cuisine: "Japanese",
      rating: 4.7,
      deliveryTime: "30-40 min",
      deliveryFee: 3.49,
      image: "🍱",
      menu: [
        { id: 201, name: "California Roll", price: 10.99, description: "Crab, avocado, cucumber", category: "Rolls" },
        { id: 202, name: "Salmon Nigiri", price: 13.99, description: "Fresh salmon on rice", category: "Nigiri" },
        { id: 203, name: "Miso Soup", price: 4.99, description: "Traditional soybean soup", category: "Soups" },
        { id: 204, name: "Edamame", price: 5.99, description: "Steamed soybeans", category: "Appetizers" }
      ]
    },
    {
      id: 3,
      name: "Burger Bros",
      cuisine: "American",
      rating: 4.3,
      deliveryTime: "20-30 min",
      deliveryFee: 1.99,
      image: "🍔",
      menu: [
        { id: 301, name: "Classic Burger", price: 9.99, description: "Beef patty with all toppings", category: "Burgers" },
        { id: 302, name: "Cheese Fries", price: 5.99, description: "Crispy fries with melted cheese", category: "Sides" },
        { id: 303, name: "Milkshake", price: 4.99, description: "Vanilla, chocolate, or strawberry", category: "Drinks" },
        { id: 304, name: "Chicken Wings", price: 11.99, description: "BBQ or buffalo style", category: "Appetizers" }
      ]
    },
    {
      id: 4,
      name: "Thai Spice",
      cuisine: "Thai",
      rating: 4.6,
      deliveryTime: "35-45 min",
      deliveryFee: 2.49,
      image: "🍜",
      menu: [
        { id: 401, name: "Pad Thai", price: 12.99, description: "Stir-fried rice noodles", category: "Noodles" },
        { id: 402, name: "Green Curry", price: 13.99, description: "Spicy coconut curry", category: "Curries" },
        { id: 403, name: "Spring Rolls", price: 6.99, description: "Vegetable spring rolls", category: "Appetizers" },
        { id: 404, name: "Mango Sticky Rice", price: 7.99, description: "Sweet coconut dessert", category: "Desserts" }
      ]
    }
  ];

  const addToCart = (restaurant, item) => {
    const existingItem = cart.find(i => i.id === item.id && i.restaurantId === restaurant.id);
    if (existingItem) {
      setCart(cart.map(i => 
        i.id === item.id && i.restaurantId === restaurant.id 
          ? { ...i, quantity: i.quantity + 1 }
          : i
      ));
    } else {
      setCart([...cart, { 
        ...item, 
        restaurantId: restaurant.id,
        restaurantName: restaurant.name,
        quantity: 1 
      }]);
    }
  };

  const updateQuantity = (itemId, restaurantId, delta) => {
    setCart(cart.map(item => {
      if (item.id === itemId && item.restaurantId === restaurantId) {
        const newQuantity = item.quantity + delta;
        return newQuantity > 0 ? { ...item, quantity: newQuantity } : null;
      }
      return item;
    }).filter(Boolean));
  };

  const removeFromCart = (itemId, restaurantId) => {
    setCart(cart.filter(item => !(item.id === itemId && item.restaurantId === restaurantId)));
  };

  const getCartTotal = () => {
    const subtotal = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
    const deliveryFee = cart.length > 0 ? (selectedRestaurant?.deliveryFee || 2.99) : 0;
    return { subtotal, deliveryFee, total: subtotal + deliveryFee };
  };

  const filteredRestaurants = restaurants.filter(r => 
    r.name.toLowerCase().includes(searchQuery.toLowerCase()) ||
    r.cuisine.toLowerCase().includes(searchQuery.toLowerCase())
  );

  return (
    <div className="min-h-screen bg-gray-50">
      {/* Header */}
      <header className="bg-white shadow-sm sticky top-0 z-40">
        <div className="max-w-7xl mx-auto px-4 py-4">
          <div className="flex items-center justify-between mb-4">
            <div className="flex items-center gap-3">
              <div className="text-3xl">🍽️</div>
              <h1 className="text-2xl font-bold text-orange-600">FoodDash</h1>
            </div>
            <button
              onClick={() => setShowCart(!showCart)}
              className="relative bg-orange-600 text-white px-4 py-2 rounded-lg flex items-center gap-2 hover:bg-orange-700 transition"
            >
              <ShoppingCart size={20} />
              <span className="font-semibold">{cart.length}</span>
            </button>
          </div>
          
          {view === 'restaurants' && (
            <div className="relative">
              <Search className="absolute left-3 top-1/2 -translate-y-1/2 text-gray-400" size={20} />
              <input
                type="text"
                placeholder="Search restaurants or cuisines..."
                value={searchQuery}
                onChange={(e) => setSearchQuery(e.target.value)}
                className="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-orange-500"
              />
            </div>
          )}
        </div>
      </header>

      <div className="max-w-7xl mx-auto px-4 py-6">
        {/* Restaurants View */}
        {view === 'restaurants' && (
          <div>
            <div className="mb-6">
              <h2 className="text-2xl font-bold mb-2">Popular Restaurants</h2>
              <p className="text-gray-600">Choose from {filteredRestaurants.length} restaurants near you</p>
            </div>

            <div className="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
              {filteredRestaurants.map(restaurant => (
                <div
                  key={restaurant.id}
                  onClick={() => {
                    setSelectedRestaurant(restaurant);
                    setView('menu');
                  }}
                  className="bg-white rounded-xl shadow-sm hover:shadow-md transition cursor-pointer overflow-hidden"
                >
                  <div className="h-40 bg-gradient-to-br from-orange-100 to-orange-200 flex items-center justify-center text-7xl">
                    {restaurant.image}
                  </div>
                  <div className="p-4">
                    <h3 className="text-xl font-bold mb-1">{restaurant.name}</h3>
                    <p className="text-gray-600 text-sm mb-3">{restaurant.cuisine}</p>
                    <div className="flex items-center justify-between text-sm">
                      <div className="flex items-center gap-1 text-yellow-600">
                        <Star size={16} fill="currentColor" />
                        <span className="font-semibold">{restaurant.rating}</span>
                      </div>
                      <div className="flex items-center gap-1 text-gray-600">
                        <Clock size={16} />
                        <span>{restaurant.deliveryTime}</span>
                      </div>
                      <div className="text-gray-600">
                        ${restaurant.deliveryFee} delivery
                      </div>
                    </div>
                  </div>
                </div>
              ))}
            </div>
          </div>
        )}

        {/* Menu View */}
        {view === 'menu' && selectedRestaurant && (
          <div>
            <button
              onClick={() => setView('restaurants')}
              className="mb-4 text-orange-600 hover:text-orange-700 font-semibold"
            >
              ← Back to restaurants
            </button>

            <div className="bg-white rounded-xl shadow-sm p-6 mb-6">
              <div className="flex items-start gap-4">
                <div className="text-6xl">{selectedRestaurant.image}</div>
                <div className="flex-1">
                  <h2 className="text-3xl font-bold mb-2">{selectedRestaurant.name}</h2>
                  <p className="text-gray-600 mb-3">{selectedRestaurant.cuisine} Cuisine</p>
                  <div className="flex items-center gap-4 text-sm">
                    <div className="flex items-center gap-1 text-yellow-600">
                      <Star size={16} fill="currentColor" />
                      <span className="font-semibold">{selectedRestaurant.rating}</span>
                    </div>
                    <div className="flex items-center gap-1 text-gray-600">
                      <Clock size={16} />
                      <span>{selectedRestaurant.deliveryTime}</span>
                    </div>
                    <div className="text-gray-600">
                      ${selectedRestaurant.deliveryFee} delivery fee
                    </div>
                  </div>
                </div>
              </div>
            </div>

            <div className="space-y-4">
              {selectedRestaurant.menu.map(item => (
                <div key={item.id} className="bg-white rounded-lg shadow-sm p-4 flex justify-between items-center">
                  <div className="flex-1">
                    <h3 className="font-bold text-lg mb-1">{item.name}</h3>
                    <p className="text-gray-600 text-sm mb-2">{item.description}</p>
                    <p className="text-orange-600 font-bold">${item.price.toFixed(2)}</p>
                  </div>
                  <button
                    onClick={() => addToCart(selectedRestaurant, item)}
                    className="bg-orange-600 text-white p-2 rounded-lg hover:bg-orange-700 transition"
                  >
                    <Plus size={20} />
                  </button>
                </div>
              ))}
            </div>
          </div>
        )}
      </div>

      {/* Cart Sidebar */}
      {showCart && (
        <div className="fixed inset-0 bg-black bg-opacity-50 z-50 flex justify-end" onClick={() => setShowCart(false)}>
          <div 
            className="bg-white w-full max-w-md h-full overflow-y-auto"
            onClick={(e) => e.stopPropagation()}
          >
            <div className="p-6">
              <div className="flex items-center justify-between mb-6">
                <h2 className="text-2xl font-bold">Your Cart</h2>
                <button onClick={() => setShowCart(false)} className="text-gray-500 hover:text-gray-700">
                  <X size={24} />
                </button>
              </div>

              {cart.length === 0 ? (
                <div className="text-center py-12">
                  <div className="text-6xl mb-4">🛒</div>
                  <p className="text-gray-600">Your cart is empty</p>
                </div>
              ) : (
                <>
                  <div className="space-y-4 mb-6">
                    {cart.map(item => (
                      <div key={`${item.restaurantId}-${item.id}`} className="border-b pb-4">
                        <div className="flex justify-between items-start mb-2">
                          <div className="flex-1">
                            <h3 className="font-semibold">{item.name}</h3>
                            <p className="text-sm text-gray-600">{item.restaurantName}</p>
                          </div>
                          <button
                            onClick={() => removeFromCart(item.id, item.restaurantId)}
                            className="text-red-500 hover:text-red-700"
                          >
                            <X size={18} />
                          </button>
                        </div>
                        <div className="flex items-center justify-between">
                          <div className="flex items-center gap-3">
                            <button
                              onClick={() => updateQuantity(item.id, item.restaurantId, -1)}
                              className="bg-gray-200 p-1 rounded hover:bg-gray-300"
                            >
                              <Minus size={16} />
                            </button>
                            <span className="font-semibold">{item.quantity}</span>
                            <button
                              onClick={() => updateQuantity(item.id, item.restaurantId, 1)}
                              className="bg-gray-200 p-1 rounded hover:bg-gray-300"
                            >
                              <Plus size={16} />
                            </button>
                          </div>
                          <span className="font-bold text-orange-600">
                            ${(item.price * item.quantity).toFixed(2)}
                          </span>
                        </div>
                      </div>
                    ))}
                  </div>

                  <div className="border-t pt-4 space-y-2 mb-6">
                    <div className="flex justify-between">
                      <span className="text-gray-600">Subtotal</span>
                      <span className="font-semibold">${getCartTotal().subtotal.toFixed(2)}</span>
                    </div>
                    <div className="flex justify-between">
                      <span className="text-gray-600">Delivery Fee</span>
                      <span className="font-semibold">${getCartTotal().deliveryFee.toFixed(2)}</span>
                    </div>
                    <div className="flex justify-between text-lg font-bold border-t pt-2">
                      <span>Total</span>
                      <span className="text-orange-600">${getCartTotal().total.toFixed(2)}</span>
                    </div>
                  </div>

                  <button className="w-full bg-orange-600 text-white py-4 rounded-lg font-bold hover:bg-orange-700 transition flex items-center justify-center gap-2">
                    <CreditCard size={20} />
                    Proceed to Checkout
                  </button>
                </>
              )}
            </div>
          </div>
        </div>
      )}
    </div>
  );
};

export default FoodDeliveryApp;
