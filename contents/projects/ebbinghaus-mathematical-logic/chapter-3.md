---
title: Semantics of First-Order Languages
date:
  - start: 2015-12
  - end: work-in-progress
plugin:
  - mathjax
---

# Semantics of First-Order Languages

## Structures and Interpretations

An <u>$S$-structure</u> is a pair $\mathfrak{A} = (A, \mathfrak{a})$ with the following properties:

* $A$ is a nonempty set, the <u>domain</u> or <u>universe</u> of $\mathfrak{A}$.
* $\mathfrak{a}$ is a function defined on  $S$ satisfying:
  * for every _n_-ary relation symbol $R$ in $S$, $\mathfrak{a}(R)$ is an _n_-ary relation on A.
  * for every _n_-ary function symbol $f$ in $S$, $\mathfrak{a}(f)$ is an _n_-ary function on A.
  * for every constant $c$ in $S$, $\mathfrak{a}(c)$ is an element of $A$.

Frequently, we write $R^\mathfrak{A}, f^\mathfrak{A}, c^\mathfrak{A}$ instead of $\mathfrak{a}(R), \mathfrak{a}(f), \mathfrak{a}(c)$. For structures $\mathfrak{A}, \mathfrak{B}, \dots$, we shall use $A, B, \dots$ to denote their domains. We often replace $\mathfrak{a}$ by a list of its values. For example, we write an $\{R, f, g\}$-structure as $\mathfrak{A} = (A, R^\mathfrak{A}, f^\mathfrak{A}, g^\mathfrak{A})$.

An <u>assignment</u> in an $S$-structure $\mathfrak{A}$ is a map $\beta: \{v_n : n \in \mathbb{N}\} \rightarrow A$ of the set of **variables** into the domain A.

An <u>$S$-interpretation</u> $\mathfrak{I}$ is a pair $(\mathfrak{A}, \beta)$ consistent of an $S$-structure $\mathfrak{A}$ and an assignment $\beta$ in $\mathfrak{A}$.

If $\alpha \in A$ and $x$ is a variable, then:

