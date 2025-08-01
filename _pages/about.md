---
layout: about
title: about
permalink: /
subtitle: Lecturer, <a href='https://www.liverpool.ac.uk/computer-science/'>Department of Computer Science, University of Liverpool</a>

profile:
  align: right
  image: L1008477-Edit.jpg
  image_circular: false # crops the image to make it circular
  more_info: >
    <p>Ashton Building 2.02</p>
    <p>Ashton Street</p>
    <p>Liverpool L69 3BX</p>

news: false # includes a list of news items
latest_posts: false # includes a list of the newest posts
selected_papers: false # includes a list of papers marked as "selected={true}"
social: false # includes social icons at the bottom of the page
---

My research is concerned with generalizations of the propositional satisfiability (SAT) problem. SAT is a fundamental problem in computer science and the canonical NP-complete decision problem. This means that many problems, such as finding the shortest possible round-trip visiting a number of cities, can be efficiently expressed in SAT.

Although SAT is hard to solve in the worst case, there has been significant progress in practical solving, and SAT solvers have become a standard tool in areas such as formal methods and electronic design automation. However, the increasing complexity of specifications in these domains can lead to enormous encodings that are unmanageable for even the most efficient SAT solvers.

This has prompted research into more succinct logics, such as *Quantified Boolean Formulas (QBF)*, which extend propositional logic with universal and existential quantification over the Boolean domain. Building decision procedures for QBF (and related logics) is challenging. My research aims to address some of the underlying issues. More specifically, here are some of the topics that I've worked on:

- **Variable dependencies** The nesting of universal and existential quantifiers in QBFs causes dependencies between variables. One way this manifests is that variables in QBF solvers cannot be assigned in any order. Because of this, some solvers resort to assigning variables strictly following the nesting of quantifiers. However, this is often needlessly restrictive and makes certain problems provably much harder to solve. *Dependency learning* is a technique I've developed to address this. The idea is to let solvers assign variables in an arbitrary order, and only add (temporary) constraints on the order if something goes wrong. It is implemented in the solvers [Qute](https://github.com/fslivovsky/qute) and [miniQU](https://github.com/fslivovsky/miniQU).
- **Proof logging and strategy extraction** Solvers, like any other piece of software, can contain bugs. Given that, how can we trust their results? Formal verification is usually not viable because solvers are too complex. In SAT, this has been addressed through the adoption of proof logging and validation. Solvers output proofs that can be validated by trusted checkers, which are even simple enough to be formally verified. In SAT, the [DRAT](https://www.cs.utexas.edu/~marijn/drat-trim/) format (and its variants) is the gold standard. In QBF, proof logging is more fractured. There is an analogue of DRAT, called *QRAT*, but it does not have *strategy extraction* (unless P=PSPACE), meaning that a circuit representing a strategy for QBF cannot be efficiently computed from a QRAT proof. [Leroy Chew](https://leroychew.wordpress.com/) and I have shown that a simpler proof system with strategy extraction can capture what's going on in most QBF solvers. Curiously, this result in turn uses the fact that proofs generated by these solvers allow efficient strategy extraction.
- **Unique strategy functions** Rather than running a QBF solver and computing a strategy from its proof, one can try and directly compute strategies inside a solver. That is the underlying idea of my Dependency QBF (DQBF) solver [Pedant](https://github.com/fslivovsky/pedant-solver). One of its features is that it can detect when the strategy function for a variable is unique by using a SAT solver, and compute the function by interpolation. This is also implemented in the standalone preprocessor [Unique](https://github.com/fslivovsky/unique).

