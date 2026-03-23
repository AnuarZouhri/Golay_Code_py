# Golay Code

This project illustrates, through a program, the functioning of the Golay code. This argument was part of Thesis for bachelor in Mathematics.

## What is the Golay Code?

The Golay code is a perfect linear error-correcting code, constructed in 1949 by Marcel J. E. Golay. It is one of the most remarkable codes in coding theory, as it achieves the Hamming bound with equality, meaning it is capable of correcting errors with maximum efficiency given its parameters.

The binary Golay code $\mathcal{G}_{23}$ is a $[23, 12, 7]$ linear code, meaning it encodes 12 information bits into 23-bit codewords and can correct up to 3 errors per codeword. Its extended version $\mathcal{G}_{24}$, obtained by adding a parity bit to each codeword, is a $[24, 12, 8]$ code with even stronger error-detection capabilities.

## Applications

The Golay code has found use in several real-world applications:

- **Deep space communications**: NASA used the Golay code in the Voyager 1 and Voyager 2 missions (1977) to transmit images of Jupiter and Saturn back to Earth reliably over vast distances.
- **Data storage**: its strong error-correction properties make it suitable for environments where data integrity is critical.

## Mathematical Background

### Parity-Check Matrix of $\mathcal{G}_{23}$

The Golay code $\mathcal{G}_{23}$ admits a parity-check matrix in systematic form:

$$H = (P \mid I_{11})$$

where $P$ is the following $11 \times 12$ matrix:

$$
P=\left(
\begin{array}{cccccccccccc}
1 & 0 & 1 & 0 & 0 & 0 & 1 & 1 & 1 & 0 & 1 & 1 \\
1 & 1 & 0 & 1 & 0 & 0 & 0 & 1 & 1 & 1 & 0 & 1 \\
0 & 1 & 1 & 0 & 1 & 0 & 0 & 0 & 1 & 1 & 1 & 1 \\
1 & 0 & 1 & 1 & 0 & 1 & 0 & 0 & 0 & 1 & 1 & 1 \\
1 & 1 & 0 & 1 & 1 & 0 & 1 & 0 & 0 & 0 & 1 & 1 \\
1 & 1 & 1 & 0 & 1 & 1 & 0 & 1 & 0 & 0 & 0 & 1 \\
0 & 1 & 1 & 1 & 0 & 1 & 1 & 0 & 1 & 0 & 0 & 1 \\
0 & 0 & 1 & 1 & 1 & 0 & 1 & 1 & 0 & 1 & 0 & 1 \\
0 & 0 & 0 & 1 & 1 & 1 & 0 & 1 & 1 & 0 & 1 & 1 \\
1 & 0 & 0 & 0 & 1 & 1 & 1 & 0 & 1 & 1 & 0 & 1 \\
0 & 1 & 0 & 0 & 0 & 1 & 1 & 1 & 0 & 1 & 1 & 1 \\
\end{array}
\right)
$$

Note that $P$ has a cyclic structure: each row is a one-position right cyclic rotation of the previous one.

### Extended Golay Code $\mathcal{G}_{24}$

The extended Golay code is obtained by appending a parity bit to each codeword of $\mathcal{G}_{23}$. Its parity-check matrix is:

$$H_1 = (Q \mid I_{12})$$

where $Q$ is the $12 \times 12$ matrix obtained by appending a row to $P$:

$$
Q=\left(
\begin{array}{c}
P \\
\hline
1 \; 1 \; 1 \; 1 \; 1 \; 1 \; 1 \; 1 \; 1 \; 1 \; 1 \; 0
\end{array}
\right)
$$

The parity-check matrix used in the decoding proof takes the form:

$$
H'=\left(
\begin{array}{c|c|c}
P & I_{11} & \mathbf{0} \\
\hline
1\cdots1 & 1\cdots1 & 1
\end{array}
\right)
$$

## Decoding Algorithm

The following algorithm decodes a received word for the extended Golay code $\mathcal{G}_{24}$.

Let $\underline{r} = (\underline{r}_1 \mid \underline{r}_2)$ be the received word,
$\underline{s}_1 = \underline{r}H_1^T$, $\underline{s}_2 = \underline{r}H_2^T$.
Let $\underline{q}_0, \dots, \underline{q}_{11}$ be the rows of $Q$,
$\underline{q}_0', \dots, \underline{q}_{11}'$ the rows of $Q^T$,
and $\underline{\delta}_i \in GF(2)^{12}$ the vector with only the $i$-th bit equal to 1.
```
IF w_H(s1) <= 3:
    return r1

ELSE IF w_H(s2) <= 3:
    return r1 + s2

ELSE:
    FOR i = 0, ..., 11:
        s1_i = s1 + q'_i
        IF w_H(s1_i) <= 2:
            return r1 + delta_i

    FOR i = 0, ..., 11:
        s2_i = s2 + q_i
        IF w_H(s2_i) <= 2:
            return r1 + s2_i

    detect an uncorrectable error
```

The algorithm exploits the structure of the syndrome to locate errors. Since $\mathcal{G}_{24}$ can correct up to 3 errors, the algorithm is guaranteed to succeed whenever at most 3 bit errors have occurred.
