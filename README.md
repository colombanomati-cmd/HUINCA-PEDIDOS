# HUINCA-PEDIDOS
import React, { useState, useMemo, useEffect } from 'react';
import { 
  Search, ShoppingBag, MapPin, Star, Clock, Bike, ChevronRight, 
  Plus, Minus, X, Check, ArrowLeft, Phone, CreditCard, DollarSign, 
  Send, AlertCircle, Sparkles, Utensils, Heart, Info, Filter, ShieldCheck
} from 'lucide-react';

const CATEGORIES = [
  { id: 'all', name: 'Todas', icon: '🍽️' },
  { id: 'rotiseria', name: 'Rotiserías y Comidas', icon: '🍗' },
  { id: 'lomitos', name: 'Hamburguesas y Lomitos', icon: '🍔' },
  { id: 'pizzas', name: 'Empanadas y Pizzas', icon: '🍕' },
  { id: 'helados', name: 'Heladerías y Postres', icon: '🍦' },
  { id: 'kiosco', name: 'Kioscos y Bebidas', icon: '🥤' },
  { id: 'mandados', name: 'Farmacias y Mandados', icon: '🛒' }
];

const MERCHANTS = [
  {
    id: 'don-luis',
    name: 'Rotisería Don Luis',
    category: 'rotiseria',
    rating: 4.9,
    reviewsCount: 128,
    deliveryTime: '25-40 min',
    deliveryFee: 400,
    minOrder: 1500,
    isOpen: true,
    image: 'https://images.unsplash.com/photo-1555396273-367ea4eb4db5?auto=format&fit=crop&w=600&q=80',
    coverImage: 'https://images.unsplash.com/photo-1504674900247-0877df9cc836?auto=format&fit=crop&w=1000&q=80',
    address: 'Av. San Martín 340, Huinca Renancó',
    badge: 'Más Popular 🌟',
    menu: [
      {
        id: 'dl-1',
        name: 'Pollo al Spiedo con Papas Fritas',
        description: 'Pollo entero dorado a las brasas con abundante porción de papas fritas provenzal.',
        price: 9800,
        category: 'Platos Principales',
        image: 'https://images.unsplash.com/photo-1626645738196-c2a7c87a8f58?auto=format&fit=crop&w=400&q=80',
        popular: true
      },
      {
        id: 'dl-2',
        name: 'Milanesa Completa a la Napolitana con Guarnición',
        description: 'Carne vacuna tierna, salsa fileto, jamón, queso cremoso y orégano. Sale con papas o ensalada.',
        price: 6500,
        category: 'Platos Principales',
        image: 'https://images.unsplash.com/photo-1619860860774-1e2e17343432?auto=format&fit=crop&w=400&q=80',
        popular: true
      },
      {
        id: 'dl-3',
        name: 'Pastel de Papa Casero (Porción abundante)',
        description: 'Relleno de carne cortada a cuchillo, huevo, aceitunas y cubierta de puré gratinado.',
        price: 4800,
        category: 'Platos Principales',
        image: 'https://images.unsplash.com/photo-1589301760014-d929f3979dbc?auto=format&fit=crop&w=400&q=80'
      },
      {
        id: 'dl-4',
        name: 'Ensalada Rusa Tradicional (500g)',
        description: 'Papa, zanahoria, arvejas y mayonesa casera de la abuela.',
        price: 2500,
        category: 'Guarniciones',
        image: 'https://images.unsplash.com/photo-1540420773420-3366772f4999?auto=format&fit=crop&w=400&q=80'
      }
    ]
  },
  {
    id: 'asador-huincan',
    name: 'El Asador Huinqueño',
    category: 'lomitos',
    rating: 4.8,
    reviewsCount: 94,
    deliveryTime: '20-35 min',
    deliveryFee: 0, // Envío gratis
    minOrder: 2000,
    isOpen: true,
    image: 'https://images.unsplash.com/photo-1568901346375-23c9450c58cd?auto=format&fit=crop&w=600&q=80',
    coverImage: 'https://images.unsplash.com/photo-1550547660-d9450f859349?auto=format&fit=crop&w=1000&q=80',
    address: 'Calle Córdoba 512, Huinca Renancó',
    badge: 'Envío Gratis 🛵',
    menu: [
      {
        id: 'ah-1',
        name: 'Lomito Completo "El Huinqueño"',
        description: 'Lomo tierno de ternera, queso, jamón, huevo frito, lechuga, tomate y mayonesa especial de la casa.',
        price: 6800,
        category: 'Lomitos & Burgers',
        image: 'https://images.unsplash.com/photo-1521305916504-4a1121188589?auto=format&fit=crop&w=400&q=80',
        popular: true
      },
      {
        id: 'ah-2',
        name: 'Hamburguesa Doble Cheddar & Bacon',
        description: '200g de medallón de carne 100% vacuno, panceta crocante y doble queso cheddar fundido.',
        price: 5900,
        category: 'Lomitos & Burgers',
        image: 'https://images.unsplash.com/photo-1586190848861-99aa4a171e90?auto=format&fit=crop&w=400&q=80',
        popular: true
      },
      {
        id: 'ah-3',
        name: 'Papas Rústicas Cheddar y Verdeo',
        description: 'Porción grande de papas rústicas con salsa cheddar tibia y verdeo fresco picado.',
        price: 3200,
        category: 'Acompañamientos',
        image: 'https://images.unsplash.com/photo-1576107232684-1279f3908594?auto=format&fit=crop&w=400&q=80'
      }
    ]
  },
  {
    id: 'pizzeria-centenario',
    name: 'Pizzería & Empanadas Centenario',
    category: 'pizzas',
    rating: 4.7,
    reviewsCount: 110,
    deliveryTime: '30-45 min',
    deliveryFee: 350,
    minOrder: 2500,
    isOpen: true,
    image: 'https://images.unsplash.com/photo-1513104890138-7c749659a591?auto=format&fit=crop&w=600&q=80',
    coverImage: 'https://images.unsplash.com/photo-1579751626657-72bc17010498?auto=format&fit=crop&w=1000&q=80',
    address: 'Av. Suipacha 120, Huinca Renancó',
    badge: 'Promos Docena 🔥',
    menu: [
      {
        id: 'pc-1',
        name: 'Pizza Muzzarella Gigante (8 porciones)',
        description: 'Salsa casera, abundante muzzarella de tambo local, aceitunas verdes y orégano.',
        price: 7200,
        category: 'Pizzas Especiales',
        image: 'https://images.unsplash.com/photo-1513104890138-7c749659a591?auto=format&fit=crop&w=400&q=80',
        popular: true
      },
      {
        id: 'pc-2',
        name: 'Pizza Fugazzeta Rellena',
        description: 'Masa crocante rellena de queso muzzarella y jamón, cubierta de cebolla dorada al horno.',
        price: 8500,
        category: 'Pizzas Especiales',
        image: 'https://images.unsplash.com/photo-1574071318508-1cdbab80d002?auto=format&fit=crop&w=400&q=80'
      },
      {
        id: 'pc-3',
        name: 'Docena de Empanadas Criollas Cortadas a Cuchillo',
        description: 'Empanadas tradicionales frotadas en grasa de pella o al horno. Carne, Jamón y Queso, Humita.',
        price: 7800,
        category: 'Empanadas',
        image: 'https://images.unsplash.com/photo-1626700051175-6818013e1d4f?auto=format&fit=crop&w=400&q=80',
        popular: true
      }
    ]
  },
  {
    id: 'heladeria-la-crema',
    name: 'Heladería Artesanal La Crema',
    category: 'helados',
    rating: 4.9,
    reviewsCount: 205,
    deliveryTime: '15-30 min',
    deliveryFee: 300,
    minOrder: 2000,
    isOpen: true,
    image: 'https://images.unsplash.com/photo-1567206563064-6f60f40a2b57?auto=format&fit=crop&w=600&q=80',
    coverImage: 'https://images.unsplash.com/photo-1501443762994-82bd5dace89a?auto=format&fit=crop&w=1000&q=80',
    address: 'Calle Rivadavia 205, Huinca Renancó',
    badge: 'Helado Premium 🍦',
    menu: [
      {
        id: 'lc-1',
        name: '1 Kilo de Helado Artesanal (Hasta 4 gustos)',
        description: 'Dulce de leche Huinca, Chocolate Granizado, Tramontana, Frutilla a la crema, Sabores al agua.',
        price: 6900,
        category: 'Potes de Helado',
        image: 'https://images.unsplash.com/photo-1567206563064-6f60f40a2b57?auto=format&fit=crop&w=400&q=80',
        popular: true
      },
      {
        id: 'lc-2',
        name: '1/2 Kilo de Helado Artesanal (Hasta 3 gustos)',
        description: 'Tu combinación favorita en pote térmico protector.',
        price: 3900,
        category: 'Potes de Helado',
        image: 'https://images.unsplash.com/photo-1570197788417-0e82375c9371?auto=format&fit=crop&w=400&q=80'
      },
      {
        id: 'lc-3',
        name: 'Cucurucho Gigante Bañado en Chocolate',
        description: 'Cucurucho crocante relleno con dulce de leche en la base y bañado en chocolate semiamargo.',
        price: 1800,
        category: 'Postres & Especiales',
        image: 'https://images.unsplash.com/photo-1557142046-c704a3adf364?auto=format&fit=crop&w=400&q=80'
      }
    ]
  },
  {
    id: 'kiosco-central',
    name: 'Kiosco & Drinks 24hs',
    category: 'kiosco',
    rating: 4.6,
    reviewsCount: 78,
    deliveryTime: '15-25 min',
    deliveryFee: 400,
    minOrder: 1000,
    isOpen: true,
    image: 'https://images.unsplash.com/photo-1527661591475-527312dd65f5?auto=format&fit=crop&w=600&q=80',
    coverImage: 'https://images.unsplash.com/photo-1625246333195-78d9c38ad449?auto=format&fit=crop&w=1000&q=80',
    address: 'Av. San Martín 780, Huinca Renancó',
    badge: 'Bebidas Frías ❄️',
    menu: [
      {
        id: 'kc-1',
        name: 'Pack Fernet Branca 750ml + Coca-Cola 2.25L',
        description: 'Combo clásico huinqueño listo para preparar, incluye bolsa de hielo de regalo.',
        price: 14500,
        category: 'Combos & Bebidas',
        image: 'https://images.unsplash.com/photo-1514362545857-3bc16c4c7d1b?auto=format&fit=crop&w=400&q=80',
        popular: true
      },
      {
        id: 'kc-2',
        name: 'Cerveza Quilmes / Brahma 1 Litro Retornable (Fría)',
        description: 'Cerveza rubia helada lista para servir.',
        price: 2400,
        category: 'Cervezas',
        image: 'https://images.unsplash.com/photo-1608270586620-248524c67de9?auto=format&fit=crop&w=400&q=80'
      },
      {
        id: 'kc-3',
        name: 'Combo Picada Snack (Papas Lays + Doritos + Maní)',
        description: 'Pack variadito para picar viendo el partido o con amigos.',
        price: 3600,
        category: 'Snacks',
        image: 'https://images.unsplash.com/photo-1566478989037-eec170784d0b?auto=format&fit=crop&w=400&q=80'
      }
    ]
  },
  {
    id: 'farmacia-huinca',
    name: 'Farmacia & Turno Huinca',
    category: 'mandados',
    rating: 4.9,
    reviewsCount: 52,
    deliveryTime: '20-30 min',
    deliveryFee: 300,
    minOrder: 1000,
    isOpen: true,
    image: 'https://images.unsplash.com/photo-1586015555751-63bb77f4322a?auto=format&fit=crop&w=600&q=80',
    coverImage: 'https://images.unsplash.com/photo-1576602976047-174e57a47881?auto=format&fit=crop&w=1000&q=80',
    address: 'Calle Balcarce 410, Huinca Renancó',
    badge: 'De Turno 🏥',
    menu: [
      {
        id: 'fh-1',
        name: 'Kit Cuidado Personal & Higiene',
        description: 'Jabón neutro, alcohol en gel 250ml y paquete de pañuelos descartables.',
        price: 3200,
        category: 'Cuidado Personal',
        image: 'https://images.unsplash.com/photo-1584308666744-24d5c474f2ae?auto=format&fit=crop&w=400&q=80'
      },
      {
        id: 'fh-2',
        name: 'Protector Solar FPS 50 (200ml)',
        description: 'Protección alta resistente al agua y sudor.',
        price: 8900,
        category: 'Perfumería',
        image: 'https://images.unsplash.com/photo-1522337360788-8b13dee7a37e?auto=format&fit=crop&w=400&q=80'
      }
    ]
  }
];