$$
\beta\frac{\alpha}{x} :=
\left\{
\begin{array}{l l}
\beta(y) & \text{if} \ y \neq x \\
\alpha & \text{if} \ y = x
\end{array}
\right.
$$

For $\mathfrak{I} = (\mathfrak{A}, \beta)$, let $\mathfrak{I}\frac{\alpha}{x} := (\mathfrak{A}, \beta\frac{\alpha}{x})$.

## Standardization of Connectives

Connectives for which the truth-values of compound propositions depends only on the truth-values of the constituents are called <u>extensional</u>, like all connectives used here. In contrast, in <u>intentional</u> usage the truth-values of compound statements also depend on other facts, like temporal relation: *She fell ill and went to the hospital.*

## The Satisfaction Relation

First, for every interpretation $\mathfrak{I} = (\mathfrak{A}, \beta)$, we associate with every term $t$ an element $\mathfrak{I}(t)$ with  from the domain $A$:

* $\mathfrak{I}(x) := \beta(x)$
* $\mathfrak{I}(c) := c^\mathfrak{A}$
* $\mathfrak{I}(ft_1\dots t_n) := f^\mathfrak{A}(\mathfrak{I}(t_1) \dots \mathfrak{I}(t_n))$

The satisfaction relation can therefore be defined as:

| Formula                                  | Definition                               |
| ---------------------------------------- | ---------------------------------------- |
| $\mathfrak{I} \models t_1 \equiv t_2$    | $\mathfrak{I}(t_1) = \mathfrak{I}(t_2)$  |
| $\mathfrak{I} \models Rt_1 \dots t_n$    | $R^\mathfrak{A}\mathfrak{I}(t_1) \dots \mathfrak{I}(t_2)$ |
| $\mathfrak{I} \models \neg \varphi$      | not $\mathfrak{I} \models \varphi$       |
| $\mathfrak{I} \models \varphi \land \psi$ | $\mathfrak{I} \models \varphi$ and $\mathfrak{I} \models \psi$ |
| $\mathfrak{I} \models \varphi \lor \psi$ | $\mathfrak{I} \models \varphi$ or $\mathfrak{I} \models \psi$ |
| $\mathfrak{I} \models \varphi \rightarrow \psi$ | if $\mathfrak{I} \models \varphi$ then $\mathfrak{I} \models \psi$ |
| $\mathfrak{I} \models \varphi \leftrightarrow \psi$ | $\mathfrak{I} \models \varphi$ if and only if $\mathfrak{I} \models \psi$ |
| $\mathfrak{I} \models \forall x \varphi$ | for all $a \in A$, $\mathfrak{I}\frac{a}{x} \models \varphi$ |
| $\mathfrak{I} \models \exists x \varphi$ | there is an $a \in A$ such that $\mathfrak{I}\frac{a}{x} \models \varphi$ |

In English, the above relation is equivalent to saying that $\mathfrak{I}$ is a model of $\varphi$, that $\mathfrak{I}$ satisfies $\varphi$, or that $\varphi$ holds in $\mathfrak{I}$.

### Exercise

> Show that for every positive formula, i.e. a formula which does not contain $\neg, \to, \leftrightarrow$, there is an $S$-interpretation which satisfies it.

This can be proved inductively. Consider a set with only one element $x$. Let $\mathfrak{a}$ be a map such that for every constant $c$, $\mathfrak{a}(c) = x$, that for every function symbol $f$, $\mathfrak{a}(f)$ is a constant function whose value is always $x$, and that for every relation symbol $R$, $\mathfrak{a}(R)$ always holds. The rest proof is merely repetitive applications of the inductive hypothesis.

## The Consequence Relation

Let $\Phi$ be a set of formulas and $\varphi$ a formula. $\varphi$ is a <u>consequence</u> of $\Phi$, or $\Phi \models \varphi$, :iff every interpretation which is a model of $\Phi$ is also a model of $\varphi$. Instead of $\{\varphi\} \models \psi$, we write $\varphi \models \psi$.

The meaning of $\models$, whether it is the satisfaction or the consequence relation, is determined by what comes before it—an interpretation, or a set of formulas.

If $\Phi \models \varphi$ doesn’t hold, it doesn’t necessarily imply that $\Phi \models \varphi$. An example is that given only the group axioms we can say nothing about $v_0 \circ v_1 = v_1 \circ v_0$.

### Validity, Satisfiability, and Logic Equivalence

A formula $\varphi$ is <u>valid</u>, or $\models \varphi$, :iff $\emptyset \models \varphi$. Another term for validity is <u>tautology</u>. Examples include $\varphi \lor \neg \varphi$ and $\exists x\  x \equiv x$.

A formula $\varphi$ is <u>satisfiable</u>, or $\text{Sat } \varphi$, iff there is an interpretation which is a model of $\varphi$. A set of formulas $\Phi$, is <u>satisfiable</u>, or $\text{Sat } \Phi$ iff there is an interpretation which is a model of all the formulas in $\Phi$.

**Lemma**. for all $\Phi$ and all $\varphi$, $\Phi \models \varphi$ if and only if *not* $\text{Sat } \Phi \cup \{\neg \varphi\}$. **Proof**. Simple direct derivation with quantifier negation.

----

Two formulas $\varphi$ and $\psi$ are <u>logically equivalent</u>, or $\newcommand\logicequiv{\mathrel{{=}\mkern-3mu\vert\vert\mkern-3mu{=}}} \varphi \logicequiv \psi$, :iff $\varphi \models \psi$ and $\psi \models \varphi$. Thus, the two formulas are valid under the same interpretations, namely $\models \varphi \leftrightarrow \psi$.

From truth-tables we can easily prove that the left and right of each row are logically equivalent:

| Syntactic Sugar              | Expanded Form                            |
| ---------------------------- | ---------------------------------------- |
| $\varphi \land \psi$         | $\neg(\neg\varphi \lor \psi)$            |
| $\varphi \to \psi$           | $\neg \varphi \lor \psi$                 |
| $\varphi\leftrightarrow\psi$ | $\neg(\varphi\lor\psi)\lor\neg(\neg\varphi\lor\neg\psi)$ |
| $\forall x\varphi$           | $\neg\exists x\neg\varphi$               |

A *desugar* map $^*: \varphi \mapsto \varphi^*$ can be defined inductively.

### Coincidence Lemma

Let $\mathfrak{I}_1 = (\mathfrak{A}_1, \beta_1)$ be an $S_1$-interpretation and $\mathfrak{I}_2 = (\mathfrak{A}_2, \beta_2)$ be an $S_2$-interpretation, both with the same domain, put $S := S_1 \cup S_2$:

* Let $t$ be an $S$-term. If $\mathfrak{I}_1$ and $\mathfrak{I}_2$ agree on the $S$-symbols occurring in $t$ and on the variables occurring in $t$, then $\mathfrak{I}_1(t) = \mathfrak{I}_2(t)$.
* Let $\varphi$ be an $S$-formula. If $\mathfrak{I}_1$ and $\mathfrak{I}_2$ agree on the $S$-symbols occurring in $t$ and on the free variables occurring in $t$, then $\mathfrak{I}_1 \models \varphi$ *iff* $\mathfrak{I}_2 \models \varphi$.

The lemma can be proven by induction trivially.

A more suggestive notation. If $\varphi \in L^S_n$, that is $\varphi$ has _n_ free variables, instead of $(\mathfrak{A}, \beta) \models \varphi$, we write $\mathfrak{A} \models \varphi[a_0, \dots, a_{n-1}]$. If $\text{var}(t) \subset \{v_0, \dots, v_{n-1}\}$, we write $t^\mathfrak{A}[a_0, \dots, a_{n-1}]$. When there is no free variable in $\varphi$, i.e. $\varphi$ is a <u>sentence</u>, we write $\mathfrak{A} \models \varphi$.

----

Let $S$ and $S'$ be symbol sets such that $S \subset S'$; let $\mathfrak{A} = (A, \mathfrak{a})$ be an $S$-structure, and $\mathfrak{A}' = (A', \mathfrak{a}')$ be an $S'$-structure. When and only when $A = A'$ and $\mathfrak{a}$ and $\mathfrak{a}'$ agree on $S$, we call $\mathfrak{A}$ a <u>reduct</u>—more precisely $S$-<u>reduct</u>—of $\mathfrak{A}'$, and conversely the latter an <u>expansion</u> of $\mathfrak{A}$. We write $\mathfrak{A} = \mathfrak{A}'|_S$.

If $\mathfrak{A} = \mathfrak{A}'|_S$, we have $\mathfrak{A} \models \varphi[a_0, \dots, a_n]$ *iff* $\mathfrak{A}' \models \varphi[a_0, \dots, a_n]$. This can be easily shown by constructing $\beta : v_i \mapsto a_i$ and applying the coincidence lemma.

A fixed symbol set $S$ is no longer necessary. Assuming that $S \subset S'$, $\Phi$ is satisfiable with respect to $S$ _iff_ $\Phi$ is satisfiable with respect to $S'$. The proof is straightforward.

### Exercises

#### 4.9

* Show that $(\varphi \lor \psi) \models \chi$ *iff* $\varphi \models \chi$ and $\psi \models \chi$
  
  $(\varphi \lor \psi) \models \chi$
  
  * *iff* every interpretation which is a model of $\varphi \lor \psi$ is also a model of $\chi$
  * *iff* every interpretation which is either a model of $\varphi$ or of $\psi$ is also a model of $\chi$
  * *iff* every interpretation which, if it is a model of $\varphi$ then it is a model of $\chi$, or if it is a model of $\psi$ then it is a model of $\chi$
  * *iff* every interpretation which is a model of $\varphi$ is also a model of $\chi$ and every interpretation which is a model of $\psi$ is a model of $\chi$
  * *iff* $\varphi \models \chi$ and $\psi \models \chi$
  
* Show that $\models (\varphi \to \psi)$ iff $\varphi \models \psi$
  
  $\models (\varphi \to \psi)$
  
  * *iff* $\varphi \to \psi$ holds under all interpretations
  * *iff* every interpretation under which $\varphi$ holds then $\psi$ holds
  * *iff* $\varphi \models \psi$

#### 4.10

* Show that $\exists x \forall y \varphi \models \forall x \exists y \varphi$
  
  Let $\mathfrak{I}$ be an arbitrary interpretation such that $\mathfrak{I} \models \varphi$. There exists $a$ in the domain of $\mathfrak{I}$ such that $\mathfrak{I}\frac{a}{x} \models \forall y \varphi$. Then, for each element $b$ of the domain of $\mathfrak{I}$, we have $(\mathfrak{I}\frac{a}{x})\frac{b}{y} \models \varphi$. Therefore, $\mathfrak{I}\frac{b}{y} \models \exists x \varphi$ for each element $b$ of the domain of $\mathfrak{I}$. Consequently, we know $\mathfrak{I} \models \forall x \exists y \varphi$.
  
* Show that $\forall x \exists y Rxy \models \exists x \forall y Rxy$ does not hold.
  
  Let the domain be $\mathbb{R}$ and $R$ be the $<$ relation. Clearly for all real numbers there exists some number such that the former is smaller than the latter, but there doesn’t exist a number such that it is smaller than every number else.

#### 4.11

Prove $\forall x(\varphi \land \psi) \logicequiv (\forall x \varphi \land \forall x \psi)$.

* Prove $\forall x (\varphi \land \psi) \models (\forall x \varphi \land \forall x \psi)$
  
  Let $\mathfrak{I}$ be an arbitrary interpretation such that $\mathfrak{I} \models \forall x (\varphi \land \psi)$. For any $ a \in A$, we know that $\mathfrak{I}\frac{a}{x} \models \varphi \land \psi$, namely $\mathfrak{I}\frac{a}{x} \models \varphi$ and $\mathfrak{I}\frac{a}{x} \models \psi$. Since $a$ can be any element of $A$, we know that $\mathfrak{I} \models \forall x \varphi$ and $\mathfrak{I} \models \forall x \psi$. Consequently, $\forall x (\varphi \land \psi) \models (\forall x \varphi \land \forall x \psi)$.
  
* Prove $(\forall x \varphi \land \forall x \psi) \models \forall x (\varphi \land \psi)$
  
  Similar to the proof above.

Prove $\exists x(\varphi \lor \psi) \logicequiv (\exists x \varphi \lor \exists x \psi)$.

* Prove $\exists x(\varphi \lor \psi) \models (\exists x \varphi \lor \exists x \psi)$
  
  Similar to the proof below.
  
* Prove $(\exists x \varphi \lor \exists x \psi) \models \exists x(\varphi \lor \psi)$
  
  Let $\mathfrak{I}$ be an arbitrary interpretation such that $\mathfrak{I} \models \exists x \varphi \lor \exists x \psi$. At least one of $\exists x \varphi$ or $\exists x \psi$ must hold under $\mathfrak{I}$. For simplicity, assume that $\exists x \varphi$ holds under $\mathfrak{I}$. We know that there must be an $a \in A$ such that $\mathfrak{I}\frac{a}{x} \models \varphi$. Therefore, $\mathfrak{I}\frac{a}{x} \models (\varphi \lor \psi)$. Consequently, $\mathfrak{I} \models \exists x (\varphi \lor \psi)$.

Prove $\forall x (\varphi \lor \psi) \logicequiv (\varphi \lor \forall x \psi)$, if $x \notin \text{free}(\varphi)$.

* Prove $\forall x (\varphi \lor \psi) \models (\varphi \lor \forall x \psi)$
  
  Let $\mathfrak{I}$ be an arbitrary interpretation such that $\mathfrak{I} \models \forall x (\varphi \lor \psi)$. Then, for all $a \in A$, $\mathfrak{I}\frac{a}{x} \models (\varphi \lor \psi)$. Since $x \notin \text{free}(\varphi)$, applying the coincidence lemma we know that $\mathfrak{I}\frac{a}{x} \models \varphi$ *iff* $\mathfrak{I} \models \varphi$.  If $\mathfrak{I}\frac{a}{x} \models \varphi$, we have $\mathfrak{I} \models \varphi$ and $\mathfrak{I} \models (\varphi \lor \psi)$. If $\varphi$ doesn’t hold under $\mathfrak{I}\frac{a}{x}$, neither does $\varphi$ hold under $\mathfrak{I}$. Therefore, $\psi$ must hold under $\mathfrak{I}\frac{a}{x}$ for all $x \in A$, and $\mathfrak{I} \models \forall x \psi$. Consequently, $\mathfrak{I} \models (\varphi \lor \forall x \psi)$.
  
* The reverse proof is similar.
  
* It’s not hard to construct $\varphi$ such that it holds for some $x$ but not all elements in $A$. Since $x$ is a free variable of $\varphi$, we can construct an interpretation $\mathfrak{I}$ such that $\mathfrak{I} \models \varphi$, but $\forall x \varphi$ doesn’t hold. In other words, one can not apply the coincidence lemma, a crucial step in proving their logical equivalence.

The last one is similar to the third one and therefore omitted.

#### 4.12

> Let $\varphi$ and $\psi$ be formulas such that $\varphi \logicequiv \psi$. Let $\chi'$ be obtained from the formula $\chi$ by replacing all sub formulas of the form $\varphi$ by $\psi$.


> 1. Define the map $'$ be induction on formulas.
> 2. Show that for all $\chi$, $\chi \logicequiv \chi'$.

$\varphi$ should have some formula variables—connected by logical connectives—and term variables—connected by $\equiv$, relation symbols, or term level things. The procedure to determine whether a sub formula of $\chi$ is of the form $\varphi$ is a simple recursive algorithm:

1. Let $\lambda$ be the current sub formula of $\chi$ and $\mu$ be $\varphi$. Let $\Gamma$ be an empty substitution—a function from variables to some sub formula of $\chi$.
2. Match the main connectives of $\lambda$ and $\mu$. If the do not match, the algorithm terminates unsuccessfully.
3. We check each subpart of $\lambda$ and $\mu$. Let $\lambda$ and $\mu$ be the corresponding subpart of themselves:
   1. If $\mu$ is not atomic—namely it is neither a formula variables nor a term variable—we go to step 2. If the algorithm proceeds successfully, we go back to step 3 and check the next subpart.
   2. If $\mu$ is atomic and $\mu \in \Gamma$ (i.e. it is unified), we compare $\Gamma(\mu)$ and $\lambda$. If they are identical, we go back to step 3 and check the next subpart. If not, the algorithm terminates unsuccessfully.
   3. Otherwise we add $(\mu, \lambda)$ to $\Gamma$ and check the next subpart.

Taking the size of each call’s arguments as measures, we can see the algorithm will always terminate.

The main replacing algorithm recursively call the above algorithm to each sub formula, using a top-down fashion. If a sub formula $\lambda$ matches $\varphi$, we “instantiate” $\psi$ with  $\Gamma$ to obtain $\lambda'$ and replace $\lambda$ with $\lambda'$. We then recursively apply the mapping algorithm to $\lambda'$. In other words, $'$ is an <u>anamorphism</u>.

The proof of logical equivalence is merely recursive application of the induction hypothesis and thus omitted.

#### 4.13

> Prove that $\varphi \models \psi$ with respect to $S$ iff $\varphi \models \psi$ with respect to $S'$.

Assume $\varphi \models \psi$ with respect to $S'$. Let $\mathfrak{I}=(\mathfrak{A}, \beta)$ be an $S$-interpretation such that $\mathfrak{I} \models \varphi$,  we  can construct an expansion $\mathfrak{A}'$ of $\mathfrak{A}$ to $S'$ such that $\mathfrak{A} = \mathfrak{A}'|_s$. Let $\mathfrak{I}' = (\mathfrak{A}', \beta)$. By coincidence lemma, we know $\mathfrak{I}' \models \varphi$, therefore $\mathfrak{I}' \models \psi$. Applying coincidence lemma again and we obtain that $\mathfrak{I} \models \psi$.

