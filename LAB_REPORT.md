# SE3006 - Software Architecture

## Lab 01 – Layered Architecture (Pure Java)

### Overview

In this lab, a simple layered architecture was implemented using pure Java without any frameworks. The system was divided into three layers:

- Presentation (Controller)
    
- Business (Service)
    
- Persistence (Repository)
    

Strict layering was followed, meaning each layer only communicates with the layer directly below it.

---

### What I Implemented

**Persistence Layer**

- Created `ProductRepository`
    
- Used a `HashMap<Long, Product>` as in-memory storage
    
- Implemented:
    
    - `findById(Long id)`
        
    - `save(Product product)`
        

**Business Layer**

- Created `OrderService`
    
- Injected `ProductRepository` using constructor
    
- Implemented `placeOrder(productId, quantity)`:
    
    - Find product
        
    - Check stock
        
    - Throw exception if insufficient
        
    - Reduce stock
        
    - Save updated product
        

**Presentation Layer**

- Created `OrderController`
    
- Injected `OrderService`
    
- Implemented `handleUserRequest(...)`
    
- Used try-catch for error handling
    
- Printed success / error messages
    

**Main (Manual Wiring)**  
Objects were created from bottom to top:

```powershell
ProductRepository → OrderService → OrderController
```

Dependency injection was done manually.

---

### Test Scenario

The system was tested by calling:

```java
orderController.handleUserRequest(...)
```

---

### Results

Console output after running:

```powershell
--- Test Scenarios ---

New Request: Product ID=1, Quantity=2
Order Confirmed

New Request: Product ID=1, Quantity=10
ERROR: Insufficient stock for product: MacBook Pro

New Request: Product ID=2, Quantity=5
Order Confirmed

New Request: Product ID=4, Quantity=10
Order Confirmed
```

---

### Notes

- Layer separation worked correctly
    
- Business rules were enforced in service layer
    
- Exceptions were handled in controller
    
- Manual dependency injection was successful
    
- Strict layering rule was preserved
    

---

### Conclusion

The lab successfully demonstrated layered architecture with manual dependency injection. Each layer had a clear responsibility and communicated only with the allowed layer. The test scenarios confirmed that stock validation and order handling worked as expected.