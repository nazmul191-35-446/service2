# 🦅 Birdseye ERP Dashboard - Implementation Plan

---

## 📊 Project Analysis Summary

### Current State (Existing Codebase)
আপনার বর্তমান codebase হলো **Vite + React + TypeScript** based একটি ERP Dashboard prototype:

| Component | Technology |
|-----------|------------|
| **Framework** | Vite (React 19.2.4) |
| **Styling** | Tailwind CSS (CDN based) |
| **Routing** | React Router DOM (HashRouter) |
| **Charts** | Recharts 3.x |
| **Icons** | Lucide React |
| **Language** | TypeScript |

### Key Features Identified (Screenshots + Code Analysis)

#### 1. **Authentication System**
- Login page with email/password
- Demo access button
- Google OAuth integration (UI ready)
- Dark mode support in login

#### 2. **Dashboard Components**
- KPI Cards (Revenue, Expenses, Profit, Users)
- Revenue & Expenses Area Chart
- Expense Breakdown Pie Chart
- Transaction Volume Bar Chart
- Financial Accounts Display
- Recent Transactions Table
- Financial Goals Progress Bars
- Team Members Section

#### 3. **Navigation System**
- Collapsible Sidebar with nested menus
- Top Navigation with Search
- User Profile Dropdown
- Dark/Light Theme Toggle
- Breadcrumb Navigation

#### 4. **ERP Modules (Sidebar Menu)**
- **MAIN**: Dashboard, Analytics, Organization, Projects
- **ERP**: Finance, User Management, Products, Warehouse
- **SYSTEM**: Website Config, POS System, OTP System
- **MARKETING**: Flash Deals, Popups, Campaigns, Activity
- **ACCOUNT**: Profile, Subscription, Settings

---

## 🎯 Target Architecture

```
birdseye-erp/
├── frontend/          # Next.js 14+ App Router
│   └── (Full Dashboard UI)
│
└── backend/           # Node.js + Express API
    └── (RESTful API + Database)
```

---

# 📋 Phase 1: Frontend Development (Next.js)

## 1.1 Project Setup
```bash
# Commands to run:
npx create-next-app@latest frontend --typescript --tailwind --eslint --app --src-dir
cd frontend
npm install lucide-react recharts axios zustand
npm install @tanstack/react-query
```