The reverse is similar and thus omitted.

#### 4.14

Group axioms without:

- Identity: $(\{a, b\}, \circ, a)$ where $a \circ a = b \circ b = a$ and $a \circ b = b \circ a = b$.
- Inverse: a free monoid.
- Associativity: bijective functions over the set of real numbers, with identity function as identity and function composition as group multiplication.
- Closure: $(\{0,1,-1\},+,1)$

Axioms for equivalence relations without:

- Reflexivity: a singleton set with an “empty” relation.
- Symmetry: subset relation.
- Transitivity: a distance relation, namely $Rab$ iff $|a - b| < \epsilon$ for some $\epsilon > 0$.

#### 4.15

Proof by induction. Omitted.

#### 4.16

Induction hypothesis: If $\varphi$ is a Horn formula and if every $\mathfrak{I}_i$ is a model of  $\varphi$ then $\Pi_{i \in I}\mathfrak{I}_i\models\varphi$.

If $\varphi = \varphi_1 \land \varphi_2$. For any interpretation $\mathfrak{I}_i \models \varphi$, we know $\mathfrak{I}_i \models \varphi_1$ and $\mathfrak{I}_i \models \varphi_2$. Therefore, by induction hypothesis, we have $\Pi_{i\in I} \mathfrak{I}_i \models \varphi_1$ and $\Pi_{i\in I} \mathfrak{I}_i \models \varphi_2$. Then, we have $\Pi_{i\in I} \mathfrak{I}_i \models \varphi_1 \land \varphi_2$.

