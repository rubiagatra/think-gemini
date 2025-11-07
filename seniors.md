# Let's think like a Senior Dev

Create a function (in Python) to calculate a discount

---

## Do you write like this? Is there any problem?

```python
def calculate_discount(price, discount):
    return price - (price * discount / 100)


print(calculate_discount(100000, 20))  # Output: 80000.0

```

---

## What are the Problems? 

```python
def calculate_discount(price, discount):
    return price - (price * discount / 100)


print(calculate_discount(100000, 20))  # Output: 80000.0

```

- What if the price is negative?

- Discount more than 100%?

- Discount Negative?

- What if the input not number?

---

## Let's Think Before Coding

### 🧐 **Understand the Problem Completely**

* **What is a discount?** (A percentage off the price)
* **What is the valid range?** (0–100%)
* **What should be returned?** (The final price after the discount)
* **How to handle errors?**


### 🛠️ **Break Down the Complexity**

* **Input:** **Price (IDR)** (float/int), **Discount (%)** (float/int)
* **Validation:**
    * The **Price** must be greater than 0 Rupiah.
    * The **Discount** must be between 0 and 100.
    * Both inputs must be **numeric**.
* **Process:**
    * **Discount Amount** = Price * Discount / 100 
    * **Final_Price** = Price - Discount_Amount
* **Output:** Final_Price (IDR) (float) or raise an error

---

## If You want to write Pseudecode

```python
"""
def calculate_discount(price, discount):
    validate_input(price, discount)
    if valid:
        calculate_discount_amount()
        return result
    else:
        raise error with clear message
"""
```

---

## Better Calculate Discount Function

```python
# discount.py

def calculate_discount(price, discount):
    
    # Validate data types
    if not isinstance(price, (int, float)) or not isinstance(discount, (int, float)):
        raise ValueError("Price and discount must be numbers")
    
    # Validate price value
    if price <= 0:
        raise ValueError("Price must be greater than 0")
    
    # Validate discount value
    if discount < 0 or discount > 100:
        raise ValueError("Discount must be between 0-100")
    
    # Calculate
    discount_amount = price * (discount / 100)
    final_price = price - discount_amount
    
    # Round to avoid floating point issues
    return round(final_price, 2)

```

---

## Write test

```python
# test_discount.py
import pytest
from discount import calculate_discount

class TestCalculateDiscount:
    """Test suite for calculate_discount function"""
    
    # ========== NORMAL CASES ==========
    def test_discount_20_percent(self):
        """Test normal 20% discount"""
        assert calculate_discount(100000, 20) == 80000.0
        
    # ========== BOUNDARY CASES ==========
    def test_discount_0_percent(self):
        """Test 0% discount (price stays the same)"""
        assert calculate_discount(100000, 0) == 100000.0

    # ========== ERROR CASES - INVALID PRICE ==========
    def test_negative_price(self):
        """Test error if price is negative"""
        with pytest.raises(ValueError, match="Price must be greater than 0"):
            calculate_discount(-100000, 20)

```

---

## How to run

```bash
# Install pytest first
uv add init
uv add pytest

# Run all tests
uv run pytest test_discount.py -v
```
