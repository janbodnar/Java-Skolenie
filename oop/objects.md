# Objects 


## Equals & hashcode

I'd be glad to explain the `equals` and `hashCode` methods in Java:

**equals**

- **Purpose:** Determines if two objects are equal in terms of their content or state.
- **Contract:**
  - Reflexive: `x.equals(x)` is always true.
  - Symmetric: If `x.equals(y)` is true, then `y.equals(x)` is also true.
  - Transitive: If `x.equals(y)` and `y.equals(z)` are true, then `x.equals(z)` is also true.
  - Consistent: Multiple invocations of `equals` on the same object with the same non-null
    argument should produce the same result.
  - For any non-null reference `x`, `x.equals(null)` is always false.
- **Default implementation:** The default implementation in `Object` compares references.  
- Two objects are considered equal only if they are the same object.  
- **Custom implementation:** To define your own equality criteria, override the `equals` method  
  in your class. Consider comparing relevant fields using `==` for primitive types and `equals` for objects.  

**hashCode**

- **Purpose:** Returns a hash code value for an object. This value is used by data structures like `HashMap`  
  and `HashSet` to efficiently store and retrieve objects.
- **Contract:**
  - If two objects are equal according to `equals`, then their hash codes must be equal.
  - If two objects are not equal according to `equals`, their hash codes are not required to be different,  
    but it's generally recommended to have different hash codes for different objects to improve performance.  
- **Default implementation:** The default implementation in `Object` generates a hash code based on the  
  object's memory address.
- **Custom implementation:** To improve the efficiency of hash-based data structures, override the  
  `hashCode` method in your class. Consider using a combination of hash codes for relevant fields,  
   applying appropriate algorithms to avoid collisions.

**Relationship between `equals` and `hashCode`**

- If two objects are equal according to `equals`, their `hashCode` methods must return the same value.
- If two objects have different `hashCode` values, they are not equal according to `equals`. However, it's  
  possible for two non-equal objects to have the same `hashCode` (this is known as a hash collision).

**Best Practices**

- Always override both `equals` and `hashCode` together whenever you override one.
- Ensure that your `equals` implementation adheres to the contract.
- Choose a `hashCode` algorithm that minimizes collisions and provides a good distribution of hash values.  
- Consider using a library like Apache Commons Lang's `EqualsBuilder` and `HashCodeBuilder` to simplify  
  the implementation.

By following these guidelines, you can effectively implement `equals` and `hashCode` in your Java classes,  
ensuring correct object comparison and efficient use of hash-based data structures.