If $\varphi = \lnot \varphi_0 \lor \dots \lor \lnot \varphi_n$. Pick a pair of $i, j$ such that $\mathfrak{I}_i \models \varphi_j$ doesn’t hold. Since each sub-formulas are atomic, following the definition of direct product (c.f. 4.15) $\Pi_{i \in I}\mathfrak{I}_i \models \lnot \varphi_j$. Then, $\Pi_{i \in I} \mathfrak{I}_i \models \lnot \varphi_0 \lor \dots \lor \lnot \varphi_n$.

If $\varphi = \lnot \varphi_0 \lor \dots \lor \lnot \varphi_n \lor \psi$. If there exists a pair of $i, j$ such that $\mathfrak{I}_i \models \lnot \varphi_j$, we reduce the case to the last one. If not, then $\mathfrak{I}_i \models \psi$ for all $i \in I$. Again, following the definition of direct product, $\Pi_{i \in I} \mathfrak{I}_i \models \psi$. Thus $\Pi_{i \in I} \mathfrak{I}_i \models \lnot \varphi_0 \lor \dots \lor \lnot \varphi_n \lor \psi$.

If $\varphi = \exists x \psi$. Then, there exists $c_i$ for each $i \in I$ such that $\mathfrak{I}_i \frac{c_i}{x} \models \psi$. Let $c = (c_1, \dots, c_n)$, by induction hypothesis—and coincidence lemma if necessary—$(\Pi_{i \in I} \mathfrak{I}_i)\frac{c}{x} \models \psi$. Thus, $\Pi_{i \in I}\mathfrak{I}_i \models \exists x \psi$.