### Folder Structure (Next.js App Router)
```
frontend/
├── src/
│   ├── app/
│   │   ├── (auth)/
│   │   │   ├── login/
│   │   │   │   └── page.tsx
│   │   │   ├── register/
│   │   │   │   └── page.tsx
│   │   │   └── layout.tsx
│   │   │
│   │   ├── (dashboard)/
│   │   │   ├── dashboard/
│   │   │   │   └── page.tsx
│   │   │   ├── analytics/
│   │   │   │   └── page.tsx
│   │   │   ├── organization/
│   │   │   │   └── page.tsx
│   │   │   ├── projects/
│   │   │   │   └── page.tsx
│   │   │   ├── finance/
│   │   │   │   ├── page.tsx
│   │   │   │   ├── transactions/
│   │   │   │   │   └── page.tsx
│   │   │   │   └── profit-loss/
│   │   │   │       └── page.tsx
│   │   │   ├── users/
│   │   │   │   ├── page.tsx
│   │   │   │   ├── roles/
│   │   │   │   │   └── page.tsx
│   │   │   │   └── sessions/
│   │   │   │       └── page.tsx
│   │   │   ├── products/
│   │   │   │   ├── page.tsx
│   │   │   │   ├── brands/
│   │   │   │   │   └── page.tsx
│   │   │   │   ├── categories/
│   │   │   │   │   └── page.tsx
│   │   │   │   └── [id]/
│   │   │   │       └── page.tsx
│   │   │   ├── warehouse/
│   │   │   │   ├── page.tsx
│   │   │   │   ├── vendors/
│   │   │   │   │   └── page.tsx
│   │   │   │   ├── purchase/
│   │   │   │   │   └── page.tsx
│   │   │   │   └── stock/
│   │   │   │       └── page.tsx
│   │   │   ├── settings/
│   │   │   │   └── page.tsx
│   │   │   └── layout.tsx
│   │   │
│   │   ├── layout.tsx
│   │   ├── globals.css
│   │   └── page.tsx (redirect to /dashboard)
│   │
│   ├── components/
│   │   ├── ui/
│   │   │   ├── Button.tsx
│   │   │   ├── Card.tsx
│   │   │   ├── Input.tsx
│   │   │   ├── Modal.tsx
│   │   │   ├── Table.tsx
│   │   │   ├── Dropdown.tsx
│   │   │   ├── Badge.tsx
│   │   │   ├── Avatar.tsx
│   │   │   ├── Progress.tsx
│   │   │   ├── Skeleton.tsx
│   │   │   └── Toast.tsx
│   │   │
│   │   ├── layout/
│   │   │   ├── Sidebar.tsx
│   │   │   ├── TopNav.tsx
│   │   │   ├── Breadcrumb.tsx
│   │   │   ├── DashboardLayout.tsx
│   │   │   └── AuthLayout.tsx
│   │   │
│   │   ├── charts/
│   │   │   ├── AreaChartCard.tsx
│   │   │   ├── PieChartCard.tsx
│   │   │   ├── BarChartCard.tsx
│   │   │   └── CustomTooltip.tsx
│   │   │
│   │   ├── dashboard/
│   │   │   ├── KPICard.tsx
│   │   │   ├── AccountsPanel.tsx
│   │   │   ├── TransactionsTable.tsx
│   │   │   ├── GoalsProgress.tsx
│   │   │   └── TeamMembers.tsx
│   │   │
│   │   ├── auth/
│   │   │   ├── LoginForm.tsx
│   │   │   └── SocialLogin.tsx
│   │   │
│   │   └── common/
│   │       ├── ThemeToggle.tsx
│   │       └── UserMenu.tsx
│   │
│   ├── lib/
│   │   ├── api.ts
│   │   ├── utils.ts
│   │   └── auth.ts
│   │
│   ├── hooks/
│   │   ├── useAuth.ts
│   │   ├── useTheme.ts
│   │   ├── useSidebar.ts
│   │   └── useApi.ts
│   │
│   ├── store/
│   │   ├── authStore.ts
│   │   ├── uiStore.ts
│   │   └── index.ts
│   │
│   ├── types/
│   │   ├── index.ts
│   │   ├── user.ts
│   │   ├── finance.ts
│   │   ├── product.ts
│   │   └── api.ts
│   │
│   └── constants/
│       ├── menu.ts
│       ├── mockData.ts
│       └── theme.ts
│
├── public/
│   ├── logo.svg
│   └── images/
│
├── tailwind.config.ts
├── next.config.js
└── package.json
```

---

## 1.2 Design System Setup (tailwind.config.ts)

```typescript
import type { Config } from 'tailwindcss'

const config: Config = {
  darkMode: 'class',
  content: [
    './src/pages/**/*.{js,ts,jsx,tsx,mdx}',
    './src/components/**/*.{js,ts,jsx,tsx,mdx}',
    './src/app/**/*.{js,ts,jsx,tsx,mdx}',
  ],
  theme: {
    container: {
      center: true,
      padding: '1.5rem',
      screens: {
        '2xl': '1400px',
      },
    },
    extend: {
      colors: {
        brand: {
          DEFAULT: '#C75B12',
          hover: '#A94B0F',
          light: '#E7B089',
          soft: '#F7E6D8',
        },
        surface: {
          page: '#FAF7F2',
          card: '#FFF9F1',
          sidebar: '#F3E6D8',
          hover: '#EAD3BE',
          border: '#E6DDD4',
        },
        dark: {
          page: '#151312',
          card: '#1F1B18',
          sidebar: '#1B1715',
          border: '#3A2E25',
        },
        ink: {
          heading: '#2E1F14',
          body: '#5F5147',
          muted: '#8A7B6E',
        },
        success: {
          DEFAULT: '#1F9D55',
          bg: '#E6F6ED',
        },
        danger: {
          DEFAULT: '#D64545',
          bg: '#FBEAEA',
        },
        warning: {
          DEFAULT: '#D6A100',
          bg: '#FFF4CC',
        },
        info: {
          DEFAULT: '#4B6CB7',
          bg: '#EAF0FA',
        },
      },
      fontFamily: {
        sans: ['Inter', 'system-ui', 'sans-serif'],
      },
      boxShadow: {
        card: '0 6px 20px rgba(46, 31, 20, 0.08)',
        soft: '0 2px 10px rgba(46, 31, 20, 0.06)',
        hover: '0 8px 28px rgba(46, 31, 20, 0.12)',
      },
      keyframes: {
        fadeIn: {
          '0%': { opacity: '0', transform: 'translateY(6px)' },
          '100%': { opacity: '1', transform: 'translateY(0)' },
        },
        slideIn: {
          '0%': { transform: 'translateX(-100%)' },
          '100%': { transform: 'translateX(0)' },
        },
      },
      animation: {
        fade: 'fadeIn 0.3s ease-out',
        'slide-in': 'slideIn 0.3s ease-out',
      },
    },
  },
  plugins: [],
}
export default config
```

