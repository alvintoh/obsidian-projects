Modulus & inner product
* 3 Properties of Vectors
![[Commutative property.png]]

![[Distributive over addition property.png]]

![[Associative over scalar multiplication property.png]]

![[Size of vector formula.png]]

![[Cosine & dot product properties.png]]

![[Projection.png]]

Vectors
* Changing Basis (co-ordinate systems) example using the projection product
* Basis are set at orthogonal (right angled) for each vector

![[Representing Vectors based on different basis.png]]

Basis is a set of n vectors that:
- (i) are not linear combinations of each other (linearly independent)
- (ii) span the space
- The space is then n-dimensional
 ![[Basis and the theory of linear independence.png]]

You can rotate the orthogonal vector, things might be rotated, inverted, stretched or spaced but linear combinations still work
When the new vectors are not orthogonal, you wont be able to use the dot product. You will need to use matrics.
![[Projection of an orthogonal vector.png]]

![[Applications of changing basis.png]]

### Facts about linear independence
1.  Two vectors are linearly dependent if and only if they are collinear, i.e., one is a scalar multiple of the other.
2.  Any set containing the zero vector is linearly dependent.
3.  If a subset of {v1,v2,...,vk} is linearly dependent, then {v1,v2,...,vk} is linearly dependent as well.
  

The following set of vectors cannot be used as a basis for a three dimensional space. Why?
* The vectors do not span three dimensional space. There are three vectors but they are linearly dependent. If we remove one of the vectors the remaining two are linearly independent, which means that the vectors only span two dimensions.
* The vectors are not linearly independent. We can see that c = 2a - b so the vectors are linearly dependent. The definition of a basis requires that the vectors are linearly independent.