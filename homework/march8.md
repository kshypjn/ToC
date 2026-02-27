Q : Let $H = \{\langle M, w \rangle \mid M \text{ is a Turing machine that halts on input } w\}$. Prove that $H$ is recursively enumerable but not recursive. That is, show that no Turing machine can decide $H$, even though one can semi-decide it.

---

## $H$ is recursively enumerable

we need to show there exists a TM that accepts $\langle M, w \rangle$ whenever $M$ halts on $w$, and doesn't accept otherwise.

just build a universal Turing machine $U$. on input $\langle M, w \rangle$:

- simulate $M$ on $w$ step by step
- if $M$ halts, accept

that's it. if $M$ halts on $w$, then $U$ will eventually reach that point and accept. if $M$ loops forever on $w$, then $U$ loops forever too — it never accepts but it never explicitly rejects either.

so $U$ semi-decides $H$, which means $H$ is recursively enumerable. 

---

## $H$ is not recursive 


### assume for contradiction

suppose there exists a TM $D$ that decides $H$. so $D$ always halts and:

$$D(\langle M, w \rangle) = \begin{cases} \text{accept} & \text{if } M \text{ halts on } w \\ \text{reject} & \text{if } M \text{ loops on } w \end{cases}$$

---

### build a machine $B$

using $D$, construct a new TM $B$ that takes as input a TM encoding $\langle M \rangle$ and does the following:
```
B on input <M>:
  1. run D on <M, M>   (ask: does M halt on its own encoding?)
  2. if D accepts  →  loop forever
  3. if D rejects  →  halt
```

so $B$ does the opposite of what $D$ predicts about $M$ running on $\langle M \rangle$. since $D$ always halts, $B$ always halts too (it either halts in step 3, or loops in step 2 — wait, looping in step 2 means $B$ doesn't halt on that branch, that's the point).

now feed $B$ its own encoding $\langle B \rangle$. two cases:

case 1 — suppose $B$ halts on $\langle B \rangle$.

then $D(\langle B, B \rangle)$ accepts (since $D$ is correct and $B$ halts on $\langle B \rangle$). but then $B$ goes to step 2 and loops forever on $\langle B \rangle$. contradiction — we assumed $B$ halts.

case 2 — suppose $B$ loops on $\langle B \rangle$.

then $D(\langle B, B \rangle)$ rejects (since $D$ is correct and $B$ loops on $\langle B \rangle$). but then $B$ goes to step 3 and halts. contradiction — we assumed $B$ loops.

both cases give a contradiction. 

