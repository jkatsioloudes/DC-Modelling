# Summary
A symbolic model checking analysis for the Dining Cryptographers' Protocol which inspired Tor's Onion Routing based on synchronous finite-state and infinite-state systems.  In cryptography, the dining cryptographers problem studies how to perform a secure multi-party computation of the boolean-OR function. David Chaum first proposed this problem in the early 1980s and used it as an illustrative example to show that it was possible to send anonymous messages with unconditional sender and recipient untraceability. Anonymous communication networks based on this problem are often referred to as DC-nets (where DC stands for "dining cryptographers").

## The Problem
“Three cryptographers are sitting down to dinner at their favorite three- star restaurant. Their waiter informs them that arrangements have been made with the maitre d’hˆotel for the bill to be paid anonymously. One of the cryptographers might be paying for the dinner, or it might have been NSA (U.S. National Security Agency). The three cryptographers respect each other’s right to make an anonymous payment, but they wonder if NSA is paying. They resolve their uncertainty fairly by carrying out the following protocol:

Each cryptographer flips an unbiased coin behind his menu, between him and the cryptographer on his right, so that only the two of them can see the outcome. Each cryptographer then states aloud whether the two coins he can see — the one he flipped and the one his left-hand neighbor flipped — fell on the same side or on different sides. If one of the cryptographers is the payer, he states the opposite of what he sees. An odd number of differences uttered at the table indicates that a cryptographer is paying; an even number indicates that NSA is paying (assuming that the dinner was paid for only once). Yet if a cryptographer is paying, neither of the other two learns anything from the utterances about which cryptographer it is.”

## Example
In the first stage, every two cryptographers establish a shared one-bit secret, say by tossing a coin behind a menu so that only two cryptographers see the outcome in turn for each two cryptographers. Suppose, for example, that after the coin tossing, cryptographer A and B share a secret bit 1, A and C share 0, and B and C share 1.

In the second stage, each cryptographer publicly announces a bit, which is:
* if they didn't pay for the meal, the exclusive OR (XOR) of the two shared bits they hold with their two neighbours,
* if they did pay for the meal, the opposite of that XOR.

Supposing none of the cryptographers paid, then A announces 1 XOR 0 = 1, B announces 1 XOR 1 = 0, and C announces 0 COR 1 = 1.  On the other hand, if A paid, she announces NOT (1 XOR 0) = 0.

The three public announcements combined reveal the answer to their question. One simply computes the XOR of the three bits announced. If the result is 0, it implies that none of the cryptographers paid (so the NSA must have paid the bill). Otherwise, one of the cryptographers paid, but their identity remains unknown to the other cryptographers.

## What is Symbolic Model Checking
model checking or property checking refers to the following problem: Given a model of a system, exhaustively and automatically check whether this model meets a given specification. Typically, one has hardware or software systems in mind, whereas the specification contains safety requirements such as the absence of deadlocks and similar critical states that can cause the system to crash. Model checking is a technique for automatically verifying correctness properties of finite-state systems.

In order to solve such a problem algorithmically, both the model of the system and the specification are formulated in some precise mathematical language. To this end, the problem is formulated as a task in logic, namely to check whether a given structure satisfies a given logical formula. This general concept applies to many kinds of logics and suitable structures. A simple model checking problem is verifying whether a given formula in the propositional logic is satisfied by a given structure.

## This Solution
The code implemented performs exsaustive checking by approaching this problem in an Object Oriented Fashion using NuSMV.  NuSMV is a symbolic model checker developed by FBK-IRST.  It is aiming at the development of a state-of-the-art model checker that:
* is robust, open and customizable
* can be applied in technology transfer projects; can be used as research tool in different domains.