If $\varphi = \forall x \psi$. For any pair of $(c_1, \dots, c_n)$, $\mathfrak{I}_i\frac{c_i}{x} \models \psi$ for each $i \in I$. Let $c = (c_1, \dots, c_n)$, by induction hypothesis, $(\Pi_{i \in I}\mathfrak{I}_i)\frac{c}{x} \models \psi$. Consequently, $\Pi_{i \in I} \mathfrak{I}_i \models \forall x \psi$.

Hence the proof of this hypothesis completes. The extension to Horn sentences is trivial.

## Two Lemmas on the Satisfaction Relation

This section talks the following topics:

- <u>Isomorphism</u> and <u>isomorphic structures</u>. The **isomorphism lemma** states that we cannot distinguish isomorphic structures using first-order sentences.
- <u>Substructures</u>, $\mathfrak{A} \subset \mathfrak{B}$. Note that $A \subset B$ and that $A$ is $S$-closed in $\mathfrak{B}$. Conversely, if $X \subset B$ and $X$ is $S$-closed in $\mathfrak{A}$,  X determines exactly one substructure, denoted as $[X]^\mathfrak{B}$ and called the <u>substructure generated by $X$ in $\mathfrak{B}$</u>.
- <u>Universal</u> and <u>existential</u> formulas.
- If $\varphi$ is universal, $\mathfrak{B} \models \varphi$ implies $\mathfrak{A} \models \varphi$, known as the **substructure lemma**. The converse holds for existential formulas.

