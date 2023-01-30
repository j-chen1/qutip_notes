# Unitary Transformation for Single Qubit

Created: January 25, 2023 10:45 PM
Edited: January 28, 2023 9:28 PM

**************************************************Single Qubit Hamiltonian**************************************************

$$
H = \frac{1}{2}\omega_r\sigma_z + \sigma_x\Omega(e^{-i\omega_d t} + e^{-i\omega_d t})\\
\text{where } \sigma_z = \begin{pmatrix}
1 & 0\\
0 & -1
\end{pmatrix} \text{ and } \sigma_x = \begin{pmatrix}
0 & 1\\
1 & 0
\end{pmatrix}
$$

The above describes the Hamiltonian of a qubit whose frame is rotating at a frequency $\omega_r$ around the Bloch sphere and the path of the qubit’s state is traced out by  $\sigma_x\Omega(e^{-i\omega_d t} + e^{-i\omega_d t})$ driven by a frequency $\omega_d$. 

From [Unitary Transformation - Wikipedia](https://en.wikipedia.org/wiki/Unitary_transformation_(quantum_mechanics)), the Hamiltonian can be interpreted as: 

> “ an atom with two states, ground $\ket{g}$ and excited $\ket{e}$. $\omega_r$ is the frequency of light associated with the ground to excited transition. Now suppose we illuminate the atom with a drive at frequency $\omega_d$ which couples the two states”
> 

********************************************Apply Unitary Transformation********************************************

So to simplify the Hamiltonian, we want to apply the unitary transformation:

$$
H \rightarrow UHU^\dagger + i\dot UU^\dagger \text{ where } U = e^{i\omega_dt\sigma_z/2}
$$

More documentation on unitary transformation can be found: 

[Unitary transformation (quantum mechanics) - Wikipedia](https://en.wikipedia.org/wiki/Unitary_transformation_(quantum_mechanics))

We solve for $i\dot UU^\dagger$ through the following:

$$
\begin{align*}
U^{\dagger} &= e^{-i\omega_dt\sigma_z/2}\\
\dot U &= (\frac{i\omega_dt\sigma_z}{2})e^{i\omega_dt\sigma_z/2}\\ \\
i\dot UU^\dagger &= i(\frac{i\omega_d\sigma_z}{2}e^{i\omega_dt\sigma_z/2})(e^{-i\omega_dt\sigma_z/2})\\
&= -\frac{\omega_d\sigma_z}{2}
\end{align*}
$$

---

Now we look at $UHU^{\dagger}$ which is considerably more complicated:

$$
e^{i\omega_dt\sigma_z/2}\left(\frac{1}{2}\omega_r\sigma_z + \sigma_x\Omega(e^{-i\omega_d t} + e^{-i\omega_d t})  \right)e^{-i\omega_dt\sigma_z/2}
$$

From the matrix multiplication property: $A(B+C)D = ABD + ACD$, we can distribute the outer matrices to obtain:

$$
= \frac{1}{2}\omega_r (e^{i\omega_dt\sigma_z/2}\sigma_ze^{-i\omega_dt\sigma_z/2}) + \Omega(e^{-i\omega_d t} + e^{-i\omega_d t})(e^{i\omega_dt\sigma_z/2}\sigma_xe^{-i\omega_dt\sigma_z/2})
$$

Now let’s first take a look at the first expression on the left:

$$
\begin{align*}
\frac{1}{2}\omega_r e^{i\omega_dt\sigma_z/2}\sigma_ze^{-i\omega_dt\sigma_z/2} &=\\
&= \frac{\omega_r\sigma_z}{2}
\end{align*}
$$

This is because $e^{i\omega_dt\sigma_z/2}\sigma_ze^{-i\omega_dt\sigma_z/2}$ commutes as a consequence of $[A, e^A] =0$, which can be verified by applying the Taylor series expansion and examining how $Ae^A = e^AA$.  

To simplify the 2nd expression, we first want to transform $e^{i\omega_dt\sigma_z/2} \text{ and } e^{-i\omega_dt\sigma_z/2}$ into matrices we can work with and multiply. To do so, we use the technique detailed in the link below: 

[Matrix exponentiation of Pauli matrix](https://physics.stackexchange.com/questions/510221/matrix-exponentiation-of-pauli-matrix)

Because $\sigma_z$ is a symmetric matrix, this means we can diagonalize it and convert it into the form $PDP^{-1}$ where $D$ is a diagonal matrix. So $\sigma_z$ is equal to: 

$$
\begin{align*}
&= \begin{pmatrix}
1 & 0\\
0 & 1
\end{pmatrix}\\ 
&= 
\begin{pmatrix}
1 & 0\\
0 & 1
\end{pmatrix}\\
&=
\begin{pmatrix}
1 & 0\\
0 & -1
\end{pmatrix}\\
&=
\begin{pmatrix}
1 & 0\\
0 & 1
\end{pmatrix}\\
&= I\sigma_zI\\
\sigma_z ^n &= \begin{pmatrix}
1^n & 0\\
0 & (-1)^n
\end{pmatrix}\\
\left(\frac{i\omega_dt\sigma_z}{2}\right)^n &= 
\begin{pmatrix}
\frac{i\omega_dt}{2}^n & 0\\
0 & (-\frac{i\omega_dt}{2})^n
\end{pmatrix}\\
\end{align*}
$$

By the exponential of a matrix we can use the previous results to derive the matrix form: 
$$
\begin{align*}
e^{\frac{i\omega_dt\sigma_z}{2}} &= \sum_{n=0}^{\infty} \frac{(\frac{i\omega_dt\sigma_z}{2})^n}{n!}\\
&= 
\begin{pmatrix}
e^{\frac{i\omega_dt}{2}} & 0\\
0 & e^{-\frac{i\omega_dt}{2}}
\end{pmatrix}
\end{align*}
$$

Let’s now compute the following: 

$$
\begin{align*}
e^{i\omega_dt\sigma_z/2}\sigma_xe^{-i\omega_dt\sigma_z/2} &= \\
&= \begin{pmatrix}
e^{\frac{i\omega_dt}{2}} & 0\\
0 & e^{-\frac{i\omega_dt}{2}}
\end{pmatrix} \begin{pmatrix}
0 & 1\\
1 & 0
\end{pmatrix}\begin{pmatrix}
e^{-\frac{i\omega_dt}{2}} & 0\\
0 & e^{\frac{i\omega_dt}{2}}
\end{pmatrix}\\
&= \begin{pmatrix}
e^{\frac{i\omega_dt}{2}} & 0\\
0 & e^{-\frac{i\omega_dt}{2}}
\end{pmatrix}\begin{pmatrix}
0 & e^{\frac{i\omega_dt}{2}}\\
e^{-\frac{i\omega_dt}{2}} & 0
\end{pmatrix}\\
&= \begin{pmatrix}
0 & e^{i\omega_dt}\\
e^{-i\omega_dt} & 0
\end{pmatrix}\\ \\
\Omega(e^{-i\omega_d t} + e^{-i\omega_d t})e^{i\omega_dt\sigma_z/2}\sigma_xe^{-i\omega_dt\sigma_z/2} &= \Omega(e^{-i\omega_d t} + e^{-i\omega_d t})\begin{pmatrix}
0 & e^{i\omega_dt}\\
e^{-i\omega_dt} & 0
\end{pmatrix}\\
\end{align*}
$$

We can simplify this further by utilizing:

$$
\sigma_+ = \begin{pmatrix}
0 & 1\\
0 & 0
\end{pmatrix} \quad \sigma_- = \begin{pmatrix}
0 & 0\\
1 & 0
\end{pmatrix}
$$

$$
\begin{align*}
\Omega(e^{-i\omega_d t} + e^{-i\omega_d t})\begin{pmatrix}
0 & e^{i\omega_dt}\\
e^{-i\omega_dt} & 0
\end{pmatrix} &=\\
&= \Omega(e^{-i\omega_d t} + e^{-i\omega_d t})(e^{i\omega_dt}\sigma_+ + e^{-i\omega_dt}\sigma_-)\\
&= \Omega\left(\sigma_+ + e^{-2i\omega_d t}\sigma_- + e^{2i\omega_d t}\sigma_+ + \sigma_-\right)
\end{align*}
$$

**The final combined expression becomes:**

$$
H \rightarrow UHU^\dagger + i\dot UU^\dagger \text{ where } U = e^{i\omega_dt\sigma_z/2}\\
= -\frac{\omega_d\sigma_z}{2} + \left(\frac{\omega_r\sigma_z}{2} + \Omega\left(\sigma_+ + e^{-2i\omega_d t}\sigma_- + e^{2i\omega_d t}\sigma_+ + \sigma_-\right) \right)\\
= \frac{(\omega_r -\omega_d)\sigma_z}{2} +\Omega\left(\sigma_+ + e^{-2i\omega_d t}\sigma_- + e^{2i\omega_d t}\sigma_+ + \sigma_-\right)
$$

When $\omega_r = \omega_d$, there is resonance in the system and the first term disappears. And at sufficiently high frequencies, the $e^{-2i\omega_dt}$ and $e^{2i\omega_dt}$ disappear, leaving us with:

$$
\frac{\sigma_z}{2} \Delta+\Omega\left(\sigma_+ + \sigma_-\right)
$$