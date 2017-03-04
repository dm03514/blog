# Encapsulate Conditional Logic

Encapsulating conditional logic is an easily identifiable refactor, which helps with readability, testability, and can help insulate calling code from changes to business requirements.  I frequently observe code with business logic embedded directly into decision logic without the use of abstractions, which leads to unintutive, brittle, difficult to test code because:
- conditionals frequently involve magic numbers
- when business requirements change, decision logic with multiple conditionals has to be updated, resulting in risky changes
- isloating specific logic branches is difficult and often requires data that is not directly related to the logic branch

To illustrate this, suppose we have an online ordering system.  There is a check out routine where the bulk of client ordering logic takes place:

```python
def checkout(cart, state):
  pass
```
