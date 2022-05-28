![[Summation convention and symmetry of the dot product.png]]

![[Symmetry of dot product.png]]

![[Proving summation convention.png]]

![[Dot Product practical example.png]]

![[Matrices changing basis.png]]

![[Proving orthogonal matrices.png]]
![[Doing a transformation in changed basis.png]]

![[Orthogonal matrices.png]]

![[Gram-Schmidt process.png]]

Lab Assignment
```
# Gram-Schmidt process

## Instructions
In this assignment you will write a function to perform the Gram-Schmidt procedure, which takes a list of vectors and forms an orthonormal basis from this set.
As a corollary, the procedure allows us to determine the dimension of the space spanned by the basis vectors, which is equal to or less than the space which the vectors sit.

You'll start by completing a function for 4 basis vectors, before generalising to when an arbitrary number of vectors are given.

Again, a framework for the function has already been written.
Look through the code, and you'll be instructed where to make changes.
We'll do the first two rows, and you can use this as a guide to do the last two.

### Matrices in Python
Remember the structure for matrices in *numpy* is,
```python
A[0, 0]  A[0, 1]  A[0, 2]  A[0, 3]
A[1, 0]  A[1, 1]  A[1, 2]  A[1, 3]
A[2, 0]  A[2, 1]  A[2, 2]  A[2, 3]
A[3, 0]  A[3, 1]  A[3, 2]  A[3, 3]
```
You can access the value of each element individually using,
```python
A[n, m]
```
You can also access a whole row at a time using,
```python
A[n]
```

Building on last assignment, in this exercise you will need to select whole columns at a time.
This can be done with,
```python
A[:, m]
```
which will select the m'th column (starting at zero).

In this exercise, you will need to take the dot product between vectors. This can be done using the @ operator.
To dot product vectors u and v, use the code,
```python
u @ v
```

```
# GRADED FUNCTION
import numpy as np
import numpy.linalg as la

verySmallNumber = 1e-14 # That's 1×10⁻¹⁴ = 0.00000000000001

# Our first function will perform the Gram-Schmidt procedure for 4 basis vectors.
# We'll take this list of vectors as the columns of a matrix, A.
# We'll then go through the vectors one at a time and set them to be orthogonal
# to all the vectors that came before it. Before normalising.
# Follow the instructions inside the function at each comment.
# You will be told where to add code to complete the function.
def gsBasis4(A) :
    B = np.array(A, dtype=np.float_) # Make B as a copy of A, since we're going to alter it's values.
    # The zeroth column is easy, since it has no other vectors to make it normal to.
    # All that needs to be done is to normalise it. I.e. divide by its modulus, or norm.
    B[:, 0] = B[:, 0] / la.norm(B[:, 0])
    # For the first column, we need to subtract any overlap with our new zeroth vector.
    B[:, 1] = B[:, 1] - B[:, 1] @ B[:, 0] * B[:, 0]
    # If there's anything left after that subtraction, then B[:, 1] is linearly independant of B[:, 0]
    # If this is the case, we can normalise it. Otherwise we'll set that vector to zero.
    if la.norm(B[:, 1]) > verySmallNumber :
        B[:, 1] = B[:, 1] / la.norm(B[:, 1])
    else :
        B[:, 1] = np.zeros_like(B[:, 1])
    # Now we need to repeat the process for column 2.
    # Insert two lines of code, the first to subtract the overlap with the zeroth vector,
    # and the second to subtract the overlap with the first.
    B[:, 2] = B[:, 2] - B[:, 2] @ B[:, 0] * B[:, 0] - B[:, 2] @ B[:, 1] * B[:, 1]
    # Again we'll need to normalise our new vector.
    # Copy and adapt the normalisation fragment from above to column 2.
    if la.norm(B[:, 2]) > verySmallNumber :
        B[:, 2] = B[:, 2] / la.norm(B[:, 2])
    else :
        B[:, 2] = np.zeros_like(B[:, 2])
    # Finally, column three:
    # Insert code to subtract the overlap with the first three vectors.
    B[:, 3] = B[:, 3] - B[:, 3] @ B[:, 0] * B[:, 0] - B[:, 3] @ B[:, 1] * B[:, 1] - B[:, 3] @ B[:, 2] * B[:, 2]
    
    # Now normalise if possible
    if la.norm(B[:, 3]) > verySmallNumber :
        B[:, 3] = B[:, 3] / la.norm(B[:, 3])
    else :
        B[:, 3] = np.zeros_like(B[:, 3])    
    
    # Finally, we return the result:
    return B

# The second part of this exercise will generalise the procedure.
# Previously, we could only have four vectors, and there was a lot of repeating in the code.
# We'll use a for-loop here to iterate the process for each vector.
def gsBasis(A) :
    B = np.array(A, dtype=np.float_) # Make B as a copy of A, since we're going to alter it's values.
    # Loop over all vectors, starting with zero, label them with i
    for i in range(B.shape[1]) :
        # Inside that loop, loop over all previous vectors, j, to subtract.
        for j in range(i) :
            # Complete the code to subtract the overlap with previous vectors.
            # you'll need the current vector B[:, i] and a previous vector B[:, j]
            B[:, i] = B[:, i] - B[:, i] @ B[:, j] * B[:, j]
        # Next insert code to do the normalisation test for B[:, i]
        if la.norm(B[:, i]) > verySmallNumber :
            B[:, i] = B[:, i] / la.norm(B[:, i])
        else :
            B[:, i] = np.zeros_like(B[:, i])
            
        
            
    # Finally, we return the result:
    return B