export default function App() {
  // Navigation and filtering states
  const [selectedCategory, setSelectedCategory] = useState('all');
  const [searchQuery, setSearchQuery] = useState('');
  const [selectedMerchant, setSelectedMerchant] = useState(null);
  
  // Cart state
  const [cart, setCart] = useState([]);
  const [isCartOpen, setIsCartOpen] = useState(false);
  const [isCheckoutOpen, setIsCheckoutOpen] = useState(false);
  
  // Toast Notification state
  const [toast, setToast] = useState(null);

  // Delivery Address State
  const [userAddress, setUserAddress] = useState('Av. San Martín 450, Huinca Renancó');
  const [isEditingAddress, setIsEditingAddress] = useState(false);

  // Form Checkout State
  const [checkoutData, setCheckoutData] = useState({
    customerName: '',
    phone: '',
    notes: '',
    paymentMethod: 'efectivo', // 'efectivo', 'mp', 'posnet'
    cashAmount: ''
  });

  // Display Toast Notification Helper
  const showToast = (message) => {
    setToast(message);
    setTimeout(() => setToast(null), 3000);
  };

  const addToCart = (item, merchant) => {
    // If cart has items from a different merchant, ask for confirmation
    if (cart.length > 0 && cart[0].merchantId !== merchant.id) {
      if (window.confirm(`Tu carrito tiene productos de "${cart[0].merchantName}". ¿Deseas vaciarlo para agregar productos de "${merchant.name}"?`)) {
        setCart([{ ...item, merchantId: merchant.id, merchantName: merchant.name, quantity: 1 }]);
        showToast(`Agregado: ${item.name}`);
      }
      return;
    }

    setCart(prevCart => {
      const existing = prevCart.find(i => i.id === item.id);
      if (existing) {
        return prevCart.map(i => i.id === item.id ? { ...i, quantity: i.quantity + 1 } : i);
      }
      return [...prevCart, { ...item, merchantId: merchant.id, merchantName: merchant.name, quantity: 1 }];
    });
    showToast(`Agregado a tu pedido: ${item.name}`);
  };

  const updateCartQuantity = (itemId, delta) => {
    setCart(prevCart => {
      return prevCart.map(item => {
        if (item.id === itemId) {
          const newQty = item.quantity + delta;
          return newQty > 0 ? { ...item, quantity: newQty } : null;
        }
        return item;
      }).filter(Boolean);
    });
  };

  // Calculations
  const cartSubtotal = useMemo(() => {
    return cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
  }, [cart]);

  const currentCartMerchant = useMemo(() => {
    if (cart.length === 0) return null;
    return MERCHANTS.find(m => m.id === cart[0].merchantId);
  }, [cart]);

  const deliveryFee = currentCartMerchant ? currentCartMerchant.deliveryFee : 0;
  const cartTotal = cartSubtotal + deliveryFee;
  const totalItemsCount = cart.reduce((sum, i) => sum + i.quantity, 0);

  const filteredMerchants = useMemo(() => {
    return MERCHANTS.filter(m => {
      const matchesCategory = selectedCategory === 'all' || m.category === selectedCategory;
      const matchesSearch = searchQuery.trim() === '' || 
        m.name.toLowerCase().includes(searchQuery.toLowerCase()) ||
        m.menu.some(dish => dish.name.toLowerCase().includes(searchQuery.toLowerCase()) || dish.description.toLowerCase().includes(searchQuery.toLowerCase()));
      return matchesCategory && matchesSearch;
    });
  }, [selectedCategory, searchQuery]);

  const handleSendWhatsApp = (e) => {
    e.preventDefault();
    if (!checkoutData.customerName.trim()) {
      alert('Por favor ingresa tu nombre completo.');
      return;
    }
    if (!checkoutData.phone.trim()) {
      alert('Por favor ingresa un número de teléfono de contacto.');
      return;
    }

    const itemsText = cart.map(item => `• ${item.quantity}x ${item.name} ($${item.price * item.quantity})`).join('%0A');
    let paymentInfoText = '';

    if (checkoutData.paymentMethod === 'efectivo') {
      paymentInfoText = `Efectivo ${checkoutData.cashAmount ? `(Paga con $${checkoutData.cashAmount})` : ''}`;
    } else if (checkoutData.paymentMethod === 'mp') {
      paymentInfoText = 'Transferencia Mercado Pago (Alias: huincapedidos.mp)';
    } else {
      paymentInfoText = 'Tarjeta Débito/Crédito al repartidor';
    }

    const message = 
      `*¡NUEVO PEDIDO DESDE HUINCA PEDIDOS!* 🛵%0A%0A` +
      `*Local:* ${currentCartMerchant?.name}%0A` +
      `*Cliente:* ${checkoutData.customerName}%0A` +
      `*Teléfono:* ${checkoutData.phone}%0A` +
      `*Dirección de Envío:* ${userAddress}%0A` +
      `${checkoutData.notes ? `*Notas/Aclaraciones:* ${checkoutData.notes}%0A` : ''}` +
      `%0A*Detalle del Pedido:*%0A${itemsText}%0A%0A` +
      `*Subtotal:* $${cartSubtotal}%0A` +
      `*Costo de Envío:* $${deliveryFee}%0A` +
      `*TOTAL A PAGAR:* $${cartTotal}%0A%0A` +
      `*Forma de Pago:* ${paymentInfoText}%0A%0A` +
      `_Enviado desde huincapedidos.com.ar_`;

    // Simulated phone number for local Huinca Pedidos dispatch
    const whatsappUrl = `https://api.whatsapp.com/send?phone=5493583400000&text=${message}`;
    window.open(whatsappUrl, '_blank');
  };

  return (
    <div className="min-h-screen bg-slate-50 font-sans text-slate-800 flex flex-col pb-24 md:pb-8">
      {/* Toast Notification Alert */}
      {toast && (
        <div className="fixed top-20 right-4 z-50 bg-emerald-600 text-white px-4 py-3 rounded-xl shadow-2xl flex items-center gap-2 animate-bounce">
          <Check className="w-5 h-5" />
          <span className="font-medium text-sm">{toast}</span>
        </div>
      )}

      {}
      <header className="sticky top-0 z-40 bg-gradient-to-r from-orange-600 via-orange-500 to-amber-500 text-white shadow-md">
        <div className="max-w-6xl mx-auto px-4 py-3 flex items-center justify-between gap-3">
          
          {/* Logo & Local Identity */}
          <div 
            onClick={() => { setSelectedMerchant(null); }}
            className="flex items-center gap-2 cursor-pointer group"
          >
            <div className="bg-white text-orange-600 p-2 rounded-2xl shadow-inner font-extrabold text-xl tracking-tight group-hover:scale-105 transition-transform flex items-center justify-center">
              <Bike className="w-6 h-6 text-orange-600" />
            </div>
            <div>
              <h1 className="font-black text-xl tracking-wide leading-none flex items-center gap-1">
                HUINCA <span className="text-amber-200">PEDIDOS</span>
              </h1>
              <p className="text-[10px] text-orange-100 font-medium tracking-wider uppercase">Huinca Renancó, Cba</p>
            </div>
          </div>

          {/* Delivery Address Selector */}
          <div className="hidden md:flex items-center bg-orange-700/40 border border-orange-400/30 px-3 py-1.5 rounded-full text-xs">
            <MapPin className="w-4 h-4 text-amber-300 mr-1.5 shrink-0" />
            <span className="text-orange-100 mr-1">Enviar a:</span>
            {isEditingAddress ? (
              <input
                type="text"
                value={userAddress}
                onChange={(e) => setUserAddress(e.target.value)}
                onBlur={() => setIsEditingAddress(false)}
                className="bg-white text-slate-800 px-2 py-0.5 rounded text-xs font-semibold focus:outline-none"
                autoFocus
              />
            ) : (
              <button 
                onClick={() => setIsEditingAddress(true)}
                className="font-bold text-white hover:underline flex items-center gap-1"
              >
                {userAddress}
              </button>
            )}
          </div>

          {/* Cart Icon & Counter Header Button */}
          <button
            onClick={() => setIsCartOpen(true)}
            className="relative bg-white text-orange-600 hover:bg-orange-50 font-bold px-4 py-2 rounded-full shadow-md transition-all flex items-center gap-2 text-sm"
          >
            <ShoppingBag className="w-5 h-5 text-orange-600" />
            <span className="hidden sm:inline">Tu Pedido</span>
            {totalItemsCount > 0 && (
              <span className="bg-orange-600 text-white text-xs font-extrabold px-2 py-0.5 rounded-full">
                {totalItemsCount}
              </span>
            )}
            <span className="font-extrabold text-orange-700">
              ${cartTotal.toLocaleString('es-AR')}
            </span>
          </button>
        </div>

        {/* Address Bar Mobile View */}
        <div className="md:hidden bg-orange-700/50 px-4 py-2 flex items-center justify-between text-xs text-orange-100 border-t border-orange-400/20">
          <div className="flex items-center gap-1 truncate max-w-[85%]">
            <MapPin className="w-3.5 h-3.5 text-amber-300 shrink-0" />
            <span>Enviar a:</span>
            <span className="font-bold text-white truncate">{userAddress}</span>
          </div>
          <button 
            onClick={() => {
              const newAdd = prompt("Ingresa tu dirección en Huinca Renancó:", userAddress);
              if (newAdd) setUserAddress(newAdd);
            }} 
            className="underline font-semibold text-amber-200 shrink-0"
          >
            Cambiar
          </button>
        </div>
      </header>

      {}
      {selectedMerchant ? (
        /* ================= MERCHANT DETAIL VIEW ================= */
        <main className="max-w-5xl mx-auto w-full px-4 py-6 flex-grow animate-fadeIn">
          {/* Back Button */}
          <button
            onClick={() => setSelectedMerchant(null)}
            className="inline-flex items-center gap-2 text-sm font-bold text-orange-600 bg-white border border-slate-200 px-4 py-2 rounded-xl shadow-sm hover:bg-orange-50 transition-colors mb-4"
          >
            <ArrowLeft className="w-4 h-4" />
            Volver a Comercios
          </button>

          {/* Merchant Header Card */}
          <div className="bg-white rounded-2xl shadow-sm border border-slate-200 overflow-hidden mb-6">
            <div className="h-48 sm:h-64 relative w-full overflow-hidden bg-slate-100">
              <img 
                src={selectedMerchant.coverImage} 
                alt={selectedMerchant.name} 
                className="w-full h-full object-cover"
              />
              <div className="absolute inset-0 bg-gradient-to-t from-black/70 via-black/20 to-transparent" />
              
              {/* Badge Overlay */}
              <span className="absolute top-4 right-4 bg-orange-500 text-white font-bold text-xs px-3 py-1.5 rounded-full shadow-lg">
                {selectedMerchant.badge}
              </span>
            </div>

            <div className="p-5 sm:p-6 relative -mt-12 bg-white rounded-t-3xl border-t border-slate-100 shadow-lg">
              <div className="flex flex-col sm:flex-row sm:items-center justify-between gap-4">
                <div>
                  <h2 className="text-2xl sm:text-3xl font-black text-slate-900 tracking-tight">
                    {selectedMerchant.name}
                  </h2>
                  <p className="text-slate-500 text-xs sm:text-sm mt-1 flex items-center gap-1">
                    <MapPin className="w-3.5 h-3.5 text-slate-400" />
                    {selectedMerchant.address}
                  </p>
                </div>

                {/* Rating & Delivery Info */}
                <div className="flex items-center gap-3 bg-slate-50 p-3 rounded-xl border border-slate-100 self-start sm:self-auto">
                  <div className="flex items-center gap-1 bg-amber-100 text-amber-800 px-2 py-1 rounded-lg font-bold text-sm">
                    <Star className="w-4 h-4 fill-amber-500 text-amber-500" />
                    <span>{selectedMerchant.rating}</span>
                  </div>
                  <div className="h-6 w-px bg-slate-200" />
                  <div className="text-xs">
                    <p className="text-slate-500 font-medium flex items-center gap-1">
                      <Clock className="w-3.5 h-3.5 text-slate-400" /> {selectedMerchant.deliveryTime}
                    </p>
                    <p className="text-slate-700 font-bold mt-0.5">
                      {selectedMerchant.deliveryFee === 0 ? 'Envío Gratis' : `Envío: $${selectedMerchant.deliveryFee}`}
                    </p>
                  </div>
                </div>
              </div>
            </div>
          </div>

          {/* Menu Items Grid */}
          <h3 className="text-xl font-bold text-slate-900 mb-4 flex items-center gap-2">
            <Utensils className="w-5 h-5 text-orange-600" />
            Menú disponible
          </h3>

          <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
            {selectedMerchant.menu.map(dish => (
              <div 
                key={dish.id} 
                className="bg-white rounded-2xl p-4 border border-slate-200/80 shadow-sm hover:shadow-md transition-all flex justify-between gap-4 relative overflow-hidden"
              >
                {dish.popular && (
                  <span className="absolute top-0 right-0 bg-amber-500 text-white text-[10px] font-extrabold px-2.5 py-0.5 rounded-bl-xl uppercase tracking-wider">
                    Recomendado
                  </span>
                )}
                <div className="flex-1 flex flex-col justify-between">
                  <div>
                    <h4 className="font-bold text-slate-900 text-base leading-snug">{dish.name}</h4>
                    <p className="text-slate-500 text-xs mt-1.5 line-clamp-2 leading-relaxed">
                      {dish.description}
                    </p>
                  </div>
                  <div className="mt-4 flex items-center justify-between">
                    <span className="font-black text-slate-900 text-lg">
                      ${dish.price.toLocaleString('es-AR')}
                    </span>
                    <button
                      onClick={() => addToCart(dish, selectedMerchant)}
                      className="bg-orange-600 hover:bg-orange-700 active:scale-95 text-white font-bold text-xs px-3.5 py-2 rounded-xl shadow-sm transition-all flex items-center gap-1"
                    >
                      <Plus className="w-4 h-4" /> Agregar
                    </button>
                  </div>
                </div>

                <div className="w-24 h-24 sm:w-28 sm:h-28 rounded-xl overflow-hidden bg-slate-100 shrink-0 border border-slate-100">
                  <img 
                    src={dish.image} 
                    alt={dish.name} 
                    className="w-full h-full object-cover"
                  />
                </div>
              </div>
            ))}
          </div>
        </main>
      ) : (
        /* ================= MAIN HOME / CATALOG VIEW ================= */
        <main className="max-w-6xl mx-auto w-full px-4 py-6 flex-grow">
          
          {}
          <div className="bg-gradient-to-r from-orange-500 to-amber-500 rounded-3xl p-6 sm:p-8 text-white shadow-xl mb-8 relative overflow-hidden">
            <div className="relative z-10 max-w-xl">
              <span className="inline-flex items-center gap-1.5 bg-white/20 backdrop-blur-md px-3 py-1 rounded-full text-xs font-semibold text-amber-100 mb-3 border border-white/20">
                <Sparkles className="w-3.5 h-3.5 text-amber-200" />
                Delivery de Comidas y Mandados en Huinca Renancó
              </span>
              <h2 className="text-3xl sm:text-4xl font-black tracking-tight leading-tight">
                ¿Qué vas a pedir hoy?
              </h2>
              <p className="text-orange-100 text-sm sm:text-base mt-2">
                Los mejores locales de tu pueblo, directo a tu mesa con un clic.
              </p>

              {/* Search Bar */}
              <div className="mt-5 relative">
                <Search className="w-5 h-5 text-slate-400 absolute left-4 top-1/2 -translate-y-1/2" />
                <input
                  type="text"
                  placeholder="Buscar rotisería, hamburguesa, lomito, pizza, helado..."
                  value={searchQuery}
                  onChange={(e) => setSearchQuery(e.target.value)}
                  className="w-full pl-11 pr-4 py-3.5 rounded-2xl bg-white text-slate-900 placeholder-slate-400 font-medium text-sm shadow-md focus:outline-none focus:ring-4 focus:ring-orange-300/50"
                />
                {searchQuery && (
                  <button 
                    onClick={() => setSearchQuery('')}
                    className="absolute right-4 top-1/2 -translate-y-1/2 text-slate-400 hover:text-slate-600"
                  >
                    <X className="w-4 h-4" />
                  </button>
                )}
              </div>
            </div>

            {/* Decorative Background Circles */}
            <div className="absolute -right-12 -bottom-12 w-64 h-64 bg-white/10 rounded-full blur-2xl pointer-events-none" />
          </div>

          {}
          <section className="mb-8">
            <div className="flex items-center justify-between mb-3">
              <h3 className="font-extrabold text-slate-900 text-lg tracking-tight">Categorías</h3>
            </div>
            
            <div className="flex items-center gap-2.5 overflow-x-auto pb-2 scrollbar-none">
              {CATEGORIES.map(cat => {
                const isActive = selectedCategory === cat.id;
                return (
                  <button
                    key={cat.id}
                    onClick={() => setSelectedCategory(cat.id)}
                    className={`flex items-center gap-2 px-4 py-2.5 rounded-2xl font-bold text-xs whitespace-nowrap transition-all border ${
                      isActive 
                        ? 'bg-orange-600 text-white border-orange-600 shadow-md scale-105' 
                        : 'bg-white text-slate-700 border-slate-200/80 hover:border-orange-300 hover:bg-orange-50/50'
                    }`}
                  >
                    <span className="text-base">{cat.icon}</span>
                    <span>{cat.name}</span>
                  </button>
                );
              })}
            </div>
          </section>

          {}
          <section>
            <div className="flex items-center justify-between mb-4">
              <h3 className="font-extrabold text-slate-900 text-xl tracking-tight flex items-center gap-2">
                Comercios Adheridos
                <span className="text-xs bg-orange-100 text-orange-700 px-2.5 py-0.5 rounded-full font-bold">
                  {filteredMerchants.length}
                </span>
              </h3>
            </div>

            {filteredMerchants.length === 0 ? (
              <div className="text-center py-12 bg-white rounded-3xl border border-slate-200/80 p-6">
                <Utensils className="w-12 h-12 text-slate-300 mx-auto mb-3" />
                <h4 className="font-bold text-slate-700 text-base">No encontramos resultados</h4>
                <p className="text-slate-400 text-xs mt-1">Prueba buscar otro tipo de comida o borra los filtros de búsqueda.</p>
                <button
                  onClick={() => { setSelectedCategory('all'); setSearchQuery(''); }}
                  className="mt-4 text-xs font-bold text-orange-600 hover:underline"
                >
                  Restablecer filtros
                </button>
              </div>
            ) : (
              <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
                {filteredMerchants.map(merchant => (
                  <div
                    key={merchant.id}
                    onClick={() => setSelectedMerchant(merchant)}
                    className="bg-white rounded-2xl border border-slate-200/80 shadow-sm hover:shadow-xl transition-all duration-300 overflow-hidden cursor-pointer group flex flex-col justify-between"
                  >
                    <div>
                      {/* Image Banner */}
                      <div className="h-44 relative overflow-hidden bg-slate-100">
                        <img 
                          src={merchant.image} 
                          alt={merchant.name} 
                          className="w-full h-full object-cover group-hover:scale-105 transition-transform duration-500"
                        />
                        <div className="absolute inset-0 bg-gradient-to-t from-black/60 via-transparent to-transparent opacity-80" />
                        
                        {/* Rating Badge */}
                        <div className="absolute top-3 left-3 bg-white/95 backdrop-blur-md px-2.5 py-1 rounded-xl shadow-md flex items-center gap-1 font-extrabold text-xs text-slate-900">
                          <Star className="w-3.5 h-3.5 fill-amber-400 text-amber-400" />
                          <span>{merchant.rating}</span>
                          <span className="text-slate-400 font-normal">({merchant.reviewsCount})</span>
                        </div>

                        {/* Status / Feature Badge */}
                        <span className="absolute top-3 right-3 bg-orange-600 text-white font-bold text-[10px] px-2.5 py-1 rounded-lg shadow-md uppercase tracking-wide">
                          {merchant.badge}
                        </span>

                        <div className="absolute bottom-3 left-3 right-3 text-white">
                          <h4 className="font-black text-lg leading-snug drop-shadow-md">
                            {merchant.name}
                          </h4>
                          <p className="text-slate-200 text-xs flex items-center gap-1 mt-0.5">
                            <MapPin className="w-3 h-3 text-amber-300" />
                            {merchant.address}
                          </p>
                        </div>
                      </div>

                      {/* Card Body Info */}
                      <div className="p-4 flex items-center justify-between text-xs text-slate-600">
                        <div className="flex items-center gap-1 font-medium bg-slate-100 px-2.5 py-1 rounded-lg">
                          <Clock className="w-3.5 h-3.5 text-slate-500" />
                          <span>{merchant.deliveryTime}</span>
                        </div>

                        <div className="font-bold text-slate-800">
                          {merchant.deliveryFee === 0 ? (
                            <span className="text-emerald-600 font-extrabold">Envío Gratis</span>
                          ) : (
                            <span>Envío: ${merchant.deliveryFee}</span>
                          )}
                        </div>
                      </div>
                    </div>

                    {/* Action Footer */}
                    <div className="px-4 py-3 bg-slate-50/80 border-t border-slate-100 flex items-center justify-between">
                      <span className="text-[11px] text-slate-500 font-medium">Mínimo: ${merchant.minOrder}</span>
                      <span className="text-xs font-bold text-orange-600 flex items-center gap-1 group-hover:translate-x-1 transition-transform">
                        Ver Menú <ChevronRight className="w-3.5 h-3.5" />
                      </span>
                    </div>
                  </div>
                ))}
              </div>
            )}
          </section>
        </main>
      )}

      {}
      {isCartOpen && (
        <div className="fixed inset-0 z-50 overflow-hidden bg-slate-900/60 backdrop-blur-sm animate-fadeIn">
          <div className="absolute inset-y-0 right-0 max-w-full flex pl-10">
            <div className="w-screen max-w-md bg-white shadow-2xl flex flex-col justify-between">
              
              {/* Drawer Header */}
              <div className="p-4 bg-orange-600 text-white flex items-center justify-between">
                <div className="flex items-center gap-2">
                  <ShoppingBag className="w-5 h-5" />
                  <h3 className="font-bold text-lg">Tu Pedido</h3>
                </div>
                <button 
                  onClick={() => setIsCartOpen(false)}
                  className="p-1 rounded-full hover:bg-orange-700 text-white"
                >
                  <X className="w-6 h-6" />
                </button>
              </div>

              {/* Drawer Body Items List */}
              <div className="p-4 flex-1 overflow-y-auto">
                {cart.length === 0 ? (
                  <div className="text-center py-16 text-slate-400">
                    <ShoppingBag className="w-16 h-16 mx-auto mb-3 opacity-40" />
                    <p className="font-bold text-slate-600 text-base">Tu carrito está vacío</p>
                    <p className="text-xs mt-1">Explora los comercios de Huinca y agrega tus productos favoritos.</p>
                  </div>
                ) : (
                  <div>
                    {/* Merchant banner badge inside cart */}
                    <div className="bg-amber-50 border border-amber-200 p-3 rounded-xl mb-4 flex items-center justify-between">
                      <span className="text-xs font-bold text-amber-900">
                        Pedido a: <span className="underline">{currentCartMerchant?.name}</span>
                      </span>
                      <span className="text-[10px] bg-amber-200 text-amber-800 font-bold px-2 py-0.5 rounded">
                        Huinca Renancó
                      </span>
                    </div>

                    <div className="space-y-3">
                      {cart.map(item => (
                        <div 
                          key={item.id} 
                          className="flex items-center justify-between p-3 bg-slate-50 rounded-xl border border-slate-200/80"
                        >
                          <div className="flex-1 pr-2">
                            <h5 className="font-bold text-slate-900 text-sm leading-tight">{item.name}</h5>
                            <p className="text-xs font-semibold text-slate-500 mt-1">
                              ${(item.price * item.quantity).toLocaleString('es-AR')}
                            </p>
                          </div>

                          {/* Quantity Controls */}
                          <div className="flex items-center gap-2 bg-white border border-slate-200 rounded-lg p-1">
                            <button
                              onClick={() => updateCartQuantity(item.id, -1)}
                              className="p-1 hover:bg-slate-100 rounded text-slate-600"
                            >
                              <Minus className="w-3.5 h-3.5" />
                            </button>
                            <span className="font-bold text-xs text-slate-900 px-1">
                              {item.quantity}
                            </span>
                            <button
                              onClick={() => updateCartQuantity(item.id, 1)}
                              className="p-1 hover:bg-slate-100 rounded text-slate-600"
                            >
                              <Plus className="w-3.5 h-3.5" />
                            </button>
                          </div>
                        </div>
                      ))}
                    </div>

                    {/* Order Summary Breakdown */}
                    <div className="mt-6 border-t border-slate-200 pt-4 space-y-2 text-xs">
                      <div className="flex justify-between text-slate-600">
                        <span>Subtotal productos</span>
                        <span className="font-bold">${cartSubtotal.toLocaleString('es-AR')}</span>
                      </div>
                      <div className="flex justify-between text-slate-600">
                        <span>Costo de envío (Local)</span>
                        <span className="font-bold">
                          {deliveryFee === 0 ? '¡Gratis!' : `$${deliveryFee.toLocaleString('es-AR')}`}
                        </span>
                      </div>
                      <div className="flex justify-between text-slate-900 font-extrabold text-base border-t border-slate-200 pt-2">
                        <span>Total Final</span>
                        <span className="text-orange-600">${cartTotal.toLocaleString('es-AR')}</span>
                      </div>
                    </div>
                  </div>
                )}
              </div>

              {/* Drawer Footer Actions */}
              {cart.length > 0 && (
                <div className="p-4 bg-slate-50 border-t border-slate-200">
                  <button
                    onClick={() => {
                      setIsCartOpen(false);
                      setIsCheckoutOpen(true);
                    }}
                    className="w-full bg-emerald-600 hover:bg-emerald-700 text-white font-extrabold py-3 rounded-xl shadow-lg transition-all flex items-center justify-center gap-2 text-sm"
                  >
                    <span>Continuar al Checkout</span>
                    <ChevronRight className="w-4 h-4" />
                  </button>
                </div>
              )}
            </div>
          </div>
        </div>
      )}

      {}
      {isCheckoutOpen && (
        <div className="fixed inset-0 z-50 overflow-y-auto bg-slate-900/60 backdrop-blur-sm flex items-center justify-center p-4 animate-fadeIn">
          <div className="bg-white rounded-3xl max-w-lg w-full overflow-hidden shadow-2xl border border-slate-100 my-8">
            
            {/* Modal Header */}
            <div className="bg-gradient-to-r from-orange-600 to-amber-500 p-5 text-white flex items-center justify-between">
              <div>
                <h3 className="font-black text-xl tracking-tight">Finalizar Pedido</h3>
                <p className="text-orange-100 text-xs mt-0.5">Huinca Pedidos • Envío a Domicilio</p>
              </div>
              <button 
                onClick={() => setIsCheckoutOpen(false)}
                className="text-white hover:bg-white/20 p-1.5 rounded-full transition-colors"
              >
                <X className="w-5 h-5" />
              </button>
            </div>

            {/* Modal Form */}
            <form onSubmit={handleSendWhatsApp} className="p-6 space-y-4">
              
              {/* Customer Info */}
              <div>
                <label className="block text-xs font-bold text-slate-700 mb-1">Nombre Completo *</label>
                <input
                  type="text"
                  required
                  placeholder="Ej: Juan Pérez"
                  value={checkoutData.customerName}
                  onChange={(e) => setCheckoutData({ ...checkoutData, customerName: e.target.value })}
                  className="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 text-sm focus:outline-none focus:ring-2 focus:ring-orange-500/50"
                />
              </div>

              <div>
                <label className="block text-xs font-bold text-slate-700 mb-1">Teléfono / WhatsApp *</label>
                <input
                  type="tel"
                  required
                  placeholder="Ej: 3583 123456"
                  value={checkoutData.phone}
                  onChange={(e) => setCheckoutData({ ...checkoutData, phone: e.target.value })}
                  className="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 text-sm focus:outline-none focus:ring-2 focus:ring-orange-500/50"
                />
              </div>

              <div>
                <label className="block text-xs font-bold text-slate-700 mb-1">Dirección de Entrega</label>
                <div className="flex items-center gap-2 bg-slate-100 p-3 rounded-xl text-xs font-bold text-slate-800 border border-slate-200">
                  <MapPin className="w-4 h-4 text-orange-600 shrink-0" />
                  <span className="flex-1 truncate">{userAddress}</span>
                  <button 
                    type="button"
                    onClick={() => {
                      const newAdd = prompt("Ingresa tu nueva dirección:", userAddress);
                      if (newAdd) setUserAddress(newAdd);
                    }}
                    className="text-orange-600 text-[11px] underline shrink-0 font-bold"
                  >
                    Editar
                  </button>
                </div>
              </div>

              <div>
                <label className="block text-xs font-bold text-slate-700 mb-1">Notas para la cocina o repartidor (Opcional)</label>
                <textarea
                  placeholder="Ej: Timbre blanco, empanadas sin aceituna, etc."
                  value={checkoutData.notes}
                  onChange={(e) => setCheckoutData({ ...checkoutData, notes: e.target.value })}
                  rows={2}
                  className="w-full px-3.5 py-2 rounded-xl border border-slate-300 text-xs focus:outline-none focus:ring-2 focus:ring-orange-500/50"
                />
              </div>

              {/* Payment Method Selector */}
              <div>
                <label className="block text-xs font-bold text-slate-700 mb-2">Método de Pago</label>
                <div className="grid grid-cols-3 gap-2">
                  <button
                    type="button"
                    onClick={() => setCheckoutData({ ...checkoutData, paymentMethod: 'efectivo' })}
                    className={`p-2.5 rounded-xl border text-xs font-bold flex flex-col items-center gap-1 transition-all ${
                      checkoutData.paymentMethod === 'efectivo' 
                        ? 'border-orange-600 bg-orange-50 text-orange-700 shadow-sm' 
                        : 'border-slate-200 text-slate-600 hover:bg-slate-50'
                    }`}
                  >
                    <DollarSign className="w-4 h-4" />
                    <span>Efectivo</span>
                  </button>

                  <button
                    type="button"
                    onClick={() => setCheckoutData({ ...checkoutData, paymentMethod: 'mp' })}
                    className={`p-2.5 rounded-xl border text-xs font-bold flex flex-col items-center gap-1 transition-all ${
                      checkoutData.paymentMethod === 'mp' 
                        ? 'border-orange-600 bg-orange-50 text-orange-700 shadow-sm' 
                        : 'border-slate-200 text-slate-600 hover:bg-slate-50'
                    }`}
                  >
                    <Send className="w-4 h-4" />
                    <span>Transferencia</span>
                  </button>

                  <button
                    type="button"
                    onClick={() => setCheckoutData({ ...checkoutData, paymentMethod: 'posnet' })}
                    className={`p-2.5 rounded-xl border text-xs font-bold flex flex-col items-center gap-1 transition-all ${
                      checkoutData.paymentMethod === 'posnet' 
                        ? 'border-orange-600 bg-orange-50 text-orange-700 shadow-sm' 
                        : 'border-slate-200 text-slate-600 hover:bg-slate-50'
                    }`}
                  >
                    <CreditCard className="w-4 h-4" />
                    <span>Tarjeta</span>
                  </button>
                </div>

                {/* Conditional Cash Amount field */}
                {checkoutData.paymentMethod === 'efectivo' && (
                  <div className="mt-3 bg-slate-50 p-3 rounded-xl border border-slate-200">
                    <label className="block text-[11px] font-semibold text-slate-600 mb-1">¿Pagas con cuánto? (Para llevar vuelto)</label>
                    <input
                      type="number"
                      placeholder={`Ej: $${Math.ceil(cartTotal / 1000) * 1000}`}
                      value={checkoutData.cashAmount}
                      onChange={(e) => setCheckoutData({ ...checkoutData, cashAmount: e.target.value })}
                      className="w-full px-3 py-1.5 rounded-lg border border-slate-300 text-xs focus:outline-none"
                    />
                  </div>
                )}

                {/* Mercado Pago Alias Info */}
                {checkoutData.paymentMethod === 'mp' && (
                  <div className="mt-3 bg-blue-50 border border-blue-200 p-3 rounded-xl text-xs text-blue-900">
                    <p className="font-bold flex items-center gap-1">
                      <ShieldCheck className="w-4 h-4 text-blue-600" />
                      Alias Mercado Pago: <span className="underline font-black">huincapedidos.mp</span>
                    </p>
                    <p className="text-[11px] text-blue-700 mt-1">Envía el comprobante por WhatsApp al confirmar el pedido.</p>
                  </div>
                )}
              </div>

              {/* Total Summary */}
              <div className="bg-slate-50 p-3 rounded-xl border border-slate-200 flex items-center justify-between">
                <div>
                  <span className="text-xs text-slate-500 font-medium">Total a abonar</span>
                  <p className="text-xl font-black text-slate-900">${cartTotal.toLocaleString('es-AR')}</p>
                </div>
                <span className="text-[10px] bg-emerald-100 text-emerald-800 font-bold px-2 py-1 rounded">
                  Envío Seguro
                </span>
              </div>

              {/* WhatsApp Submit Action */}
              <button
                type="submit"
                className="w-full bg-emerald-600 hover:bg-emerald-700 active:scale-98 text-white font-black py-3.5 rounded-2xl shadow-xl transition-all flex items-center justify-center gap-2 text-sm mt-2"
              >
                <Send className="w-4 h-4" />
                Confirmar y Enviar Pedido por WhatsApp
              </button>
            </form>
          </div>
        </div>
      )}

      {}
      {cart.length > 0 && !isCartOpen && !isCheckoutOpen && (
        <div className="fixed bottom-0 left-0 right-0 z-30 p-3 bg-white border-t border-slate-200 shadow-2xl md:hidden">
          <button
            onClick={() => setIsCartOpen(true)}
            className="w-full bg-orange-600 text-white font-black py-3 px-4 rounded-xl shadow-lg flex items-center justify-between text-sm"
          >
            <div className="flex items-center gap-2">
              <span className="bg-white text-orange-600 px-2 py-0.5 rounded-full font-extrabold text-xs">
                {totalItemsCount}
              </span>
              <span>Ver Carrito</span>
            </div>
            <span className="text-amber-200 font-extrabold">
              ${cartTotal.toLocaleString('es-AR')}
            </span>
          </button>
        </div>
      )}

      {}
      <footer className="mt-auto bg-slate-900 text-slate-400 py-8 text-center text-xs border-t border-slate-800">
        <div className="max-w-6xl mx-auto px-4">
          <p className="font-bold text-slate-200 text-sm mb-1">
            HUINCA PEDIDOS
          </p>
          <p>La plataforma de pedidos online oficial de Huinca Renancó, Córdoba.</p>
          <p className="mt-4 text-slate-500">© 2026 Huinca Pedidos. Todos los derechos reservados.</p>
        </div>
      </footer>
    </div>
  );
}
