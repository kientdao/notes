---
title: logic 1 exam 2022
date: 02-05-2022
private: false
---

## 1 Symbolisations

#### 1. Ziggy didn’t bite

Z - Ziggy bites

~Z

#### 2. Archie will nap if he didn’t sleep

N - Archie naps, S - Archie sleeps

~S ~ N

#### 3. Hugh will pass only if he sits and concentrates

P - Hugh passes, S - Hugh sits, N - Hugh concentrates

(S /\ P) -> P

#### 4. If Kat is a politician, then she isn’t honest

P - is a politician, H - is honest, k - kat

Pk -> ~Hk

#### 5. Either Dave or Sam will come, but not both

D - Dave will come, S - Sam will come

(D /\ S)

#### 6. All humans are mortal

F - is mortal, H - is human

Ax(Fx /\ Hx)

#### 7. Some students partied but Maja didn’t

S - is student, P - partied, m - Maja,

Ex(Sx /\ Px) /\ ~(Sm /\ Pm)

### 8. Only knights tell the truth

K - is knight, T - tells the truth
Ax(Kx -> Tx)

#### 9. No student will pass if they goof off

S - is student, P - will pass, G - goofs off

Ax(Gx -> ~(Sx /\ Px))

#### 10. If a farmer owns a donkey, he beats it

F - is farmer, D - owns a donkey, B - beats it

(F /\ D) -> B

## 2 Derivations

#### 11. (P→¬Q). ¬¬Q ∴ ¬P - Done

#### 12. ¬R∴ (S→¬(S→R)) - Done

#### 13. (Q→¬R). (¬Q→Q)∴ ¬((P→Q)→R) - Done

#### 14. ¬(¬P → (Q∧S)). (¬R∨¬¬P) ∴ ¬R - Done

#### 15. ∃y(Fy ∨ Ha). ∀x(¬Fx ∨ Hx) ∴ ∃xHx - Done

#### 16. (∃xGx → ∀xFx). (∃y(¬Ky ∧ ¬Fy) ∨ ¬∃x¬Hx) ∴ ∀y(Gy → Hy)

#### 17. ∀y(Dy → Gy). ¬∃x(Fx ∧ ¬Dx) ∴ (Fa → ∃x(Gx ∧ Dx)) - Done

#### 18. ∴ ∀y∃x(My ∧ Hx) → ¬∀x(¬Hx ∨ ¬Mx) - Done

#### 19. (Complete without using dm) ∴ ¬(R ∧ X) <-> (¬R ∨ ¬X) - Done

#### 20. (Complete without using qn) ∴ ¬∃y¬Fy <-> ∀yFy - Done

## 3 Models

#### 21. ¬P.(P→Q)∴Q - Done

#### 22. (P→Q)∴(¬Q∨P) - Done

#### 23. ((R∧¬S)→Q) ∴ (R→Q) - Done

#### 24. (¬R→(P∨S)). (P→S). (S→(P→¬R)) ∴ (R↔P) - Done

#### 25. ∴¬(P∧¬Q)→¬(P→Q)

#### 26. (Ga∧Fb) ∴ ¬∃x¬Fx

#### 27. ∴ ¬∀z(¬Hz ∧ ¬Gz)

#### 28. ∃x(¬Gx ∧ Hx). ∃xGx. ¬¬Ga ∴ ∀xGx

#### 29. (Fc ∧ ¬Fb). ∃x¬(Hx → Gx). ∀x(Gx → (Fx ∧ Hx)) ∴ ∃x(Fx ∧ ¬Hx)

#### 30. ∴ ∃y∃z∀x((Fx → ¬Gy) ∧ (Gz → Fx)) → ∃x∀y¬(Fx ↔ Gy)

## 4 Comprehension Questions

### Presumptions

- We know that neither a knight or a knave can identify themself as a knave.
  - A knight will always be honest and say "I am a knight"
  - A Knave will always lie about his identity and say "I am a knight"

#### 31. You have met a group of two inhabitants. Their names are Ziggy and Sam. Ziggy says, “Sam is a knave and I am a knave." Is Ziggy a knight or a knave?

Ziggy's statement is an **and** statement, therefore if one of the conjuncts is false, the statement is false as a whole. As no inhabitant can identify themself as a knave, this statement is false and so Ziggy is a knave.

#### 32. You come across three of the inhabitants standing in a garden. Their names are A, B, and C. A says, “C is a knight". B says, “A never lies". C says, “A is a knight or I am a knave". How many knaves are there?

#### 33. You have met a group of two inhabitants. The first one, A, says something inaudi- ble. You ask the second one, B, what the first one said. B says that A said “I am a knave". Is B a knave?

We know that A cannot say "I am a knave", and so B is lying by saying that A said this. B is a knave.

#### 34. You come across two of the inhabitants playing chess. You ask the one with the white pieces whether the one with the black pieces is a knight, and you get an answer of ‘yes’ or ‘no’. Then you ask the one with the black pieces whether the one with the white pieces is a knight. You get an answer of ‘yes’ or ‘no’. Are the two answers necessarily the same?

answers are the same

35. Let’s say that two inhabitants are the same type of inhabitant, if they are both knights or both knaves. You come across three inhabitants: A, B, and C. A says

#### “B is a knave". B says, “A and C are of the same type". Is C a knight?

C is not a knight

For the following arguments construct an L3 symbolisation capturing as much logical form as possible, and then either provide a derivation of the conclusion from the premises or show that the argument is invalid by providing a countermodel. (5 points each)

#### 36. If all toves are slithy, then all toves gyre and gimble. Either all borogoves are mimsy or every rath is outgrabe. Therefore: If no borogoves are toves, then everything gimbles

#### 37. If the Oracle spoke truthfully, then Socrates is wise. Only that which is virtuous is wise, and only that which has knowledge is virtuous. Thus, if Socrates does not have knowledge, then either something spoke truthfully or nothing is wise

o - Oracle, T - spoke truthfully, s - Socraties, W - is wise, V - is virtuous, K, has knowlege
To -> Ws. @x(Kx -> Vx -> Wx). ~Ks -> Ex(Tx) \/ ~Ax(Wx)

Provide an answer with an explanations to the question below. (5 points) 38. Consider the following argument:

#### Lewis loves Ziggy. Thus, Lewis loves someone, and someone loves Ziggy, and someone loves someone

This is a logically good argument. Can the validity of this argument be captured in the L3 system? If so, translate the argument into L3 and show how to derive the conclusion from the premise. If the validity of the argument can’t be captured in L3, why not? What changes to our formalism are required to capture the validity of the argument?
