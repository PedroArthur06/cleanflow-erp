# CleanFlow ERP | Laundry Management System

![Status](https://img.shields.io/badge/Status-In_Production-success?style=for-the-badge)
![Private Code](https://img.shields.io/badge/Code-Proprietary-red?style=for-the-badge)
![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![Node.js](https://img.shields.io/badge/Node.js-43853D?style=for-the-badge&logo=node.js&logoColor=white)
![Prisma](https://img.shields.io/badge/Prisma-3982CE?style=for-the-badge&logo=Prisma&logoColor=white)

> **A full-stack ERP solution developed for a laundry business to streamline operations, manage finances, and track order lifecycles in real-time.**

---

## 🔒 Project Disclaimer
**This is a proprietary commercial project.**
The source code is protected under NDA (Non-Disclosure Agreement). This repository serves as a **technical case study** documenting the architecture, challenges, and solutions implemented during development.

---

## 💼 Business Context & Problems Solved

The client was managing operations using manual spreadsheets, leading to lost orders and lack of financial clarity.

**My Role:** Lead Full-Stack Engineer.
**The Solution:** I designed and built a centralized web platform that handles:
1.  **Order Lifecycle:** From reception to washing, ironing, and delivery.
2.  **Financial Health:** Automated tracking of daily revenues and operational expenses.
3.  **Customer CRM:** History tracking and loyalty management.

**Impact:**
* Reduced order processing time by **40%**.
* Eliminated financial discrepancies with automated reporting.

---

## 🏗️ Technical Architecture

The system is built as a robust Monolith, prioritizing rapid development without sacrificing code organization.

### Backend (Node.js & TypeScript)
* **Modular Pattern:** Codebase organized by feature domains (`Finance`, `Orders`, `Customers`) rather than technical layers, facilitating maintenance.
* **Database:** PostgreSQL managed via **Prisma ORM** for type-safe database queries and migrations.
* **Authentication:** JWT-based secure access for admin and staff roles.

### Frontend (React & Vite)
* **UI/UX:** Custom dashboard built with **TailwindCSS** for a responsive, mobile-ready experience for staff on the floor.
* **Data Visualization:** Interactive charts for monthly revenue and order volume.
* **Hardware Integration:** Custom implementation for **Thermal Ticket Printing** (`PrintOrder` module) generating optimized receipts for laundry tagging.

---

## 💻 Code Snippets (Abstracted)

### 1. Modular Service Architecture
*Example of how business logic is encapsulated to keep controllers clean.*

```typescript
// src/modules/orders/CreateOrderService.ts
class CreateOrderService {
  constructor(private ordersRepository: IOrdersRepository) {}

  async execute({ customerId, items, discount }: Request): Promise<Order> {
    // 1. Validate Customer
    const customer = await this.customersRepository.findById(customerId);
    if (!customer) throw new AppError("Customer not found");

    // 2. Calculate Total with Discount Logic
    const total = items.reduce((acc, item) => acc + item.price, 0);
    const finalPrice = total - (discount || 0);

    // 3. Persist Order Transactionally
    const order = await this.ordersRepository.create({
      customerId,
      items,
      total: finalPrice,
      status: 'PENDING'
    });

    return order;
  }
}
```

## 🚀 Key Features Implemented

| Feature | Technical Detail |
| :--- | :--- |
| **Financial Dashboard** | Aggregation queries using Prisma to calculate profit margins and monthly growth. |
| **Order Tracking** | State machine logic to handle status transitions (Received -> Washing -> Ready). |
| **Ticket Printing** | CSS `@media print` optimization to generate perfectly sized receipts for thermal printers. |
| **Authentication** | Secure middleware implementation ensuring data privacy. |

---

## 🛠️ Stack & Tools

* **Backend:** Node.js, Express, TypeScript, Zod.
* **Database:** PostgreSQL, Prisma, Supabase.
* **Frontend:** React, Vite, TailwindCSS, Phosphor Icons.
* **DevOps:** Docker (Containerization for easy deployment).

---

## 👨‍💻 Engineer

**Pedro Arthur Rodrigues**
*Software Engineer | Full Stack*