### Exercises

#### 5.9

The idea is to exhaustively enumerate features of $\mathfrak{A} = (A, \mathfrak{a})$. The outermost levels of $\varphi_\mathfrak{A}$ should be a series of existential quantifications to bind every single element of $A$ to a name. Then there is a conjunction of in-equivalence to ensure each variable binds to a distinct element:

$$
\varphi_\mathfrak{A} = \exists v_0 \dots \exists v_n \lnot v_0 \equiv v1 \land \dots \land \lnot v_{n-1} \equiv v_n \land \varphi
$$

Pick up an arbitrary isomorphism $\pi$ from $A$ to these variables. Then, $\varphi$ should have the form of $\land_{\psi \in \Psi} \psi$ where $\Psi$ is a set including and only including:

- for each constant symbol $c \in S$, $c \equiv \pi(c^\mathfrak{A})$
- for each $n$-ary function symbol $f \in S$ and $x_1,  \dots, x_n \in A$, $f(\pi(x_1), \dots, \pi(x_n)) \equiv \pi(f^\mathfrak{A}(x_1, \dots, x_n))$
- for each $n$-ary relation symbol $R \in S$ and $x_1, \dots, x_n \in A$ such that $R^\mathfrak{A}x_1\dots x_n$, $R\pi(x_1)\dots\pi(x_n)$
- for each $n$-ary relation symbol $R \in S$ and $x_1, \dots, x_n \in A$ such that $\lnot R^\mathfrak{A}x_1\dots x_n$, $\lnot R\pi(x_1)\dots\pi(x_n)$

