# ShopPOS - Premium Point of Sale System

A modern, premium-quality POS web application for small retail shops built with Next.js, TypeScript, Supabase, and Material UI.

## Features

### 🛍️ Core Features
- **Point of Sale (POS)**: Fast, cashier-friendly checkout interface
- **Barcode Scanner Support**: Scan products or search manually
- **Product Management**: Full CRUD with categories, pricing, and stock tracking
- **Inventory Management**: Automatic stock deduction on sales, low-stock alerts
- **Customer Management**: Store customer information for credit sales
- **Credit Ledger**: Built-in debt management system with payment tracking
- **Sales History**: View and print receipts, filter by date and payment method
- **Dashboard**: Real-time analytics and business metrics
- **Weighted Products**: Support for kg/liter based products

### 💅 UI/UX Excellence
- Premium Material UI design with custom theme
- Professional data tables with sorting, filtering, pagination
- Responsive layouts for mobile, tablet, and desktop
- Smooth animations and transitions
- Clean, modern aesthetic
- Professional business feel

### 🔐 Security
- Supabase authentication
- Row-level security policies
- Password-protected admin access
- Encrypted credentials

## Tech Stack

- **Frontend**: Next.js 14, React 18, TypeScript
- **UI Framework**: Material UI (MUI) v5
- **Tables**: MUI X Data Grid Community
- **Icons**: Lucide React + MUI Icons
- **Forms**: React Hook Form + Zod
- **State**: Zustand
- **Backend**: Supabase (PostgreSQL)
- **Charts**: Recharts
- **Styling**: Emotion (MUI's default)

## Installation

### Prerequisites
- Node.js 18+
- npm or yarn
- Supabase account (free)

### Setup Steps

1. **Clone the project**
   ```bash
   cd pos-app
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Setup Supabase**
   - Go to [supabase.com](https://supabase.com) and create a free account
   - Create a new project
   - Copy your project URL and anon key

4. **Configure environment variables**
   ```bash
   cp .env.example .env.local
   ```
   
   Edit `.env.local`:
   ```
   NEXT_PUBLIC_SUPABASE_URL=https://your-project.supabase.co
   NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key-here
   ```

5. **Setup database**
   - In Supabase dashboard, go to SQL Editor
   - Create a new query and paste the contents of `database.sql`
   - Run the query to create all tables and sample data

6. **Create a test user in Supabase**
   - Go to Supabase dashboard → Authentication → Users
   - Click "Add user"
   - Email: `test@example.com`
   - Password: `password`

7. **Start development server**
   ```bash
   npm run dev
   ```

8. **Open in browser**
   - Navigate to `http://localhost:3000`
   - Login with `test@example.com` / `password`

## Project Structure

```
pos-app/
├── app/
│   ├── layout.tsx              # Root layout with theme
│   ├── page.tsx                # Redirect to dashboard
│   ├── login/
│   │   └── page.tsx            # Login page
│   ├── dashboard/
│   │   └── page.tsx            # Dashboard with analytics
│   ├── pos/
│   │   └── page.tsx            # Point of sale interface
│   ├── products/
│   │   └── page.tsx            # Product management
│   ├── customers/
│   │   └── page.tsx            # Customer management
│   ├── sales/
│   │   └── page.tsx            # Sales history
│   ├── debtors/
│   │   └── page.tsx            # Debt/credit ledger
│   └── settings/
│       └── page.tsx            # User settings
├── components/
│   └── AdminLayout.tsx         # Sidebar + header layout
├── lib/
│   ├── supabase.ts             # Supabase client & types
│   └── store.ts                # Zustand stores
├── database.sql                # Supabase schema
├── package.json
├── tsconfig.json
├── next.config.js
└── README.md
```

## Key Pages

### Dashboard
- Today's sales and total revenue
- Total products, customers, debtors
- Outstanding debt amount
- Low stock items alert
- Sales trend chart
- Quick action buttons

### Point of Sale
- Barcode scanner input
- Product search with autocomplete
- Add to cart functionality
- Weighted product support (kg/liter)
- Cart management with quantity editing
- Payment method selection (cash, card, credit)
- Discount application
- Stock validation

### Products
- Add, edit, delete products
- Barcode field
- Buying and selling prices
- Stock quantity tracking
- Unit type selection
- Category assignment
- Minimum stock alerts
- Search and filter

### Customers
- Create customer profiles
- Phone number and notes
- Used for credit sales and debt tracking
- Search functionality

### Debtors/Credit Ledger
- View all active debtors
- Customer debt balance
- Total debt and paid amount
- Record payments
- View debt transaction history
- Debt clearing status

### Sales History
- View all sales with details
- Filter by date range
- Filter by payment method
- Filter by credit sales
- Print receipts
- View itemized sale details

## Database Tables

### products
- id, name, barcode, category_id
- buy_price, sell_price
- stock_quantity, unit_type
- image_url, minimum_stock
- created_at, updated_at

### categories
- id, name, created_at

### customers
- id, first_name, last_name
- phone, notes, created_at

### sales
- id, customer_id, total_amount
- discount_amount, payment_method
- is_credit, status, created_at

### sale_items
- id, sale_id, product_id
- quantity, unit_price, total_price
- created_at

### debts
- id, customer_id
- total_debt_amount, paid_amount
- remaining_balance, status
- last_transaction_date, created_at, updated_at

### debt_entries
- id, debt_id, amount
- type (charge/payment), notes
- created_at

## Usage Examples

### Scanning a Product
1. Navigate to POS page
2. Click in the barcode input field
3. Scan product barcode
4. Product automatically adds to cart or shows error

### Processing a Credit Sale
1. Add items to cart
2. Click Checkout
3. Select "Credit (Debt)" as payment method
4. Enter customer name and phone
5. Complete sale
6. Debt is automatically tracked

### Recording a Debt Payment
1. Go to Debtors page
2. Click on a debtor
3. Click "Record Payment"
4. Enter payment amount
5. Payment is applied to debt balance

## Customization

### Changing the Theme
Edit `app/layout.tsx` and modify the `theme` object in `createTheme()`:

```typescript
const theme = createTheme({
  palette: {
    primary: {
      main: '#your-color',
    },
    // ... other colors
  },
});
```

### Adding New Product Fields
1. Update the `Product` type in `lib/supabase.ts`
2. Modify the `products` table in `database.sql`
3. Update the form in `app/products/page.tsx`

## Deployment

### Deploy to Vercel (Recommended)
```bash
npm install -g vercel
vercel
```

### Environment Variables on Vercel
Set in Vercel project settings:
- `NEXT_PUBLIC_SUPABASE_URL`
- `NEXT_PUBLIC_SUPABASE_ANON_KEY`

## Performance Optimizations

- Server-side rendering for SEO
- Image optimization with Next.js Image
- Code splitting and lazy loading
- Memoization for expensive components
- Indexed database queries
- DataGrid pagination for large datasets

## Troubleshooting

### Auth not working
- Check Supabase URL and keys in `.env.local`
- Verify auth is enabled in Supabase dashboard
- Ensure user exists in Supabase

### Products not showing
- Check database.sql was executed
- Verify Supabase RLS policies allow SELECT
- Check browser console for errors

### Cart not saving on refresh
- This is expected - cart uses client-side state
- Consider implementing localStorage for persistence

## Future Enhancements

- Multi-user support with role-based access
- Advanced analytics and reports
- Inventory forecasting
- Supplier management
- Purchase orders
- Stock transfers
- Multi-store support
- Mobile app version
- Dark mode toggle
- Receipt templates customization

## License

MIT

## Support

For issues or questions, check the code comments or review the database schema in `database.sql`.

---

Built with ❤️ for small retail businesses
