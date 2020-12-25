# Design Stripe API

## Entity Definitions

### Charge

- id: uuid
- customer_id: uuid
- amount: integer
- currency: string (or currency-code enum)
- status: enum {"succeeded", "pending", "failed"}

### Customer

- id: uuid
- name: string
- address: string
- emails: string
- card: Card

### Card

## EndPoint Definitions

### Charges

CreateCharge
=> Charge
GetCharge
=> Charge
UpdateCharge
=> Charge
ListCharges(offset: integer, limit: integer)
=> Charge[]
CaptureCharge(id: uuid)
=> Charge

### Customers

CreateCustomer(customer: Customer)
=> Customer
GetCustomer(id: uuid)
=> Customer
UpdateCustomer(id: uuid, updateCustomer: Customer)
=> Customer
DeleteCustomer(id: uuid)
=> Customer
ListCustomers(offset: integer, limit: integer)
=> Customer[]
