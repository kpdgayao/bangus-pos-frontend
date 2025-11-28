# Bangus Bowl Co. POS System

A lightweight, modern Point of Sale (POS) web application for Bangus Bowl Co., a Filipino food business specializing in bangus (milkfish) rice bowls and snacks. Built for the Brent Bazaar market with a focus on speed, simplicity, and reliability.

## Features

### Order Management
- **Interactive Menu Selection** - Categorized menu items (Rice Bowls, Snacks, Add-ons, Mix Bowls)
- **Dynamic Shopping Cart** - Real-time cart updates with add/remove/quantity adjustment
- **Price Calculation** - Automatic total calculation with price validation
- **Cart Persistence** - Cart maintains state during active session

### Payment Processing
- **Dual Payment Methods**
  - **Cash**: Amount tendered input with automatic change calculation
  - **GCash**: Reference number tracking for digital payments
- **Real-time Validation** - Prevents submission with invalid payment amounts
- **Order Confirmation** - Modal confirmation before final submission

### User Experience
- **Responsive Design** - Optimized for mobile, tablet, and desktop
- **Recent Orders Drawer** - View last 20 orders with swipe-to-delete functionality
- **Touch & Mouse Support** - Intuitive swipe gestures on all devices
- **Loading States** - Visual feedback during order processing
- **Success/Error Notifications** - Clear feedback for all actions
- **Customer Name Input** - Optional customer identification

### Order History
- **Persistent Storage** - LocalStorage-based order history (last 50 orders)
- **Quick Access** - Recent orders displayed in reverse chronological order
- **Easy Management** - Swipe-to-delete for order removal
- **Cross-session Persistence** - Orders remain after page refresh

## Technologies

This is a **zero-dependency** application built with:

- **HTML5** - Semantic markup
- **CSS3** - Responsive Grid layout with mobile-first design
- **Vanilla JavaScript** - No frameworks or libraries
- **LocalStorage API** - Client-side data persistence
- **Fetch API** - Asynchronous backend communication
- **Azure Static Web Apps** - Production hosting

## Menu Items

Current menu offerings:

**Rice Bowls**
- Bangus Shanghai Bowl (6 pcs) - ₱115
- Bangus Sisig Bowl (without egg) - ₱150
- Breakfast Combo - ₱130
- Lechon Kawali Bowl - ₱130

**Snacks**
- Bangus Shanghai Bites (6 pcs, no rice) - ₱90
- Bangus Shanghai Dozen (12 pcs, no rice) - ₱170

**Add-ons**
- Extra Egg - ₱20
- Extra Shanghai (3 pcs) - ₱45
- Extra Rice - ₱25

**Frozen Products**
- Frozen Bangus Shanghai Pack - ₱250

## Getting Started

### Prerequisites
- A modern web browser (Chrome, Firefox, Safari, Edge)
- A static web server (optional for local development)

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd bangus-pos-frontend
   ```

2. **Open the application**
   - Simply open `index.html` in your web browser, or
   - Serve with a static web server:
   ```bash
   # Using Python 3
   python -m http.server 8000

   # Using Node.js http-server
   npx http-server

   # Using PHP
   php -S localhost:8000
   ```

3. **Access the application**
   - Direct file: `file:///path/to/index.html`
   - Local server: `http://localhost:8000`

### Configuration

The application uses a webhook endpoint for order processing. To configure:

1. Update the webhook URL in `index.html`:
   ```javascript
   const response = await fetch('YOUR_WEBHOOK_URL', {
     method: 'POST',
     headers: { 'Content-Type': 'application/json' },
     body: JSON.stringify(orderData)
   });
   ```

2. The webhook should accept POST requests with the following payload:
   ```json
   {
     "customerName": "John Doe",
     "items": [
       {"name": "Bangus Shanghai Bowl (6 pcs)", "quantity": 2, "price": 115}
     ],
     "paymentMethod": "Cash",
     "amountTendered": 300,
     "change": 70,
     "total": 230,
     "timestamp": 1234567890000
   }
   ```

## Usage

### Processing an Order

1. **Select Items**
   - Choose items from the dropdown menu
   - Click "Add to Cart" for each item
   - Adjust quantities using +/- buttons

2. **Enter Customer Information** (optional)
   - Enter customer name in the input field

3. **Choose Payment Method**
   - Select "Cash" or "GCash"
   - For Cash: Enter amount tendered (change calculated automatically)
   - For GCash: Enter reference number

4. **Submit Order**
   - Click "Submit Order"
   - Review order in confirmation modal
   - Confirm to send to backend
   - Order is saved to recent orders upon success

### Managing Recent Orders

- Click "Recent Orders" to view order history
- Swipe left (mobile) or right (desktop) to delete an order
- Last 20 orders are displayed
- Last 50 orders are stored in browser

## Project Structure

```
bangus-pos-frontend/
├── index.html                    # Main application (all-in-one file)
│   ├── Embedded CSS              # Responsive styles
│   ├── HTML Markup               # Application structure
│   └── JavaScript Logic          # Application functionality
├── staticwebapp.config.json      # Azure Static Web Apps configuration
└── README.md                     # This file
```

## Deployment

### Azure Static Web Apps

This application is configured for Azure Static Web Apps deployment:

1. The `staticwebapp.config.json` enables SPA routing
2. All routes serve `index.html` with a 200 status code
3. No build process required - deploy the repository directly

### Manual Deployment

Upload `index.html` to any static hosting service:
- GitHub Pages
- Netlify
- Vercel
- AWS S3
- Any web server (Apache, Nginx, etc.)

## Development

### Architecture

The application follows a **monolithic single-file architecture**:
- All HTML, CSS, and JavaScript in one file
- No build process or bundling required
- No external dependencies
- Immediate browser compatibility

### Key Components

**Cart Management**
- `addToCart()` - Validates and adds items
- `updateQuantity()` - Adjusts quantities
- `removeFromCart()` - Removes items
- `updateCart()` - Re-renders cart UI

**Payment Processing**
- `togglePaymentFields()` - Switches payment method fields
- `calculateChange()` - Real-time change calculation
- `showConfirmation()` - Displays order confirmation
- `submitOrder()` - Sends order to webhook

**Order History**
- `loadRecentOrders()` - Loads from localStorage
- `saveOrderToHistory()` - Persists completed orders
- `deleteOrder()` - Removes from history

### Responsive Breakpoints

- **Mobile**: Default (max-width: 450px)
- **Tablet/Desktop**: 768px and up
  - Two-column grid layout (60% menu, 40% cart)
  - Sticky cart sidebar
  - 960px maximum width container

## Browser Support

- Chrome/Edge (latest)
- Firefox (latest)
- Safari (latest)
- Mobile browsers (iOS Safari, Chrome Mobile)

## Recent Updates

- Enhanced price validation and change calculation logic
- Added Frozen Bangus Shanghai Pack and Lechon Kawali Bowl to menu
- Improved responsive design for tablet/desktop devices
- Implemented swipe-to-delete functionality for recent orders
- Fixed UI bugs and formatting issues
- Restored loading display logic

## License

[Add your license information here]

## Contact

For questions or support regarding Bangus Bowl Co. POS system, please contact [your contact information].

---

**Built for Bangus Bowl Co. @ Brent Bazaar**
