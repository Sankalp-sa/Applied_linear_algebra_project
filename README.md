# Applied_linear_algebra_project

 
Applied Linear Algebra Project Report
Topic: Image compression using SVD
________________________________________

Introduction

The purpose of our project is to make the desired image smaller/more compressed while maintaining a lesser level of quality. The ultimate objective is to utilize the image's pixels to reduce its size. 
Several methods for image compression include:
1. Transform coding - This approach is most frequently employed. Cosine Transform Discrete (DCT).
2. Chroma subsampling is the method of encoding images with lower chroma resolution than luma resolution, making use of the human visual system's weaker sensitivity for color contrasts than for brightness.
3. Compression of the fractal.
4. SVD usage (Singular Values Decomposition)

GITHUB Repository link : 

For lossy image compression in this project, we have been applying the idea of standard value decomposition, or SVD. Power Method is the name of the technique employed. Every color in the image has undergone the SVD technique to provide an overview. Here, the image's pixels are represented as a m*n matrix, and SVD is applied to it. According to the requirements for image quality, the user must set the rank for approximation in the code. The resolution of the compressed image increases with rank.


Process of Singular Value Decomposition


Singular Value Decomposition (SVD) is said to be a significant topic in linear algebra by many renowned mathematicians. SVD has many practical and theoretical values; special feature of SVD is that it can be performed on any real (m, n) matrix. Let’s say we have a matrix A with m rows and n columns, with rank r and r ≤ n ≤ m. Then the A can be factorized into three matrices:
 
 
Where Matrix U is an m × m orthogonal matrix 
column vectors u_i , for i = 1, 2, …, m, form an orthonormal set:
 
And matrix V is an n × n orthogonal matrix	
 
column vectors   v_i for i = 1, 2, …, n, form an orthonormal set:
 
Here, S is an m × n diagonal matrix with singular values (SV) on the diagonal. The matrix S
 can be showed in following

For I = 1, 2, …, n, is are called Singular Values (SV) of matrix A. It can be proved that 
 
For I = 1, 2, …, n, σ_i are called Singular Values (SVs) of matrix A. The i v_i’s and u_i’s are called right and left singular-¬vectors of A [1].

Linear transformation Using SVD

It is a matrix representation.

if there is a vector in euclidean space then we will either scale it, or rotate it, or do both sequentially.  
The diagonal matrix is used to stretch the matrix while the matrix having the data in the form of theta shows that we have to rotate it by theta. Stretching is purely based on singular values. If the singular is greater than 1 then stretching; if it is less than 1 then we will do compression; if it is 1 then no change. 
We can write a matrix in the form of multiplication as a multiplication of rotation matrix * Scaling matrix * another rotation matrix.
So in order to find linear transformation we have to find eigenvalues and eigenvectors, then singular values, and a diagonal matrix containing the singular values.
 


Applying SVD in image compression

As we have seen above, SVD rewrites the original matrix as a sum of simpler matrices of rank one. When applied on a given image matrix, SVD decomposes it into three different matrices. However, application of SVD alone does not contribute to compression. After the SVD is applied from [7] and [8], most of the singular values will be discarded while few of them are retained. The fact that we arrange the singular values in the descending order of the diagonal matrix helps in this reduction. As a result of this arrangement, the first value of the diagonal matrix contains most information and all the further values in the matrix contain decreasing amounts of information about the image. So we can conclude that lover singular values contain negligible amounts of information. Hence discarding such values reduces the size of the image while avoiding noticeable distortion from the original picture. Below steps formalized the procedure illustrated above.

Let A be the matrix of the given image. It can be expressed as

A = U∑VT = ∑µ u v T ; summation ranging from 1 to r.

Expanding the summation

A = µ u v T + µ u v T + …. + µ u v T

As we have seen, it is not necessary to compute the summation to the very last of the values in the matrices. Smaller values are dropped before the summation. After truncating the matrix, we get the following summation.

Ak = µ1u1v1T + µ2 u2 v 2T + …. + µ k u k v k T

 

Code Explanation

Algorithm of Power method:
We include a straightforward approach for computing a matrix A's singular value decomposition when it belongs to the R^m*n space. The left and right singular vectors u1 and v1 as well as the first singular value sigma1 of A are computed first.
1. Generate random unit vector(x) having mean = 0 and standard deviation= 1 
2. for i in [1,......,min(m,n)]:
3. xi = (A-transpose)*Ax(i-1)
4. v1 =xi / ||xi||
5. σ1 = ||A*v1|| 
6. u1 = (A*v1)/ σ1
7. return (σ1; u1; v1)

KEY STEPS WHICH INCLUDE LINEAR ALGEBRA:
-Let A be the m x n matrix. →ATA=(U∑VT)T(U∑VT)=V∑UT U∑VT =V∑2VT
-We can eliminate U by performing ATA. Let B = AT A = V ∑2 VT and x be the random unit vector.
-We can write it in terms of singular vectors x = ∑i ci vi. Hence Bx = ∑i ci σi2 vi and performing recursively k times it will give Bk x = ∑i ci σi2 k vi.
-As the first singular value σ1 is larger than all other singular values, the Bk x corresponding to v1 will be larger than the other others.
-Choosing a random unit vector would ensure that for all vectors vj, the ratio of σ1 /σj would be greater than 1.
-The loop computes xt+1 = Bxt, and is renormalized at each step. The loop will break when the angle between xt and xt +1 is nearly 1. Using v1, σ1 and u1 are calculated.
-We want to ensure that the vectors in span of v1 are ignored and hence we will set A to A = A – σ1 u1 v1T and repeat the whole process again.
Code Output:
 
![image](https://user-images.githubusercontent.com/102241865/222789136-e8c10b45-0592-4f13-af4a-c44d06a8f29f.png)







![Uploading image.png…]()

Advantage
	Disadvantage

Can be used to compress any format of image e.g. jpeg, jpg, bmp etc. format
	It is not a very good block- based transformation
technique, and using SVD on the whole image requires lots of memory.

Gives lossy compression
	Takes lot of time. Time complexity is high

Gives option to choose rank to vary image quality.
	To actually save data, we need k > (m*n / (m+n+1). That may not be the case with all the images

	Power method is not numerically stable as a small change in matrix could bring a larger change in singular value ratio of two images.







 
 
  
 
 
 
 

 
