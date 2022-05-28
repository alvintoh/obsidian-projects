![[2 Eigen on Scaling.png]]

![[1 Eigen on shearing.png]]

![[0 Eigen on rotation.png]]

![[Eigen value of -1.png]]

![[2 Eigen vectors (white and green) that do not change when scaled.png]]

![[Eigen vector of 3d rotation.png]]

![[Calculating Eigen values.png]]

![[Eigen vectors working.png]]

![[Power of T N.png]]

![[Computing Eigen basis.png]]

![[Applying transformation matrix to Eigen Basis.png]]

![[Eigenbasis formula.png]]

![[Proving the eigen basis transformation.png]]

![[PageRank algorithm.png]]

Lab Graded Function for Calculating Link Matrix and PageRank

```
# GRADED FUNCTION
# Complete this function to provide the PageRank for an arbitrarily sized internet.
# I.e. the principal eigenvector of the damped system, using the power iteration method.
# (Normalisation doesn't matter here)
# The functions inputs are the linkMatrix, and d the damping parameter - as defined in this worksheet.
# (The damping parameter, d, will be set by the function - no need to set this yourself.)
def pageRank(linkMatrix, d) :
    n = linkMatrix.shape[0]
    M = d * linkMatrix + (1 - d)/ n * np.ones([n, n])
    
    r = 100 * np.ones(n) / n # Sets up this vector
    lastR = r
    r = M @ r
    i = 0
    while la.norm(lastR - r) > 0.01 :
        lastR = r
        r = M @ r
        i += 1
    

    return r

```