---

## 1.3 Component Migration Priority

### 🔴 Priority 1 (Week 1) - Core Layout
| Component | Source File | Status |
|-----------|-------------|--------|
| Sidebar | `components/Sidebar.tsx` | Migrate |
| TopNav | `components/TopNav.tsx` | Migrate |
| DashboardLayout | `App.tsx` | Create New |
| ThemeProvider | New | Create |
| AuthProvider | New | Create |

### 🟠 Priority 2 (Week 1-2) - Auth
| Component | Source File | Status |
|-----------|-------------|--------|
| Login Page | `components/Login.tsx` | Migrate + Enhance |
| Protected Routes | New | Create |
| Auth Store (Zustand) | New | Create |

### 🟡 Priority 3 (Week 2) - Dashboard
| Component | Source File | Status |
|-----------|-------------|--------|
| KPI Cards | `Dashboard.tsx` | Extract |
| Revenue Chart | `Dashboard.tsx` | Extract + Component |
| Expense Pie | `Dashboard.tsx` | Extract + Component |
| Transactions | `Dashboard.tsx` | Extract + Component |
| Accounts Panel | `Dashboard.tsx` | Extract + Component |
| Goals Progress | `Dashboard.tsx` | Extract + Component |

### 🟢 Priority 4 (Week 3-4) - Module Pages
| Page | Route | Status |
|------|-------|--------|
| Analytics | `/analytics` | Create |
| Organization | `/organization` | Create |
| Projects | `/projects` | Create |
| Finance Overview | `/finance` | Create |
| Transactions | `/finance/transactions` | Create |
| User List | `/users` | Create |
| Products | `/products` | Create |
| Warehouse | `/warehouse` | Create |

---

## 1.4 API Integration Setup

### lib/api.ts
```typescript
import axios from 'axios';

const API_BASE_URL = process.env.NEXT_PUBLIC_API_URL || 'http://localhost:5000/api';

export const api = axios.create({
  baseURL: API_BASE_URL,
  headers: {
    'Content-Type': 'application/json',
  },
  withCredentials: true,
});

// Request interceptor for auth token
api.interceptors.request.use((config) => {
  const token = localStorage.getItem('accessToken');
  if (token) {
    config.headers.Authorization = `Bearer ${token}`;
  }
  return config;
});

// Response interceptor for error handling
api.interceptors.response.use(
  (response) => response,
  async (error) => {
    if (error.response?.status === 401) {
      // Handle token refresh or logout
      localStorage.removeItem('accessToken');
      window.location.href = '/login';
    }
    return Promise.reject(error);
  }
);
```

---

# 📋 Phase 2: Backend Development (Node.js)

## 2.1 Backend Tech Stack

| Layer | Technology |
|-------|------------|
| **Runtime** | Node.js |
| **Framework** | Express.js |
| **Database** | PostgreSQL (recommended) or MongoDB |
| **ORM** | Prisma (for PostgreSQL) or Mongoose |
| **Authentication** | JWT + Refresh Tokens |
| **Validation** | Zod or Joi |
| **API Docs** | Swagger/OpenAPI |

## 2.2 Project Setup
```bash
mkdir backend && cd backend
npm init -y
npm install express cors helmet morgan dotenv bcryptjs jsonwebtoken
npm install @prisma/client
npm install -D typescript ts-node nodemon @types/node @types/express prisma
npx tsc --init
npx prisma init
```

