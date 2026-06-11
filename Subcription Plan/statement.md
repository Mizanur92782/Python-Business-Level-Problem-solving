# Level 1 (Intermediate → Industry-Oriented)

# Problem: Subscription Billing and Invoice Management System

## Business Context

You work for a SaaS company called **CloudTask**, which sells project management software.

Customers subscribe to different plans, and every month the company must generate invoices. The billing department currently does this manually using spreadsheets, which has become error-prone as the customer base grows.

Your task is to build a billing engine that automates subscription charging.

The system should be designed using **Object-Oriented Programming (OOP)** principles and should be maintainable because the business expects new subscription plans and discount rules in the future.

---

# Problem Statement

CloudTask offers three subscription plans:

| Plan | Monthly Fee | Included Users |
|--------|------------|----------------|
| Basic | $20 | 3 |
| Professional | $50 | 10 |
| Enterprise | $100 | 20 |

## Additional User Charges

| Plan | Cost Per Extra User |
|--------|--------------------|
| Basic | $8 |
| Professional | $6 |
| Enterprise | $5 |

---

# Discounts

Customers may receive discounts:

### Startup Discount
- 15% off total bill.

### Nonprofit Discount
- 20% off total bill.

### Discount Rule
- Only one discount can be applied.
- If multiple discounts exist, apply the **highest discount percentage**.

---

# Taxes

Tax rules depend on the customer's country.

| Country | Tax Rate |
|----------|----------|
| USA | 8% |
| UK | 20% |
| Germany | 19% |
| Others | 0% |

### Tax Rule
Tax is calculated **after discounts** are applied.

---

# Invoice Requirements

Each generated invoice must contain:

- Customer Name
- Plan Name
- Base Plan Charge
- Extra User Charge
- Discount Amount
- Tax Amount
- Final Payable Amount

---

# Example Scenarios

## Scenario 1

### Customer Information

| Field | Value |
|---------|---------|
| Name | Alice Inc. |
| Country | USA |
| Plan | Basic |
| Active Users | 5 |
| Discounts | Startup |

### Calculation

```text
Basic Fee = 20

Extra Users = 5 - 3 = 2

Extra Charge = 2 × 8 = 16

Subtotal = 20 + 16 = 36

Discount = 15% of 36 = 5.40

Amount After Discount = 36 - 5.40 = 30.60

Tax = 8% of 30.60 = 2.448

Final Amount = 30.60 + 2.448 = 33.048

Invoice Total = $33.05
```

---

## Scenario 2

### Customer Information

| Field | Value |
|---------|---------|
| Name | Helping Hands |
| Country | UK |
| Plan | Professional |
| Active Users | 8 |
| Discounts | Nonprofit |

### Final Result

```text
Final Amount = $48.00
```

---

## Scenario 3

### Customer Information

| Field | Value |
|---------|---------|
| Name | Mega Corp |
| Country | Germany |
| Plan | Enterprise |
| Active Users | 35 |
| Discounts | None |

### Final Result

```text
Final Amount = $178.50
```

---

# Requirements Analysis

## Core Entities

### 1. Customer
Responsible for storing customer information:

- Name
- Country
- Active Users
- Subscription Plan
- Available Discounts

### 2. Subscription Plan
Responsible for plan configuration:

- Plan Name
- Monthly Fee
- Included Users
- Extra User Cost

### 3. Discount Policy
Responsible for discount calculation:

- Startup Discount
- Nonprofit Discount
- Future Discount Types

### 4. Tax Calculator
Responsible for tax calculation based on country.

### 5. Invoice
Responsible for storing billing results:

- Customer Name
- Plan Name
- Base Charge
- Extra User Charge
- Discount Amount
- Tax Amount
- Final Amount

### 6. Billing Service
Responsible for:

- Generating invoices
- Applying discounts
- Applying taxes
- Coordinating all billing operations

---

# OOP Concepts Expected

## Encapsulation
Hide billing calculations and expose only necessary methods.

Example:

```python
invoice.total_amount()
```

---

## Abstraction
Define common interfaces for:

- Discount policies
- Tax calculation strategies

Example:

```python
class DiscountPolicy(ABC):
    @abstractmethod
    def calculate_discount(self, amount):
        pass
```

---

## Polymorphism
Allow different discount implementations to behave through the same interface.

Example:

```python
StartupDiscount
NonprofitDiscount
```

Both should implement:

```python
calculate_discount()
```

---

## Composition

A `BillingService` should be composed of:

```text
BillingService
 ├── Customer
 ├── SubscriptionPlan
 ├── DiscountPolicy
 ├── TaxCalculator
 └── Invoice
```

This ensures low coupling and high maintainability.

---

# Future Extensibility Goals

The design should allow easy addition of:

- New subscription plans
- New discount policies
- New tax rules
- Promotional campaigns
- Country-specific billing requirements

Without modifying existing core business logic (**Open/Closed Principle**).

---

# Expected Deliverables

1. Design the system using OOP principles.
2. Create appropriate classes and relationships.
3. Generate invoices for customers.
4. Support future extensibility.
5. Write clean, maintainable, and testable code.
6. Follow SOLID design principles where appropriate.
