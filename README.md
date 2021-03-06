# RBM to MPS Translation

Demo code for [arXiv:1701.04831v1](http://arxiv.org/abs/1701.04831v1). You are free to use these codes. Please kindly cite the paper 
- Jing Chen, Song Cheng, Haidong Xie, Lei Wang, and Tao Xiang, *Equivalence of restricted Boltzmann machines and tensor network states*, [Phys. Rev. B 97, 085104 (2018)](https://journals.aps.org/prb/abstract/10.1103/PhysRevB.97.085104)

We implement three approaches using Matlab 

* rbm2mps1.m: The algorithm of Fig. 2. The MPS bond dimension is $2^n$, where $n$ is the number of cut RBM connections. 
    * Input:	
        * W:   $n_v$ by $n_h$ weight matrix $W$
    	* a:   vector of size $n_v$ for visible units bias 
        * b:   vector of size $n_h$ for hidden units bias
   	    * bpos: the vector telling which piece the hidden units belongs to. See Fig. 2.
    * Output: 
        * mps: a cell of MPS tensors

* rbm2mps2.m: The algorithm of Fig. 4. The MPS bond dimension is $2^m$, where $m=\min(|A_{1}|, |B_{1}|)$ is the size of the interface region. The algorithm copies the physical degree of freedoms in the interface region to the virtual bond.  
    * Input:      
      * W:  $n_v$ by $n_h$ weight matrix $W$
      * a:  vector of size $n_v$ for visible units bias 
      * b:  vector of size $n_h$ for hidden units bias 
    * Output: 
      * mps: a cell of MPS tensors

* rbm2mps3.m:  The MPS bond dimension is $2^k$, where $k$ is a minimal number of units (no matter visible or hidden) which can break the RBM into a product state if they are fixed. The algorithm copies the $k$ degree of freedoms in the interface region to the virtual bond. 
    * Input:      
      * W:  $n_v$ by $n_h$ weight matrix $W$
      * a:  vector of size $n_v$ for visible units bias 
      * b:  vector of size $n_h$ for hidden units bias 
    * Output: 
      * mps: a cell of MPS tensors

The MPS bond dimensions:
rbm2mps3.m <= rbm2mps2.m <= rbm2mps.m

## Auxillary tensor programs ##
* MPS\_Canonicalize.m: Canonicalize a finite MPS and return the entanglement spectrum of each bond.

* tensor\_product.m: Contract two tensors and permute the indices according to the given order. 
`C = tensor_product('acm',A,'abm',X,'cb')` does $C(a,c,m) = \sum_{c}A_{a,b,m)X_{c,b}$

* tensor\_reshape.m: 
 `B = tensor_reshape( A,'abcd','ac','bd')` reshapes a tensor into a matrix $B( ac,bd ) =  A(a,b,c,d)$.


## Example ##
* Example.m: Using the RBM architecure in Fig. 1(a) as an example, we construct the MPS in three approaches (rbm2mps,rbm2mps2,rbm2mps3). The bond dimensions are consistent with Fig. 2(c) and Fig. 4(c) respectively. The three MPS are identical in their canonical form. 