### Folder Structure (Backend)
```
backend/
├── src/
│   ├── app.ts                 # Express app setup
│   ├── server.ts              # Entry point
│   │
│   ├── config/
│   │   ├── database.ts
│   │   ├── jwt.ts
│   │   └── cors.ts
│   │
│   ├── routes/
│   │   ├── index.ts
│   │   ├── auth.routes.ts
│   │   ├── user.routes.ts
│   │   ├── finance.routes.ts
│   │   ├── product.routes.ts
│   │   ├── warehouse.routes.ts
│   │   └── dashboard.routes.ts
│   │
│   ├── controllers/
│   │   ├── auth.controller.ts
│   │   ├── user.controller.ts
│   │   ├── finance.controller.ts
│   │   ├── product.controller.ts
│   │   ├── warehouse.controller.ts
│   │   └── dashboard.controller.ts
│   │
│   ├── services/
│   │   ├── auth.service.ts
│   │   ├── user.service.ts
│   │   ├── finance.service.ts
│   │   ├── product.service.ts
│   │   └── analytics.service.ts
│   │
│   ├── middlewares/
│   │   ├── auth.middleware.ts
│   │   ├── validation.middleware.ts
│   │   ├── error.middleware.ts
│   │   └── role.middleware.ts
│   │
│   ├── utils/
│   │   ├── ApiError.ts
│   │   ├── ApiResponse.ts
│   │   ├── asyncHandler.ts
│   │   └── helpers.ts
│   │
│   ├── validations/
│   │   ├── auth.validation.ts
│   │   ├── user.validation.ts
│   │   └── product.validation.ts
│   │
│   └── types/
│       ├── express.d.ts
│       └── index.ts
│
├── prisma/
│   ├── schema.prisma
│   └── seed.ts
│
├── .env
├── .env.example
├── tsconfig.json
├── package.json
└── nodemon.json
```

---

## 2.3 Database Schema (Prisma)

```prisma
// prisma/schema.prisma

generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

// ============ AUTH & USERS ============
model User {
  id            String    @id @default(uuid())
  email         String    @unique
  password      String
  name          String
  avatar        String?
  role          Role      @default(USER)
  isActive      Boolean   @default(true)
  createdAt     DateTime  @default(now())
  updatedAt     DateTime  @updatedAt
  
  sessions      Session[]
  transactions  Transaction[]
  activityLogs  ActivityLog[]
  
  organizationId String?
  organization   Organization? @relation(fields: [organizationId], references: [id])
}

enum Role {
  ADMIN
  MANAGER
  USER
  VIEWER
}

model Session {
  id          String   @id @default(uuid())
  userId      String
  user        User     @relation(fields: [userId], references: [id])
  token       String   @unique
  expiresAt   DateTime
  createdAt   DateTime @default(now())
  userAgent   String?
  ipAddress   String?
}

// ============ ORGANIZATION ============
model Organization {
  id          String   @id @default(uuid())
  name        String
  logo        String?
  createdAt   DateTime @default(now())
  updatedAt   DateTime @updatedAt
  
  users       User[]
  products    Product[]
  warehouses  Warehouse[]
  accounts    FinancialAccount[]
}

// ============ FINANCE ============
model FinancialAccount {
  id              String       @id @default(uuid())
  name            String
  balance         Float        @default(0)
  accountNumber   String
  type            AccountType
  organizationId  String
  organization    Organization @relation(fields: [organizationId], references: [id])
  transactions    Transaction[]
  createdAt       DateTime     @default(now())
  updatedAt       DateTime     @updatedAt
}

enum AccountType {
  SAVINGS
  CHECKING
  CREDIT
  INVESTMENT
}

model Transaction {
  id          String       @id @default(uuid())
  title       String
  amount      Float
  type        TransactionType
  category    String
  date        DateTime
  accountId   String
  account     FinancialAccount @relation(fields: [accountId], references: [id])
  userId      String
  user        User         @relation(fields: [userId], references: [id])
  createdAt   DateTime     @default(now())
}

enum TransactionType {
  INCOME
  EXPENSE
  TRANSFER
}

model FinancialGoal {
  id          String   @id @default(uuid())
  title       String
  current     Float
  target      Float
  deadline    DateTime
  color       String?
  createdAt   DateTime @default(now())
  updatedAt   DateTime @updatedAt
}

// ============ PRODUCTS ============
model Product {
  id              String    @id @default(uuid())
  name            String
  sku             String    @unique
  description     String?
  price           Float
  costPrice       Float?
  quantity        Int       @default(0)
  minStock        Int       @default(10)
  status          ProductStatus @default(ACTIVE)
  
  brandId         String?
  brand           Brand?    @relation(fields: [brandId], references: [id])
  
  categoryId      String?
  category        Category? @relation(fields: [categoryId], references: [id])
  
  organizationId  String
  organization    Organization @relation(fields: [organizationId], references: [id])
  
  images          ProductImage[]
  stockEntries    StockEntry[]
  
  createdAt       DateTime  @default(now())
  updatedAt       DateTime  @updatedAt
}

enum ProductStatus {
  ACTIVE
  INACTIVE
  OUT_OF_STOCK
  DISCONTINUED
}

model Brand {
  id          String    @id @default(uuid())
  name        String
  logo        String?
  products    Product[]
  createdAt   DateTime  @default(now())
}

model Category {
  id          String     @id @default(uuid())
  name        String
  slug        String     @unique
  parentId    String?
  parent      Category?  @relation("CategoryToCategory", fields: [parentId], references: [id])
  children    Category[] @relation("CategoryToCategory")
  products    Product[]
  createdAt   DateTime   @default(now())
}

model ProductImage {
  id          String   @id @default(uuid())
  url         String
  alt         String?
  isPrimary   Boolean  @default(false)
  productId   String
  product     Product  @relation(fields: [productId], references: [id])
}

// ============ WAREHOUSE ============
model Warehouse {
  id              String   @id @default(uuid())
  name            String
  location        String?
  address         String?
  organizationId  String
  organization    Organization @relation(fields: [organizationId], references: [id])
  stockEntries    StockEntry[]
  createdAt       DateTime @default(now())
}

model Vendor {
  id          String     @id @default(uuid())
  name        String
  email       String?
  phone       String?
  address     String?
  purchases   Purchase[]
  createdAt   DateTime   @default(now())
}

model Purchase {
  id          String        @id @default(uuid())
  vendorId    String
  vendor      Vendor        @relation(fields: [vendorId], references: [id])
  totalAmount Float
  status      PurchaseStatus @default(PENDING)
  items       PurchaseItem[]
  createdAt   DateTime      @default(now())
  approvedAt  DateTime?
}

enum PurchaseStatus {
  PENDING
  APPROVED
  RECEIVED
  CANCELLED
}

model PurchaseItem {
  id          String   @id @default(uuid())
  purchaseId  String
  purchase    Purchase @relation(fields: [purchaseId], references: [id])
  productName String
  quantity    Int
  unitPrice   Float
}

model StockEntry {
  id          String    @id @default(uuid())
  productId   String
  product     Product   @relation(fields: [productId], references: [id])
  warehouseId String
  warehouse   Warehouse @relation(fields: [warehouseId], references: [id])
  quantity    Int
  type        StockType
  note        String?
  createdAt   DateTime  @default(now())
}

enum StockType {
  IN
  OUT
  ADJUSTMENT
  TRANSFER
}

// ============ ACTIVITY ============
model ActivityLog {
  id          String   @id @default(uuid())
  userId      String
  user        User     @relation(fields: [userId], references: [id])
  action      String
  entity      String
  entityId    String?
  metadata    Json?
  createdAt   DateTime @default(now())
}
```

