<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Meal Minds - Fast Food Billing System</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: #f5f5f5;
            color: #333;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        /* Login Page */
        .login-container {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background: url('https://images.unsplash.com/photo-1504674900247-0877df9cc836?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80') no-repeat center center;
        }

        .login-box {
            background-color: white;
            padding: 40px;
            border-radius: 10px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            text-align: center;
            width: 400px;
        }

        .login-box h1 {
            color: #e74c3c;
            margin-bottom: 20px;
            font-size: 2.5rem;
        }

        .login-box .logo {
            font-size: 3rem;
            color: #e74c3c;
            margin-bottom: 20px;
        }

        .login-box input {
            width: 100%;
            padding: 12px;
            margin: 10px 0;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 16px;
            transition: border-color 0.3s;
        }

        .login-box input:focus {
            border-color: #e74c3c;
            outline: none;
        }

        .login-box button {
            background-color: #e74c3c;
            color: white;
            border: none;
            padding: 12px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            width: 100%;
            margin-top: 10px;
            transition: background-color 0.3s;
        }

        .login-box button:hover {
            background-color: #c0392b;
        }

        /* Order Type Selection */
        .order-type-container {
            display: none;
            padding: 40px;
            text-align: center;
        }

        .order-type-container h2 {
            color: #e74c3c;
            margin-bottom: 30px;
            font-size: 2rem;
        }

        .order-options {
            display: flex;
            justify-content: center;
            gap: 30px;
            margin-top: 40px;
            flex-wrap: wrap;
        }

        .order-option {
            background-color: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            cursor: pointer;
            transition: transform 0.3s, box-shadow 0.3s;
            width: 250px;
            border: 2px solid transparent;
        }

        .order-option:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.15);
            border-color: #e74c3c;
        }

        .order-option .icon {
            font-size: 3rem;
            color: #e74c3c;
            margin-bottom: 15px;
        }

        .order-option h3 {
            color: #e74c3c;
            margin-bottom: 10px;
            font-size: 1.5rem;
        }

        .order-option p {
            color: #666;
        }

        /* Delivery Address */
        .delivery-address {
            display: none;
            background-color: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            max-width: 600px;
            margin: 40px auto;
        }

        .delivery-address h2 {
            color: #e74c3c;
            margin-bottom: 20px;
            text-align: center;
            font-size: 1.8rem;
        }

        .delivery-address textarea {
            width: 100%;
            padding: 12px;
            border: 1px solid #ddd;
            border-radius: 5px;
            margin-bottom: 20px;
            resize: vertical;
            min-height: 100px;
            font-size: 16px;
            transition: border-color 0.3s;
        }

        .delivery-address textarea:focus {
            border-color: #e74c3c;
            outline: none;
        }

        /* Menu Page */
        .menu-container {
            display: none;
            padding: 20px;
        }

        .menu-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            flex-wrap: wrap;
            gap: 15px;
        }

        .menu-header h2 {
            color: #e74c3c;
            font-size: 1.8rem;
        }

        .back-btn, .view-cart-btn, .checkout-btn {
            background-color: #e74c3c;
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 14px;
            transition: background-color 0.3s;
        }

        .back-btn:hover, .view-cart-btn:hover, .checkout-btn:hover {
            background-color: #c0392b;
        }

        .menu-categories {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
            overflow-x: auto;
            padding-bottom: 10px;
        }

        .category-btn {
            background-color: #f1f1f1;
            border: none;
            padding: 8px 15px;
            border-radius: 20px;
            cursor: pointer;
            font-size: 14px;
            white-space: nowrap;
            transition: all 0.3s;
        }

        .category-btn.active {
            background-color: #e74c3c;
            color: white;
        }

        .category-btn:hover:not(.active) {
            background-color: #ddd;
        }

        .menu-items {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 20px;
        }

        .menu-item {
            background-color: white;
            border-radius: 8px;
            overflow: hidden;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            transition: transform 0.3s, box-shadow 0.3s;
            border: 1px solid #eee;
        }

        .menu-item:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.15);
        }

        .menu-item-icon {
            background-color: #f9f9f9;
            padding: 20px;
            text-align: center;
            font-size: 2.5rem;
            color: #e74c3c;
        }

        .menu-item-details {
            padding: 15px;
        }

        .menu-item-name {
            font-weight: bold;
            margin-bottom: 5px;
            font-size: 16px;
            color: #333;
        }

        .menu-item-desc {
            color: #666;
            font-size: 14px;
            margin-bottom: 10px;
            height: 60px;
            overflow: hidden;
        }

        .menu-item-footer {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .menu-item-price {
            font-weight: bold;
            color: #e74c3c;
            font-size: 16px;
        }

        .add-to-cart {
            background-color: #e74c3c;
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 14px;
            transition: background-color 0.3s;
        }

        .add-to-cart:hover {
            background-color: #c0392b;
        }

        /* Cart Sidebar */
        .cart-sidebar {
            position: fixed;
            top: 0;
            right: -400px;
            width: 400px;
            height: 100%;
            background-color: white;
            box-shadow: -5px 0 15px rgba(0, 0, 0, 0.1);
            transition: right 0.3s;
            z-index: 1000;
            padding: 20px;
            overflow-y: auto;
        }

        .cart-sidebar.active {
            right: 0;
        }

        .cart-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 1px solid #eee;
        }

        .cart-header h3 {
            color: #e74c3c;
            font-size: 1.5rem;
        }

        .close-cart {
            background: none;
            border: none;
            font-size: 24px;
            cursor: pointer;
            color: #666;
            transition: color 0.3s;
        }

        .close-cart:hover {
            color: #e74c3c;
        }

        .cart-items {
            margin-bottom: 20px;
        }

        .cart-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px 0;
            border-bottom: 1px solid #eee;
        }

        .cart-item-info {
            flex: 1;
        }

        .cart-item-name {
            font-weight: bold;
            font-size: 16px;
        }

        .cart-item-price {
            color: #e74c3c;
            font-size: 14px;
        }

        .cart-item-quantity {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .quantity-btn {
            background-color: #f1f1f1;
            border: none;
            width: 25px;
            height: 25px;
            border-radius: 50%;
            cursor: pointer;
            display: flex;
            justify-content: center;
            align-items: center;
            transition: background-color 0.3s;
        }

        .quantity-btn:hover {
            background-color: #ddd;
        }

        .cart-total {
            margin-top: 20px;
            padding-top: 20px;
            border-top: 1px solid #eee;
            text-align: right;
        }

        .cart-total h4 {
            color: #e74c3c;
            font-size: 18px;
        }

        .checkout-btn {
            width: 100%;
            padding: 12px;
            margin-top: 20px;
            font-size: 16px;
        }

        /* Payment Page */
        .payment-container {
            display: none;
            max-width: 800px;
            margin: 0 auto;
            padding: 30px;
            background-color: white;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }

        .payment-container h2 {
            color: #e74c3c;
            margin-bottom: 20px;
            text-align: center;
            font-size: 1.8rem;
        }

        .payment-options {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }

        .payment-option {
            background-color: #f9f9f9;
            border: 1px solid #ddd;
            border-radius: 8px;
            padding: 20px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s;
        }

        .payment-option:hover {
            background-color: #f1f1f1;
        }

        .payment-option.active {
            border-color: #e74c3c;
            background-color: #ffeceb;
        }

        .payment-option .icon {
            font-size: 3rem;
            color: #e74c3c;
            margin-bottom: 10px;
        }

        .payment-option p {
            font-weight: bold;
            color: #333;
        }

        .payment-details {
            display: none;
            margin-top: 30px;
            padding: 20px;
            background-color: #f9f9f9;
            border-radius: 8px;
        }

        .payment-details.active {
            display: block;
        }

        .payment-details h3 {
            margin-bottom: 15px;
            color: #e74c3c;
        }

        .payment-details .icon {
            font-size: 4rem;
            color: #e74c3c;
            margin: 20px 0;
        }

        .bill-splitting {
            margin-top: 30px;
            padding: 20px;
            background-color: #f9f9f9;
            border-radius: 8px;
        }

        .bill-splitting h3 {
            margin-bottom: 15px;
            color: #e74c3c;
        }

        .bill-splitting input {
            width: 100px;
            padding: 8px;
            border: 1px solid #ddd;
            border-radius: 5px;
            margin-right: 10px;
            transition: border-color 0.3s;
        }

        .bill-splitting input:focus {
            border-color: #e74c3c;
            outline: none;
        }

        .discount-input {
            margin-top: 20px;
        }

        .discount-input input {
            width: 100px;
            padding: 8px;
            border: 1px solid #ddd;
            border-radius: 5px;
            margin-right: 10px;
            transition: border-color 0.3s;
        }

        .discount-input input:focus {
            border-color: #e74c3c;
            outline: none;
        }

        .confirm-payment {
            background-color: #e74c3c;
            color: white;
            border: none;
            padding: 12px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            margin-top: 20px;
            width: 100%;
            transition: background-color 0.3s;
        }

        .confirm-payment:hover {
            background-color: #c0392b;
        }

        /* Receipt Page */
        .receipt-container {
            display: none;
            max-width: 600px;
            margin: 0 auto;
            padding: 30px;
            background-color: white;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }

        .receipt-header {
            text-align: center;
            margin-bottom: 30px;
        }

        .receipt-header h2 {
            color: #e74c3c;
            margin-bottom: 10px;
            font-size: 2rem;
        }

        .receipt-header .logo {
            font-size: 3rem;
            color: #e74c3c;
            margin-bottom: 10px;
        }

        .receipt-details {
            margin-bottom: 20px;
        }

        .receipt-details p {
            margin-bottom: 5px;
            font-size: 14px;
        }

        .receipt-items {
            width: 100%;
            border-collapse: collapse;
            margin-bottom: 20px;
        }

        .receipt-items th {
            text-align: left;
            padding: 10px;
            border-bottom: 1px solid #ddd;
            background-color: #f9f9f9;
        }

        .receipt-items td {
            padding: 10px;
            border-bottom: 1px solid #eee;
        }

        .receipt-total {
            text-align: right;
            margin-top: 20px;
            padding-top: 20px;
            border-top: 1px solid #ddd;
        }

        .receipt-total h3 {
            color: #e74c3c;
            font-size: 1.5rem;
        }

        .print-receipt {
            background-color: #e74c3c;
            color: white;
            border: none;
            padding: 12px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            margin-top: 30px;
            width: 100%;
            transition: background-color 0.3s;
        }

        .print-receipt:hover {
            background-color: #c0392b;
        }

        /* Overlay */
        .overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            z-index: 999;
            display: none;
        }

        .overlay.active {
            display: block;
        }

        /* Responsive */
        @media (max-width: 768px) {
            .login-box {
                width: 90%;
                padding: 30px 20px;
            }

            .order-options {
                flex-direction: column;
                align-items: center;
            }

            .payment-options {
                grid-template-columns: 1fr;
            }

            .cart-sidebar {
                width: 90%;
                right: -90%;
            }
            
            .menu-items {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <!-- Login Page -->
    <div class="login-container" id="loginPage">
        <div class="login-box">
            <div class="logo">🍔</div>
            <h1>Meal Minds</h1>
            <input type="text" id="username" placeholder="Username">
            <input type="password" id="password" placeholder="Password">
            <button id="loginBtn">Login</button>
        </div>
    </div>

    <!-- Order Type Selection -->
    <div class="container order-type-container" id="orderTypePage">
        <h2>Select Your Order Type</h2>
        <div class="order-options">
            <div class="order-option" data-type="dine-in">
                <div class="icon">🍽️</div>
                <h3>Dine In</h3>
                <p>Enjoy your meal in our restaurant</p>
            </div>
            <div class="order-option" data-type="take-away">
                <div class="icon">🥡</div>
                <h3>Take Away</h3>
                <p>Pick up your order</p>
            </div>
            <div class="order-option" data-type="delivery">
                <div class="icon">🚚</div>
                <h3>Delivery</h3>
                <p>Get your food delivered</p>
            </div>
        </div>
    </div>

    <!-- Delivery Address -->
    <div class="container delivery-address" id="deliveryAddressPage">
        <h2>Enter Delivery Address</h2>
        <textarea id="address" placeholder="Enter your full address including street, city, and postal code"></textarea>
        <button class="confirm-address-btn">Confirm Address</button>
        <button class="back-btn">Back</button>
    </div>

    <!-- Menu Page -->
    <div class="container menu-container" id="menuPage">
        <div class="menu-header">
            <button class="back-btn">Back</button>
            <h2 id="menuTitle">Our Menu</h2>
            <button class="view-cart-btn">View Cart (<span id="cartCount">0</span>)</button>
        </div>
        
        <div class="menu-categories">
            <button class="category-btn active" data-category="all">All Items</button>
            <button class="category-btn" data-category="main-course">Main Course</button>
            <button class="category-btn" data-category="sides">Sides</button>
            <button class="category-btn" data-category="milkshakes">Milkshakes</button>
            <button class="category-btn" data-category="desserts">Desserts</button>
            <button class="category-btn" data-category="beverages">Beverages</button>
        </div>
        
        <div class="menu-items" id="menuItems">
            <!-- Menu items will be dynamically added here -->
        </div>
    </div>

    <!-- Cart Sidebar -->
    <div class="cart-sidebar" id="cartSidebar">
        <div class="cart-header">
            <h3>Your Cart</h3>
            <button class="close-cart">&times;</button>
        </div>
        <div class="cart-items" id="cartItems">
            <!-- Cart items will be dynamically added here -->
        </div>
        <div class="cart-total">
            <h4>Total: ₹<span id="cartTotal">0.00</span></h4>
        </div>
        <button class="checkout-btn">Proceed to Checkout</button>
    </div>
    <div class="overlay" id="overlay"></div>

    <!-- Payment Page -->
    <div class="container payment-container" id="paymentPage">
        <h2>Payment Options</h2>
        <div class="payment-options">
            <div class="payment-option" data-payment="upi">

                <div class="icon">💳</div>
                <p>UPI Payment</p>
            </div>
            <div class="payment-option" data-payment="cash">
                <div class="icon">💵</div>
                <p>Cash</p>
            </div>
            <div class="payment-option" data-payment="card">
                <div class="icon">💲</div>
                <p>Card</p>
            </div>
        </div>
        
        <div class="payment-details" id="upiPayment">
            <div class="upi-payment">
                <h3>UPI Payment</h3>
                <img src="https://api.qrserver.com/v1/create-qr-code/?size=200x200&data=MealMinds-Payment-UPI" alt="Scan to Pay">
                <p>Amount: ₹<span id="upiAmount">0.00</span></p>
                <p>Or enter UPI ID: mealminds@upi</p>
            </div>
        </div>
        
        <div class="payment-details" id="cashPayment">
            <div class="cash-payment">
                <h3>Pay with Cash</h3>
                <div class="icon">💰</div>
                <p>Please pay ₹<span id="cashAmount">0.00</span> at the counter</p>
            </div>
        </div>
        
        <div class="payment-details" id="cardPayment">
            <div class="card-payment">
                <h3>Pay with Card</h3>
                <div class="icon">💳</div>
                <p>Please insert/swipe your card at the terminal</p>
                <p>Amount: ₹<span id="cardAmount">0.00</span></p>
            </div>
        </div>
        
        <div class="bill-splitting">
            <h3>Bill Splitting</h3>
            <p>Split the bill among <input type="number" id="splitCount" min="1" value="1"> customers</p>
            <p>Each customer pays: ₹<span id="splitAmount">0.00</span></p>
        </div>
        
        <div class="discount-input">
            <h3>Apply Discount</h3>
            <p>Enter discount amount: ₹<input type="number" id="discountAmount" min="0" value="0"></p>
            <p>Total after discount: ₹<span id="discountedTotal">0.00</span></p>
        </div>
        
        <button class="confirm-payment">Confirm Payment</button>
        <button class="back-btn">Back</button>
    </div>

    <!-- Receipt Page -->
    <div class="container receipt-container" id="receiptPage">
        <div class="receipt-header">
            <div class="logo">🍔</div>
            <h2>Meal Minds</h2>
            <p>Order Receipt</p>
            <p id="receiptDate"></p>
            <p id="receiptOrderType"></p>
            <p id="receiptTableNo" style="display: none;">Table No: <span></span></p>
            <p id="receiptAddress" style="display: none;">Delivery Address: <span></span></p>
        </div>
        
        <div class="receipt-details">
            <p>Order ID: <span id="receiptOrderId"></span></p>
            <p>Payment Method: <span id="receiptPaymentMethod"></span></p>
        </div>
        
        <table class="receipt-items">
            <thead>
                <tr>
                    <th>Item</th>
                    <th>Qty</th>
                    <th>Price</th>
                </tr>
            </thead>
            <tbody id="receiptItems">
                <!-- Receipt items will be dynamically added here -->
            </tbody>
        </table>
        
        <div class="receipt-total">
            <p>Subtotal: ₹<span id="receiptSubtotal">0.00</span></p>
            <p>Discount: ₹<span id="receiptDiscount">0.00</span></p>
            <p>Total: ₹<span id="receiptTotal">0.00</span></p>
            <p id="receiptSplit" style="display: none;">Split among <span></span> customers</p>
            <h3>Thank You!</h3>
        </div>
        
        <button class="print-receipt">Print Receipt</button>
        <button class="back-btn">Back to Menu</button>
    </div>

    <script>
        // Global variables
        let currentPage = 'login';
        let orderType = '';
        let cart = [];
        let menuItems = [
            // Main Course
            { id: 1, name: "Classic Burger", price: 129, category: "main-course", icon: "🍔", desc: "Juicy beef patty with lettuce, tomato, and special sauce", nutrition: "Calories: 550, Protein: 25g, Carbs: 45g, Fat: 30g" },
            { id: 2, name: "Cheeseburger", price: 149, category: "main-course", icon: "🧀🍔", desc: "Classic burger with melted cheese", nutrition: "Calories: 600, Protein: 28g, Carbs: 48g, Fat: 35g" },
            { id: 3, name: "Bacon Burger", price: 179, category: "main-course", icon: "🥓🍔", desc: "Burger with crispy bacon strips", nutrition: "Calories: 650, Protein: 30g, Carbs: 50g, Fat: 40g" },
            { id: 4, name: "Veggie Burger", price: 119, category: "main-course", icon: "🥬🍔", desc: "Plant-based patty with fresh veggies", nutrition: "Calories: 400, Protein: 15g, Carbs: 50g, Fat: 15g" },
            { id: 5, name: "Chicken Burger", price: 139, category: "main-course", icon: "🍗🍔", desc: "Grilled chicken breast with mayo", nutrition: "Calories: 450, Protein: 30g, Carbs: 40g, Fat: 20g" },
            { id: 6, name: "Double Cheeseburger", price: 199, category: "main-course", icon: "🧀🍔x2", desc: "Two beef patties with double cheese", nutrition: "Calories: 800, Protein: 45g, Carbs: 50g, Fat: 50g" },
            { id: 7, name: "Fish Burger", price: 159, category: "main-course", icon: "🐟🍔", desc: "Crispy fish fillet with tartar sauce", nutrition: "Calories: 500, Protein: 25g, Carbs: 45g, Fat: 25g" },
            { id: 8, name: "Spicy Chicken Burger", price: 149, category: "main-course", icon: "🌶️🍗🍔", desc: "Spicy fried chicken with jalapeños", nutrition: "Calories: 550, Protein: 28g, Carbs: 45g, Fat: 30g" },
            { id: 9, name: "Mushroom Swiss Burger", price: 169, category: "main-course", icon: "🍄🧀🍔", desc: "Beef patty with mushrooms and Swiss cheese", nutrition: "Calories: 600, Protein: 30g, Carbs: 40g, Fat: 35g" },
            { id: 10, name: "BBQ Burger", price: 159, category: "main-course", icon: "🍖🍔", desc: "Burger with BBQ sauce and onion rings", nutrition: "Calories: 650, Protein: 28g, Carbs: 55g, Fat: 35g" },
            
            // Sides
            { id: 11, name: "French Fries", price: 59, category: "sides", icon: "🍟", desc: "Crispy golden fries with salt", nutrition: "Calories: 300, Protein: 3g, Carbs: 40g, Fat: 15g" },
            { id: 12, name: "Onion Rings", price: 69, category: "sides", icon: "🧅", desc: "Crispy battered onion rings", nutrition: "Calories: 350, Protein: 4g, Carbs: 45g, Fat: 18g" },
            { id: 13, name: "Mozzarella Sticks", price: 89, category: "sides", icon: "🧀", desc: "Breaded mozzarella with marinara", nutrition: "Calories: 400, Protein: 15g, Carbs: 30g, Fat: 25g" },
            { id: 14, name: "Chicken Nuggets (6pc)", price: 99, category: "sides", icon: "🍗", desc: "Crispy chicken nuggets with dip", nutrition: "Calories: 350, Protein: 20g, Carbs: 20g, Fat: 20g" },
            { id: 15, name: "Garlic Bread", price: 49, category: "sides", icon: "🍞", desc: "Toasted bread with garlic butter", nutrition: "Calories: 250, Protein: 5g, Carbs: 30g, Fat: 12g" },
            { id: 16, name: "Sweet Potato Fries", price: 69, category: "sides", icon: "🍠🍟", desc: "Crispy sweet potato fries", nutrition: "Calories: 320, Protein: 3g, Carbs: 50g, Fat: 12g" },
            { id: 17, name: "Cheese Fries", price: 89, category: "sides", icon: "🧀🍟", desc: "Fries topped with melted cheese", nutrition: "Calories: 450, Protein: 10g, Carbs: 40g, Fat: 25g" },
            { id: 18, name: "Loaded Fries", price: 119, category: "sides", icon: "🍟🥓🧀", desc: "Fries with cheese, bacon, and jalapeños", nutrition: "Calories: 600, Protein: 15g, Carbs: 45g, Fat: 40g" },
            { id: 19, name: "Coleslaw", price: 49, category: "sides", icon: "🥗", desc: "Fresh cabbage and carrot salad", nutrition: "Calories: 150, Protein: 1g, Carbs: 15g, Fat: 10g" },
            { id: 20, name: "Mashed Potatoes", price: 59, category: "sides", icon: "🥔", desc: "Creamy mashed potatoes with gravy", nutrition: "Calories: 200, Protein: 4g, Carbs: 30g, Fat: 8g" },
            
            // Milkshakes
            { id: 21, name: "Vanilla Milkshake", price: 99, category: "milkshakes", icon: "🥤", desc: "Creamy vanilla flavored milkshake", nutrition: "Calories: 350, Protein: 8g, Carbs: 50g, Fat: 12g" },
            { id: 22, name: "Chocolate Milkshake", price: 99, category: "milkshakes", icon: "🍫🥤", desc: "Rich chocolate flavored milkshake", nutrition: "Calories: 400, Protein: 8g, Carbs: 55g, Fat: 15g" },
            { id: 23, name: "Strawberry Milkshake", price: 99, category: "milkshakes", icon: "🍓🥤", desc: "Sweet strawberry flavored milkshake", nutrition: "Calories: 380, Protein: 8g, Carbs: 52g, Fat: 13g" },
            { id: 24, name: "Oreo Milkshake", price: 119, category: "milkshakes", icon: "🍪🥤", desc: "Milkshake with crushed Oreo cookies", nutrition: "Calories: 450, Protein: 9g, Carbs: 60g, Fat: 18g" },
            { id: 25, name: "Banana Milkshake", price: 89, category: "milkshakes", icon: "🍌🥤", desc: "Creamy banana flavored milkshake", nutrition: "Calories: 320, Protein: 7g, Carbs: 45g, Fat: 10g" },
            { id: 26, name: "Mango Milkshake", price: 109, category: "milkshakes", icon: "🥭🥤", desc: "Refreshing mango flavored milkshake", nutrition: "Calories: 370, Protein: 7g, Carbs: 55g, Fat: 12g" },
            { id: 27, name: "Peanut Butter Milkshake", price: 129, category: "milkshakes", icon: "🥜🥤", desc: "Rich peanut butter flavored milkshake", nutrition: "Calories: 500, Protein: 12g, Carbs: 45g, Fat: 25g" },
            { id: 28, name: "Caramel Milkshake", price: 119, category: "milkshakes", icon: "🍯🥤", desc: "Sweet caramel flavored milkshake", nutrition: "Calories: 420, Protein: 8g, Carbs: 58g, Fat: 16g" },
            { id: 29, name: "Coffee Milkshake", price: 109, category: "milkshakes", icon: "☕🥤", desc: "Coffee flavored milkshake", nutrition: "Calories: 350, Protein: 8g, Carbs: 45g, Fat: 15g" },
            { id: 30, name: "Cookies & Cream Milkshake", price: 129, category: "milkshakes", icon: "🍪🥛🥤", desc: "Milkshake with cookies and cream", nutrition: "Calories: 480, Protein: 9g, Carbs: 62g, Fat: 20g" },
            
            // Desserts
            { id: 31, name: "Chocolate Brownie", price: 79, category: "desserts", icon: "🍫", desc: "Warm chocolate brownie with fudge", nutrition: "Calories: 350, Protein: 4g, Carbs: 45g, Fat: 18g" },
            { id: 32, name: "Apple Pie", price: 89, category: "desserts", icon: "🍎🥧", desc: "Classic apple pie with cinnamon", nutrition: "Calories: 300, Protein: 2g, Carbs: 50g, Fat: 12g" },
            { id: 33, name: "Ice Cream Sundae", price: 99, category: "desserts", icon: "🍦", desc: "Vanilla ice cream with toppings", nutrition: "Calories: 400, Protein: 5g, Carbs: 55g, Fat: 18g" },
            { id: 34, name: "Chocolate Chip Cookie", price: 49, category: "desserts", icon: "🍪", desc: "Freshly baked chocolate chip cookie", nutrition: "Calories: 200, Protein: 2g, Carbs: 25g, Fat: 10g" },
            { id: 35, name: "Cheesecake Slice", price: 119, category: "desserts", icon: "🍰", desc: "Creamy New York style cheesecake", nutrition: "Calories: 450, Protein: 6g, Carbs: 40g, Fat: 30g" },
            { id: 36, name: "Chocolate Lava Cake", price: 129, category: "desserts", icon: "🍫🍰", desc: "Warm cake with molten chocolate center", nutrition: "Calories: 500, Protein: 6g, Carbs: 60g, Fat: 25g" },
            { id: 37, name: "Tiramisu", price: 139, category: "desserts", icon: "☕🍰", desc: "Classic Italian coffee dessert", nutrition: "Calories: 400, Protein: 6g, Carbs: 45g, Fat: 22g" },
            { id: 38, name: "Strawberry Shortcake", price: 109, category: "desserts", icon: "🍓🍰", desc: "Layered cake with fresh strawberries", nutrition: "Calories: 350, Protein: 4g, Carbs: 50g, Fat: 15g" },
            { id: 39, name: "Banana Split", price: 149, category: "desserts", icon: "🍌🍦", desc: "Banana with ice cream and toppings", nutrition: "Calories: 600, Protein: 8g, Carbs: 80g, Fat: 25g" },
            { id: 40, name: "Cinnamon Roll", price: 79, category: "desserts", icon: "🍥", desc: "Warm roll with cinnamon and icing", nutrition: "Calories: 350, Protein: 5g, Carbs: 55g, Fat: 12g" },
            
            // Beverages
            { id: 41, name: "Coca-Cola", price: 49, category: "beverages", icon: "🥤", desc: "Regular Coca-Cola", nutrition: "Calories: 140, Protein: 0g, Carbs: 39g, Fat: 0g" },
            { id: 42, name: "Diet Coke", price: 49, category: "beverages", icon: "🥤", desc: "Diet Coca-Cola", nutrition: "Calories: 0, Protein: 0g, Carbs: 0g, Fat: 0g" },
            { id: 43, name: "Sprite", price: 49, category: "beverages", icon: "🥤", desc: "Lemon-lime soda", nutrition: "Calories: 140, Protein: 0g, Carbs: 38g, Fat: 0g" },
            { id: 44, name: "Iced Tea", price: 59, category: "beverages", icon: "🍵", desc: "Freshly brewed iced tea", nutrition: "Calories: 90, Protein: 0g, Carbs: 22g, Fat: 0g" },
            { id: 45, name: "Lemonade", price: 59, category: "beverages", icon: "🍋", desc: "Fresh lemonade", nutrition: "Calories: 120, Protein: 0g, Carbs: 30g, Fat: 0g" },
            { id: 46, name: "Orange Juice", price: 69, category: "beverages", icon: "🍊", desc: "Freshly squeezed orange juice", nutrition: "Calories: 110, Protein: 2g, Carbs: 26g, Fat: 0g" },
            { id: 47, name: "Apple Juice", price: 69, category: "beverages", icon: "🍎", desc: "100% pure apple juice", nutrition: "Calories: 120, Protein: 0g, Carbs: 28g, Fat: 0g" },
            { id: 48, name: "Mineral Water", price: 39, category: "beverages", icon: "💧", desc: "Bottled mineral water", nutrition: "Calories: 0, Protein: 0g, Carbs: 0g, Fat: 0g" },
            { id: 49, name: "Coffee", price: 59, category: "beverages", icon: "☕", desc: "Freshly brewed coffee", nutrition: "Calories: 5, Protein: 0g, Carbs: 1g, Fat: 0g" },
            { id: 50, name: "Hot Tea", price: 49, category: "beverages", icon: "🍵", desc: "Hot tea with choice of flavors", nutrition: "Calories: 2, Protein: 0g, Carbs: 0g, Fat: 0g" }
        ];

        // DOM Elements
        const loginPage = document.getElementById('loginPage');
        const orderTypePage = document.getElementById('orderTypePage');
        const deliveryAddressPage = document.getElementById('deliveryAddressPage');
        const menuPage = document.getElementById('menuPage');
        const paymentPage = document.getElementById('paymentPage');
        const receiptPage = document.getElementById('receiptPage');
        
        const loginBtn = document.getElementById('loginBtn');
        const usernameInput = document.getElementById('username');
        const passwordInput = document.getElementById('password');
        
        const orderOptions = document.querySelectorAll('.order-option');
        const confirmAddressBtn = document.querySelector('.confirm-address-btn');
        const addressInput = document.getElementById('address');
        
        const menuItemsContainer = document.getElementById('menuItems');
        const categoryBtns = document.querySelectorAll('.category-btn');
        const cartSidebar = document.getElementById('cartSidebar');
        const cartItemsContainer = document.getElementById('cartItems');
        const cartCount = document.getElementById('cartCount');
        const cartTotal = document.getElementById('cartTotal');
        const viewCartBtn = document.querySelector('.view-cart-btn');
        const closeCartBtn = document.querySelector('.close-cart');
        const checkoutBtn = document.querySelector('.checkout-btn');
        const overlay = document.getElementById('overlay');
        
        const paymentOptions = document.querySelectorAll('.payment-option');
        const upiPayment = document.getElementById('upiPayment');
        const cashPayment = document.getElementById('cashPayment');
        const cardPayment = document.getElementById('cardPayment');
        const upiAmount = document.getElementById('upiAmount');
        const cashAmount = document.getElementById('cashAmount');
        const cardAmount = document.getElementById('cardAmount');
        const splitCount = document.getElementById('splitCount');
        const splitAmount = document.getElementById('splitAmount');
        const discountAmount = document.getElementById('discountAmount');
        const discountedTotal = document.getElementById('discountedTotal');
        const confirmPaymentBtn = document.querySelector('.confirm-payment');
        
        const receiptDate = document.getElementById('receiptDate');
        const receiptOrderType = document.getElementById('receiptOrderType');
        const receiptTableNo = document.getElementById('receiptTableNo');
        const receiptAddress = document.getElementById('receiptAddress');
        const receiptOrderId = document.getElementById('receiptOrderId');
        const receiptPaymentMethod = document.getElementById('receiptPaymentMethod');
        const receiptItemsContainer = document.getElementById('receiptItems');
        const receiptSubtotal = document.getElementById('receiptSubtotal');
        const receiptDiscount = document.getElementById('receiptDiscount');
        const receiptTotal = document.getElementById('receiptTotal');
        const receiptSplit = document.getElementById('receiptSplit');
        const printReceiptBtn = document.querySelector('.print-receipt');
        
        const backBtns = document.querySelectorAll('.back-btn');
        const menuTitle = document.getElementById('menuTitle');

        // Event Listeners
        loginBtn.addEventListener('click', handleLogin);
        orderOptions.forEach(option => option.addEventListener('click', handleOrderType));
        confirmAddressBtn.addEventListener('click', handleConfirmAddress);
        categoryBtns.forEach(btn => btn.addEventListener('click', filterMenu));
        viewCartBtn.addEventListener('click', toggleCart);
        closeCartBtn.addEventListener('click', toggleCart);
        overlay.addEventListener('click', toggleCart);
        checkoutBtn.addEventListener('click', proceedToPayment);
        paymentOptions.forEach(option => option.addEventListener('click', selectPaymentMethod));
        splitCount.addEventListener('input', calculateSplitAmount);
        discountAmount.addEventListener('input', calculateDiscount);
        confirmPaymentBtn.addEventListener('click', confirmPayment);
        printReceiptBtn.addEventListener('click', printReceipt);
        backBtns.forEach(btn => btn.addEventListener('click', goBack));

        // Initialize the app
        function init() {
            showPage(currentPage);
            renderMenuItems();
        }

        // Show the current page and hide others
        function showPage(page) {
            loginPage.style.display = 'none';
            orderTypePage.style.display = 'none';
            deliveryAddressPage.style.display = 'none';
            menuPage.style.display = 'none';
            paymentPage.style.display = 'none';
            receiptPage.style.display = 'none';

            switch(page) {
                case 'login':
                    loginPage.style.display = 'flex';
                    break;
                case 'orderType':
                    orderTypePage.style.display = 'block';
                    break;
                case 'deliveryAddress':
                    deliveryAddressPage.style.display = 'block';
                    break;
                case 'menu':
                    menuPage.style.display = 'block';
                    break;
                case 'payment':
                    paymentPage.style.display = 'block';
                    updatePaymentAmounts();
                    calculateSplitAmount();
                    calculateDiscount();
                    break;
                case 'receipt':
                    receiptPage.style.display = 'block';
                    generateReceipt();
                    break;
            }
        }

        // Handle login
        function handleLogin() {
            const username = usernameInput.value;
            const password = passwordInput.value;
            
            if (username === 'username' && password === 'password') {
                currentPage = 'orderType';
                showPage(currentPage);
            } else {
                alert('Invalid username or password. Please try again.');
            }
        }

        // Handle order type selection
        function handleOrderType(e) {
            orderType = e.currentTarget.dataset.type;
            
            if (orderType === 'delivery') {
                currentPage = 'deliveryAddress';
                showPage(currentPage);
            } else {
                currentPage = 'menu';
                updateMenuTitle();
                showPage(currentPage);
            }
        }

        // Handle confirm address
        function handleConfirmAddress() {
            if (addressInput.value.trim() === '') {
                alert('Please enter a valid delivery address');
                return;
            }
            
            currentPage = 'menu';
            updateMenuTitle();
            showPage(currentPage);
        }

        // Update menu title based on order type
        function updateMenuTitle() {
            let title = 'Our Menu - ';
            
            switch(orderType) {
                case 'dine-in':
                    title += 'Dine In';
                    break;
                case 'take-away':
                    title += 'Take Away';
                    break;
                case 'delivery':
                    title += 'Delivery';
                    break;
            }
            
            menuTitle.textContent = title;
        }

        // Render menu items
        function renderMenuItems(category = 'all') {
            menuItemsContainer.innerHTML = '';
            
            const filteredItems = category === 'all' 
                ? menuItems 
                : menuItems.filter(item => item.category === category);
            
            filteredItems.forEach(item => {
                const itemElement = document.createElement('div');
                itemElement.className = 'menu-item';
                itemElement.innerHTML = `
                    <div class="menu-item-icon">${item.icon}</div>
                    <div class="menu-item-details">
                        <div class="menu-item-name">${item.name} - ₹${item.price}</div>
                        <div class="menu-item-desc">${item.desc}<br>${item.nutrition}</div>
                        <div class="menu-item-footer">
                            <div class="menu-item-price">₹${item.price}</div>
                            <button class="add-to-cart" data-id="${item.id}">Add to Cart</button>
                        </div>
                    </div>
                `;
                
                menuItemsContainer.appendChild(itemElement);
            });
            
            // Add event listeners to add-to-cart buttons
            document.querySelectorAll('.add-to-cart').forEach(btn => {
                btn.addEventListener('click', addToCart);
            });
        }

        // Filter menu by category
        function filterMenu(e) {
            const category = e.currentTarget.dataset.category;
            
            // Update active button
            categoryBtns.forEach(btn => btn.classList.remove('active'));
            e.currentTarget.classList.add('active');
            
            renderMenuItems(category);
        }

        // Add item to cart
        function addToCart(e) {
            const itemId = parseInt(e.currentTarget.dataset.id);
            const item = menuItems.find(item => item.id === itemId);
            
            // Check if item already in cart
            const existingItem = cart.find(cartItem => cartItem.id === itemId);
            
            if (existingItem) {
                existingItem.quantity += 1;
            } else {
                cart.push({
                    ...item,
                    quantity: 1
                });
            }
            
            updateCart();
        }

        // Update cart display
        function updateCart() {
            cartItemsContainer.innerHTML = '';
            
            if (cart.length === 0) {
                cartItemsContainer.innerHTML = '<p>Your cart is empty</p>';
                cartCount.textContent = '0';
                cartTotal.textContent = '0.00';
                return;
            }
            
            let total = 0;
            let itemCount = 0;
            
            cart.forEach(item => {
                const itemElement = document.createElement('div');
                itemElement.className = 'cart-item';
                itemElement.innerHTML = `
                    <div class="cart-item-info">
                        <div class="cart-item-name">${item.name}</div>
                        <div class="cart-item-price">₹${item.price * item.quantity}</div>
                    </div>
                    <div class="cart-item-quantity">
                        <button class="quantity-btn minus" data-id="${item.id}">-</button>
                        <span>${item.quantity}</span>
                        <button class="quantity-btn plus" data-id="${item.id}">+</button>
                    </div>
                `;
                
                cartItemsContainer.appendChild(itemElement);
                total += item.price * item.quantity;
                itemCount += item.quantity;
            });
            
            // Add event listeners to quantity buttons
            document.querySelectorAll('.quantity-btn.minus').forEach(btn => {
                btn.addEventListener('click', decreaseQuantity);
            });
            
            document.querySelectorAll('.quantity-btn.plus').forEach(btn => {
                btn.addEventListener('click', increaseQuantity);
            });
            
            cartCount.textContent = itemCount;
            cartTotal.textContent = total.toFixed(2);
        }

        // Decrease item quantity
        function decreaseQuantity(e) {
            const itemId = parseInt(e.currentTarget.dataset.id);
            const itemIndex = cart.findIndex(item => item.id === itemId);
            
            if (cart[itemIndex].quantity > 1) {
                cart[itemIndex].quantity -= 1;
            } else {
                cart.splice(itemIndex, 1);
            }
            
            updateCart();
        }

        // Increase item quantity
        function increaseQuantity(e) {
            const itemId = parseInt(e.currentTarget.dataset.id);
            const item = cart.find(item => item.id === itemId);
            
            item.quantity += 1;
            updateCart();
        }

        // Toggle cart sidebar
        function toggleCart() {
            cartSidebar.classList.toggle('active');
            overlay.classList.toggle('active');
        }

        // Proceed to payment
        function proceedToPayment() {
            if (cart.length === 0) {
                alert('Your cart is empty. Please add items before proceeding to payment.');
                return;
            }
            
            currentPage = 'payment';
            showPage(currentPage);
            toggleCart();
        }

        // Select payment method
        function selectPaymentMethod(e) {
            const method = e.currentTarget.dataset.payment;
            
            // Update active payment option
            paymentOptions.forEach(option => option.classList.remove('active'));
            e.currentTarget.classList.add('active');
            
            // Show corresponding payment details
            upiPayment.classList.remove('active');
            cashPayment.classList.remove('active');
            cardPayment.classList.remove('active');
            
            switch(method) {
                case 'upi':
                    upiPayment.classList.add('active');
                    break;
                case 'cash':
                    cashPayment.classList.add('active');
                    break;
                case 'card':
                    cardPayment.classList.add('active');
                    break;
            }
        }

        // Update payment amounts
        function updatePaymentAmounts() {
            const total = calculateTotal();
            upiAmount.textContent = total.toFixed(2);
            cashAmount.textContent = total.toFixed(2);
            cardAmount.textContent = total.toFixed(2);
        }

        // Calculate total amount
        function calculateTotal() {
            return cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
        }

        // Calculate split amount
        function calculateSplitAmount() {
            const total = calculateTotal();
            const count = parseInt(splitCount.value) || 1;
            const split = total / count;
            splitAmount.textContent = split.toFixed(2);
        }

        // Calculate discount
        function calculateDiscount() {
            const total = calculateTotal();
            const discount = parseFloat(discountAmount.value) || 0;
            const discounted = Math.max(0, total - discount);
            
            discountedTotal.textContent = discounted.toFixed(2);
        }

        // Confirm payment
        function confirmPayment() {
            if (!document.querySelector('.payment-option.active')) {
                alert('Please select a payment method');
                return;
            }
            
            currentPage = 'receipt';
            showPage(currentPage);
        }

        // Generate receipt
        function generateReceipt() {
            const now = new Date();
            const paymentMethod = document.querySelector('.payment-option.active').textContent.trim();
            const total = calculateTotal();
            const discount = parseFloat(discountAmount.value) || 0;
            const splitCountValue = parseInt(splitCount.value) || 1;
            
            // Set receipt details
            receiptDate.textContent = now.toLocaleString();
            receiptOrderType.textContent = `Order Type: ${getOrderTypeDisplay()}`;
            receiptOrderId.textContent = `#${Math.floor(100000 + Math.random() * 900000)}`;
            receiptPaymentMethod.textContent = paymentMethod;
            
            // Show table number or address based on order type
            if (orderType === 'dine-in') {
                const tableNo = Math.floor(1 + Math.random() * 20);
                receiptTableNo.style.display = 'block';
                receiptTableNo.querySelector('span').textContent = tableNo;
                receiptAddress.style.display = 'none';
            } else if (orderType === 'delivery') {
                receiptTableNo.style.display = 'none';
                receiptAddress.style.display = 'block';
                receiptAddress.querySelector('span').textContent = addressInput.value;
            } else {
                receiptTableNo.style.display = 'none';
                receiptAddress.style.display = 'none';
            }
            
            // Add items to receipt
            receiptItemsContainer.innerHTML = '';
            cart.forEach(item => {
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${item.name}</td>
                    <td>${item.quantity}</td>
                    <td>₹${(item.price * item.quantity).toFixed(2)}</td>
                `;
                receiptItemsContainer.appendChild(row);
            });
            
            // Set totals
            receiptSubtotal.textContent = total.toFixed(2);
            receiptDiscount.textContent = discount.toFixed(2);
            receiptTotal.textContent = (total - discount).toFixed(2);
            
            // Show split if applicable
            if (splitCountValue > 1) {
                receiptSplit.style.display = 'block';
                receiptSplit.querySelector('span').textContent = splitCountValue;
            } else {
                receiptSplit.style.display = 'none';
            }
        }

        // Get order type display text
        function getOrderTypeDisplay() {
            switch(orderType) {
                case 'dine-in': return 'Dine In';
                case 'take-away': return 'Take Away';
                case 'delivery': return 'Delivery';
                default: return '';
            }
        }

        // Print receipt
        function printReceipt() {
            window.print();
        }

        // Go back to previous page
        function goBack() {
            switch(currentPage) {
                case 'orderType':
                    currentPage = 'login';
                    break;
                case 'deliveryAddress':
                    currentPage = 'orderType';
                    break;
                case 'menu':
                    if (orderType === 'delivery') {
                        currentPage = 'deliveryAddress';
                    } else {
                        currentPage = 'orderType';
                    }
                    break;
                case 'payment':
                    currentPage = 'menu';
                    break;
                case 'receipt':
                    currentPage = 'menu';
                    // Clear cart after order is complete
                    cart = [];
                    updateCart();
                    break;
            }
            
            showPage(currentPage);
        }

        // Initialize the app
        init();
    </script>
</body>
</html>
