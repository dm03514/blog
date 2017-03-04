# Encapsulate Conditional Logic

Encapsulating conditional logic is an easily identifiable refactor, which helps with readability, testability, and can help insulate calling code from changes to business requirements.  I frequently observe code with business logic embedded directly into decision logic without the use of abstractions, which leads to unintutive, brittle, difficult to test code because:
- conditionals frequently involve magic numbers
- when business requirements change, decision logic with multiple conditionals has to be updated, resulting in risky changes
- isloating specific logic branches is difficult and often requires data that is not directly related to the logic branch

To illustrate this, suppose we have an online ordering system.  There is a check out routine where the bulk of client ordering logic takes place:


```python
def calculate_order_total(items, user, state, tax_rate, coupon_code):

  if user is None:
     log_exception()
     return
  
  if len(items) == 0:
     log_exception()
     return
     
  # calculate total
  if state == 'district_of_columbia' and len(items) > 10 and set(items) == 1:
     # DC bulk order discount
     total = dc_bulk_order_discount(items)
  else:
     total = sum(i.price for i in items)
     
  if len(items) > 20:
     # heavy shipment surcharge
     total += 20.00
     
  # calculate tax
  if state == 'MD' or state == 'DE':
     if user.location == 'is_city':
        tax_rate += .01 # municiple tax rate surcharge
  elif state == 'CA' or state == 'WA' or state == 'OR':
     # west coast
     tax_rate = '.10' # flat tax
     
  # apply coupon
  if coupon_code is not None and coupon_code == 'BEST10DISC':
      total -= total * 0.10
```

This pattern frequently emerges in the wild, and is very easy to spot.  It manifests as a long chain of conditionals, or embedded conditionals, and usually involves literals and magic numbers.  Since business logic IS centralized here it's obvious that changes to requirements need to occur here.  Because core business logic is centralized here it will often be a very commited to piece of code, and will probably frequently result in bugs.   There are a series of small safe refactorings which can significantly imporove maintainability through increased testability.

The example above is actually no where near as difficult as some of the code seen in the wild.  I've seen a multimillion dollar company have code like:

```python
if e.use_case == 11 and e.sub_type == 1:
   # do something
elif e.use_case == 1 or e.use_case == 2:
    if e.subtype not in [2, 4, 11]:
       # do something
       
    # way more ...
```

# the problem


# the solution