---

## 2.4 API Endpoints

### Authentication
```
POST   /api/auth/register         # Register new user
POST   /api/auth/login            # Login
POST   /api/auth/logout           # Logout
POST   /api/auth/refresh          # Refresh token
POST   /api/auth/forgot-password  # Request password reset
POST   /api/auth/reset-password   # Reset password
GET    /api/auth/me               # Get current user
```

### Dashboard
```
GET    /api/dashboard/kpis        # Get KPI data
GET    /api/dashboard/revenue     # Revenue chart data
GET    /api/dashboard/expenses    # Expense breakdown
GET    /api/dashboard/transactions # Recent transactions
GET    /api/dashboard/goals       # Financial goals
```

### Users
```
GET    /api/users                 # List users (paginated)
GET    /api/users/:id             # Get user
POST   /api/users                 # Create user
PUT    /api/users/:id             # Update user
DELETE /api/users/:id             # Delete user
GET    /api/users/:id/sessions    # User sessions
```

### Finance
```
GET    /api/accounts              # List accounts
GET    /api/accounts/:id          # Get account
POST   /api/accounts              # Create account
PUT    /api/accounts/:id          # Update account

GET    /api/transactions          # List transactions
POST   /api/transactions          # Create transaction
GET    /api/transactions/summary  # Transaction summary
```

### Products
```
GET    /api/products              # List products
GET    /api/products/:id          # Get product
POST   /api/products              # Create product
PUT    /api/products/:id          # Update product
DELETE /api/products/:id          # Delete product

GET    /api/brands                # List brands
GET    /api/categories            # List categories
```

