import numpy as np

# https://en.wikipedia.org/wiki/Singular_value_decomposition

"""
    M(m*n) ≈ U(m.m) @ S(m.n) @ VT(n.n)
    u : eigenvector of M@MT
    v : eigenvector of MT@M
    s**2 : eigenvalues of M@MT and MT@M
    s : singular values M
    v : reduced representation of columns in M,intuitively,new set of axes that allow maximum separation of points
    M@v : projection to new axes
    M@S : reduced representation of rows in M,intuitively,new set of points that capture most variation
"""

"""
    training:
        initialize U,S,VT with appropriate shape regarding M
        constrain S to be diagonal matrix
        constrain VT such that vector length is 1 along both dimension
        update matrices till two sizes of the equation equate
    apply above constraints in training will yield sensical results that align with svd definition
"""

M = np.array([[1, 1], [-1, -1], [6, 5]])
u, s, vh = np.linalg.svd(M, full_matrices=True)
sigma = np.zeros(M.shape)
sigma[:2, :2] = np.diag(s)

"""
    M(m*n) ≈ U(m.m) @ S(m.n) @ VT(n.n)
"""
print(np.allclose(M, u @ sigma @ vh))

"""
    (M@MT)@u = λ*u
"""
eigenval = s ** 2
_eigenval = np.concatenate([s, [0]])
print((M @ M.T) @ u)
print(_eigenval * u)

"""
    (MT@M)@v = λ*v
"""
print((M.T @ M) @ vh.T)
print(eigenval * vh.T)

"""
    M@S = M@v
"""
s = np.concatenate([s, [0]])
print(u * s)
print(M @ vh.T)
print(M @ vh)
print(np.sum(vh**2,axis=0))
print(np.sum(vh**2,axis=1))