Technically, one should also ensure that for any $S$-structure $\mathfrak{B} = (B, \mathfrak{b})$ such that $\mathfrak{B} \models \varphi_\mathfrak{A}$, $B$ has as many element as $A$. One can use existential quantifications to introduce $n+1$ variables and make sure each does not equal to another, then negate the overall sentence. This is omitted above.

Then, for any $S$-structure $\mathfrak{B} = (B, \mathfrak{b})$ such that $\mathfrak{B} \models \varphi_\mathfrak{A}$, let’s show $\mathfrak{A} \cong \mathfrak{B}$. Clearly, there exists$a_1, \dots a_n \in A$ such that $\mathfrak{A} \models \varphi[a_1, \dots, a_n]$, and $b_1, \dots, b_n \in B$ such that $\mathfrak{B} \models \varphi[b_1, \dots, b_n]$. Define $\eta: A \to B$ as $\eta(a_i) = (b_i)$. It’s obvious that $\eta: \mathfrak{A} \cong\mathfrak{B}$.

#### 5.10

1. $\forall ab\exists c.b^2=a^2+c^2$
2. Let $\pi (x) = -x$ for all $x \in \mathbb{R}$, $+^{\pi} = +$, $0^{\pi} = 0$. Clearly $\pi$ is an automorphism. Assume there exists $\varphi$ such that for all $a, b \in \mathbb{R}$, $(\mathbb{R}, +, 0) \models \varphi[a, b]$ iff $a < b$. With isomorphism lemma we know $(\pi(\mathbb{R}), +^{\pi}, 0^{\pi}) = (\mathbb{R}, +, 0) \models \varphi[\pi(a), \pi(b)]$, yet $\pi(a) > \pi(b)$. This contradicts the assumption.

#### 5.11

The first part is omitted.

The second part. (i) and (ii) follows directly from induction hypothesis. If $(\mathfrak{A}, \beta) \models \exists x\varphi$, we get successively:

- there exists $a \in A$ such that $(\mathfrak{A}, \beta\frac{a}{x}) \models \varphi$
- there exists $a \in B$ such that $(\mathfrak{A}, \beta\frac{a}{x}) \models \varphi$
- there exists $a \in B$ such that $(\mathfrak{B}, \beta\frac{a}{x}) \models \varphi$
- $(\mathfrak{B}, \beta) \models \varphi$