### Warehouse
```
GET    /api/warehouses            # List warehouses
GET    /api/warehouses/:id/stock  # Warehouse stock
GET    /api/vendors               # List vendors
GET    /api/purchases             # List purchases
POST   /api/purchases             # Create purchase
PUT    /api/purchases/:id/approve # Approve purchase
```

---

# 📅 Implementation Timeline

## Week 1: Foundation
- [x] Analyze existing codebase ✅
- [ ] Setup Next.js project with TypeScript
- [ ] Configure Tailwind with custom theme
- [ ] Create basic folder structure
- [ ] Migrate Sidebar component
- [ ] Migrate TopNav component
- [ ] Create DashboardLayout
- [ ] Setup Theme Provider (dark mode)

## Week 2: Auth & Dashboard
- [ ] Create Login page
- [ ] Setup Zustand auth store
- [ ] Create protected route middleware
- [ ] Migrate Dashboard page
- [ ] Extract KPI Card component
- [ ] Extract Chart components
- [ ] Create mock data hooks

## Week 3: Module Pages
- [ ] Create Analytics page
- [ ] Create Users page with table
- [ ] Create Products listing page
- [ ] Create Finance overview page
- [ ] Add pagination & search
- [ ] Add form modals for CRUD

## Week 4: Backend Foundation
- [ ] Setup Node.js + Express
- [ ] Configure Prisma with PostgreSQL
- [ ] Create database schema
- [ ] Implement auth endpoints
- [ ] Add JWT middleware
- [ ] Create user CRUD

## Week 5: Backend Complete
- [ ] Dashboard API endpoints
- [ ] Finance module APIs
- [ ] Product module APIs
- [ ] Warehouse module APIs
- [ ] Add validation & error handling
- [ ] API documentation (Swagger)

## Week 6: Integration & Polish
- [ ] Connect frontend to backend
- [ ] Implement real authentication
- [ ] Add loading states & skeletons
- [ ] Error handling & toasts
- [ ] Performance optimization
- [ ] Testing & bug fixes

---

# 🚀 Quick Start Commands

### Frontend (Next.js)
```bash
# Step 1: Create project
npx create-next-app@latest frontend --typescript --tailwind --eslint --app --src-dir

# Step 2: Install dependencies
cd frontend
npm install lucide-react recharts axios zustand @tanstack/react-query

# Step 3: Start development
npm run dev
```

### Backend (Node.js)
```bash
# Step 1: Create project
mkdir backend && cd backend
npm init -y

# Step 2: Install dependencies
npm install express cors helmet dotenv bcryptjs jsonwebtoken
npm install @prisma/client zod
npm install -D typescript ts-node nodemon @types/node @types/express prisma

# Step 3: Initialize TypeScript & Prisma
npx tsc --init
npx prisma init

# Step 4: Start development
npm run dev
```

---

# 📝 Notes for Migration

### Code That Can Be Directly Reused:
1. **Tailwind Config** - Custom colors, shadows, animations from `index.html`
2. **Types** - All interfaces from `types.ts`
3. **Constants** - Menu structure, KPI data from `constants.tsx`
4. **Charts** - Custom tooltip and chart configurations

### Changes Required:
1. **Routing** - HashRouter → Next.js App Router
2. **Imports** - Vite imports → Next.js imports
3. **Image** - Regular img → Next.js Image component
4. **Link** - React Router Link → Next.js Link
5. **API Calls** - Mock data → Real API integration

---

# ✅ Checklist

## Before Starting:
- [ ] Install Node.js (v18+)
- [ ] Install PostgreSQL (or use Docker)
- [ ] Setup VS Code with extensions
- [ ] Clone/create project directories

## Environment Variables:

### Frontend (.env.local)
```env
NEXT_PUBLIC_API_URL=http://localhost:5000/api
```

### Backend (.env)
```env
NODE_ENV=development
PORT=5000
DATABASE_URL=postgresql://user:password@localhost:5432/birdseye?schema=public
JWT_SECRET=your-super-secret-jwt-key
JWT_EXPIRES_IN=7d
REFRESH_TOKEN_SECRET=your-refresh-token-secret
REFRESH_TOKEN_EXPIRES_IN=30d
```

---

**Ready to start? Just say "start frontend" or "start backend" and I'll begin the implementation! 🚀**