# This function uses the Gram-schmidt process to calculate the dimension
# spanned by a list of vectors.
# Since each vector is normalised to one, or is zero,
# the sum of all the norms will be the dimension.
def dimensions(A) :
    return np.sum(la.norm(gsBasis(A), axis=0))

```

![[Reflecting in a plane.png]]

If vector matrices are perpendicular to each other, they are orthogonal also called normal  in a way
The dot product of 2 matrices is equal to 0
![[Checking normal and orthonormal.png]]

![[Reflecting in a plane workings.png]]

Reflecting Bear Assignment
```
# Reflecting Bear
## Background
Panda Bear is confused. He is trying to work out how things should look when reflected in a mirror, but is getting the wrong results.
In Bear's coordinates, the mirror lies along the first axis.
But, as is the way with bears, his coordinate system is not orthonormal: so what he thinks is the direction perpendicular to the mirror isn't actually the direction the mirror reflects in.
Help Bear write a code that will do his matrix calculations properly! 

## Instructions
In this assignment you will write a Python function that will produce a transformation matrix for reflecting vectors in an arbitrarily angled mirror.

Building on the last assingment, where you wrote a code to construct an orthonormal basis that spans a set of input vectors, here you will take a matrix which takes simple form in that basis, and transform it into our starting basis.
Recall the from the last video,

\\( T = E T_E E^{-1} \\)

You will write a function that will construct this matrix.
This assessment is not conceptually complicated, but will build and test your ability to express mathematical ideas in code.
As such, your final code submission will be relatively short, but you will receive less structure on how to write it.

### Matrices in Python
For this exercise, we shall make use of the @ operator again.
Recall from the last exercise, we used this operator to take the dot product of vectors.
In general the operator will combine vectors and/or matrices in the expected linear algebra way,
i.e. it will be either the vector dot product, matrix multiplication, or matrix operation on a vector, depending on it's input.
For example to calculate the following expressions,

\\( a = \mathbf{s}\cdot\mathbf{t} \\)

\\( \mathbf{s} = A\mathbf{t} \\)

\\( M = A B \\),

One would use the code,
```python
a = s @ t
s = A @ t
M = A @ B

(This is in contrast to the * operator, which performs element-wise multiplication, or multiplication by a scalar.)
```

You may need to use some of the following functions:
```python
inv(A)
transpose(A)
gsBasis(A)
```
These, respectively, take the inverse of a matrix, give the transpose of a matrix, and produce a matrix of orthonormal column vectors given a general matrix of column vectors - i.e. perform the Gram-Schmidt process.
This exercise will require you to combine some of these functions.

```
# PACKAGE
# Run this cell first once to load the dependancies.
import numpy as np
from numpy.linalg import norm, inv
from numpy import transpose
from readonly.bearNecessities import *
# GRADED FUNCTION
# You should edit this cell.

# In this function, you will return the transformation matrix T,
# having built it out of an orthonormal basis set E that you create from Bear's Basis
# and a transformation matrix in the mirror's coordinates TE.
def build_reflection_matrix(bearBasis) : # The parameter bearBasis is a 2×2 matrix that is passed to the function.
    # Use the gsBasis function on bearBasis to get the mirror's orthonormal basis.
    E = gsBasis(bearBasis)
    # Write a matrix in component form that performs the mirror's reflection in the mirror's basis.
    # Recall, the mirror operates by negating the last component of a vector.
    # Replace a,b,c,d with appropriate values
    TE = np.array([[1, 0],
                   [0, -1]])
    # Combine the matrices E and TE to produce your transformation matrix.
    T = E @ TE @ inv(E)
    # Finally, we return the result. There is no need to change this line.
    return T
```

Test Assignment Code
```
# First load Pyplot, a graph plotting library.
%matplotlib inline
import matplotlib.pyplot as plt

# This is the matrix of Bear's basis vectors.
# (When you've done the exercise once, see what happns when you change Bear's basis.)
bearBasis = np.array(
    [[1,   -1],
     [1.5, 2]])
# This line uses your code to build a transformation matrix for us to use.
T = build_reflection_matrix(bearBasis)

# Bear is drawn as a set of polygons, the vertices of which are placed as a matrix list of column vectors.
# We have three of these non-square matrix lists: bear_white_fur, bear_black_fur, and bear_face.
# We'll make new lists of vertices by applying the T matrix you've calculated.
reflected_bear_white_fur = T @ bear_white_fur
reflected_bear_black_fur = T @ bear_black_fur
reflected_bear_face = T @ bear_face

# This next line runs a code to set up the graphics environment.
ax = draw_mirror(bearBasis)

# We'll first plot Bear, his white fur, his black fur, and his face.
ax.fill(bear_white_fur[0], bear_white_fur[1], color=bear_white, zorder=1)
ax.fill(bear_black_fur[0], bear_black_fur[1], color=bear_black, zorder=2)
ax.plot(bear_face[0], bear_face[1], color=bear_white, zorder=3)

# Next we'll plot Bear's reflection.
ax.fill(reflected_bear_white_fur[0], reflected_bear_white_fur[1], color=bear_white, zorder=1)
ax.fill(reflected_bear_black_fur[0], reflected_bear_black_fur[1], color=bear_black, zorder=2)
ax.plot(reflected_bear_face[0], reflected_bear_face[1], color=bear_white, zorder=3);

```