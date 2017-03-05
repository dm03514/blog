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

Refactoring to significantly increase comprehensibility, safety and support testability is pretty safe.  The conditional logic should be encapsulated in a method and extracted.  Martin Fowler identifies this pattern in "Refactoring" as ["Extract Method"](https://refactoring.com/catalog/extractMethod.html). This can be done by copying a conditional pasting it in a method describing what the conditional does, and parameterizing the method to take the required values. 

To illustrate using the first example above:

`state == 'district_of_columbia' and len(items) > 10 and set(items) == 1`

Would become:

```python
def is_dc_bulk_order(state, items):
  return state == 'district_of_columbia' and len(items) > 10 and set(items) == 1
```

And then the conditional becomes 

```python
if is_dc_bulk_order(state, item):
  total = dc_bulk_order_discount(items)
```

Since the method name describes the conditional, there is no longer any need for comments, removing the maintanence required to keep comments from becoming stale.

Applying this to every single conditional creates a code block which reads like a series of comments, and isolates magic numbers to only the routines that have to worry about it.  Additionally, when business requirements change, less code has to be reasoned about and verified to confidently make a change.

Take the follow example:

```python
if state == 'CA' or state == 'WA' or state == 'OR':
```

The above represents west coast states.  When business requirements change to consider Alaska as a west coast state the `calculate_order_total` method will need to be changed, and retested.  If the logic is encapsulated as:

```python
def is_west_coast_state(state):
  return state == 'CA' or state == 'WA' or state == 'OR'
```

The scope of the change is isolated to a very focused function, and the risk too is better controlled.



### Supporting Testability

So what's the problem? The first example is synchronous, with no IO.  It is easy realitvely straightforward to configure test objects and exercise all code paths.  Even though it is completely achievable to 100% coverage this routine, when different responsibilities are embededded inthe same routine it becomes difficult to isolate functionality in testing.

To test if the code can identify a west coast state correctly, we need to configure items, user, tax_rate, and a coupon code.  Additionall, we have to execute 4 conditionals before we get to the code we are testing.  This leads to brittle tests. If a new code flow is introduced, or a regression occurs in a previous statement our test for west coast state will fail.  Having a test fail for an unrelated case takes human time to debug and is a waste of human resources.  Another downside is actually isolating the code under test.  The above conditionals are flat and relatively easy to excercise the west coast detection conditional.  But if the code had nested conditionals, or more complicated code flow, it could be really difficult to exercise specific code paths.  Magic values may have to be mirrored in the tests.

Let's look at an example of a unit test excercising the west coast detection logic in the first example:

```python
def test_is_west_coast_state_identified(self):
  #
```

Because west coast logic isn't a discreet unit the test has can only indirectly exercise it.  The only information the assertion has is that the correct tax rate has been applied by assuming it based on the total returned.  This is a brittle operation, and relies on no other code paths/input combination resulting in the same total.  Or else the test will result in a false positive.




When routines are composoed of many small subroutines there should still be a select few tests which excercise that the main routine generally works to accomplish its goal, and that its subroutines colloborate correctly.
