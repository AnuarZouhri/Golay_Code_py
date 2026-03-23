# Golay_Code
Questo progetto illustra tramite un programma (artifically generated) il funzionamento del codice di Golay.
$$H = (P \mid I_{11})$$

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

$$H_1 = (Q \mid I_{12})$$

$$
Q=\left(
\begin{array}{c}
P \\
\hline
1 \; 1 \; 1 \; 1 \; 1 \; 1 \; 1 \; 1 \; 1 \; 1 \; 1 \; 0
\end{array}
\right)
$$

$$
H'=\left(
\begin{array}{c|c|c}
P & I_{11} & \mathbf{0} \\
\hline
1\cdots1 & 1\cdots1 & 1
\end{array}
\right)
$$

**Algoritmo di decodifica per il codice di Golay**

Sia $\underline{r} = (\underline{r}_1 \mid \underline{r}_2)$ la parola ricevuta,
$\underline{s}_1 = \underline{r}H_1^T$, $\underline{s}_2 = \underline{r}H_2^T$.
Siano $\underline{q}_0, \dots, \underline{q}_{11}$ le righe di $Q$,
$\underline{q}_0', \dots, \underline{q}_{11}'$ le righe di $Q^T$
e $\underline{\delta}_i \in GF(2)^{12}$ il vettore con solo il bit $i$-esimo uguale a 1.
```
SE w_H(s1) ≤ 3:
    restituisci r1 e termina

ALTRIMENTI SE w_H(s2) ≤ 3:
    restituisci r1 + s2 e termina

ALTRIMENTI:
    PER i = 0, ..., 11:
        s1_i = s1 + q'_i
        SE w_H(s1_i) ≤ 2:
            restituisci r1 + δ_i e termina

    PER i = 0, ..., 11:
        s2_i = s2 + q_i
        SE w_H(s2_i) ≤ 2:
            restituisci r1 + s2_i e termina

    rileva un errore non correggibile
```
