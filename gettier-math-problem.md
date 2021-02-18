# The Gettier problem as a math problem

The Gettier conundrum is about an ambiguity in the general definition of knowledge as a justified true belief.

## 1. The idea of knowledge as a Justified True Belief (JTB)

Knowledge is defined as a justified true belief (JTB):

* A particular belief happens to be true
* You believe that it is true
* You can justify that it is true

In that case, this belief satisfies the [definition of knowledge](https://en.wikipedia.org/wiki/Belief#Justified_true_belief).


## 2. What is the Gettier problem?

The JTB account holds that knowledge is equivalent to justified true belief.


[Gettier attempts](https://en.wikipedia.org/wiki/Gettier_problem) to illustrate by means of two counterexamples that there are cases where individuals can have a justified, true belief regarding a claim but still fail to know it because the reasons for the belief, while justified, turn out to be false. Thus, Gettier claims to have shown that the JTB account is inadequate; that it does not account for all of the necessary and sufficient conditions for knowledge. 

## 3. Gettier examples

### 3.1 The "job and 10 coins" example

Suppose that Smith and Jones have applied for a certain job. And suppose that Smith has strong evidence for the following conjunctive proposition: (d) Jones is the man who will get the job, and Jones has ten coins in his pocket. Smith's evidence for (d) might be that the president of the company assured him that Jones would, in the end, be selected and that he, Smith, had counted the coins in Jones's pocket ten minutes ago. Proposition (d) entails: (e) The man who will get the job has ten coins in his pocket. Let us suppose that Smith sees the entailment from (d) to (e), and accepts (e) on the grounds of (d), for which he has strong evidence. In this case, Smith is clearly justified in believing that (e) is true. But imagine, further, that unknown to Smith, he himself, not Jones, will get the job. And, also, unknown to Smith, he himself has ten coins in his pocket. Proposition (e) is true, though proposition (d), from which Smith inferred (e), is false. In our example, then, all of the following are true: (i) (e) is true, (ii) Smith believes that (e) is true, and (iii) Smith is justified in believing that (e) is true. But it is equally clear that Smith does not know that (e) is true; for (e) is true in virtue of the number of coins in Smith's pocket, while Smith does not know how many coins are in his pocket, and bases his belief in (e) on a count of the coins in Jones's pocket, whom he falsely believes to be the man who will get the job.

### 3.2 The "Ford and Barcelona" example

Smith, it is claimed by the hidden interlocutor, has a justified belief that "Jones owns a Ford". Smith therefore (justifiably) concludes (by the rule of disjunction introduction) that "Jones owns a Ford, or Brown is in Barcelona", even though Smith has no information whatsoever about the location of Brown. In fact, Jones does not own a Ford, but by sheer coincidence, Brown really is in Barcelona. Again, Smith had a belief that was true and justified, but not knowledge.

## 4. Representation of a knowledge database as a set of two-tuples

Say that knowledge is a two-tuple that consists of a claim and a justification:

```
knowledge = (claim, justification)
```
In the true-belief knowledge database, the following is always true:

```
claim ⇒ justification
```
In a personally-held belief knowledge database, this may or may not be true. The person just believes that it is true.

Say that T is the set of objectively true knowledge beliefs.

```
T = { (claim₁, justif₁), (claim₂, justif₂), ..., (claimₙ, justifₙ) } 
```

as such that:

```
justifₖ ⇒ claimₖ
```

Say that S is the set of JTB beliefs held by Smith:

```
S = { (claim₁, justif₁), (claim₂, justif₂), ..., (claimₘ, justifₘ) } 
```

Then, Smith believes that:

```
justifₖ ⇒ claimₖ
```

This may actually not always be true. Smith may be misguided.

## 5. Gettier's example 1 and 2 in the true knowledge database

*Example 1*

There exists a person who has a job and who has 10 coins:

```
claim₁ ⬄ ∃ p ∈ Persons ( has(p,job) ∧ has(p,ten_coins) )
```

Justified by the witness statement:

```
justif₁ ⬄ has(Smith,job) ∧ has(Smith,ten_coins)
```

*Example 2:*

```
claim₂ ⬄ has(Jones,Ford) ∨ isInLocation(Brown, Barcelona)
```

Justified by:

```
justif₂ ⬄ isInLocation(Brown, Barcelona)
```

Hence, T looks like this:

```
T = { 
        ( ∃ p ∈ Persons ( has(p,job) ∧ has(p,ten_coins) ),        has(Smith,job) ∧ has(Smith,ten_coins) ), 
        ( has(Jones,Ford) ∨ isInLocation(Brown,Barcelona),       isInLocation(Brown, Barcelona)         )
    }

```
or:
```
T = { 
        ( claim₁, justif₁), 
        ( claim₂, justif₂)
    }

```

Smith's set of JTB beliefs:
```
S= {
        // incorrect witness
        ( ∃ p ∈ Persons ( has(p,job) ∧ has(p,ten_coins) ),       has(Jones,job) ∧ has(Jones,10_coins)   ), 
        // incorrect option selected in justification
        ( has(Jones,Ford) ∨ isInLocation(Brown, Barcelona),      has(Jones,Ford)                        )  

    }
```
or:
```
S = { 
        ( claim₁, wrong_justif₁), 
        ( claim₂, wrong_justif₂)
    }
```
## 6. The JTB(Db,X) predicate


Define the `JTB(Db,X)` predicate as following:

```
CLAIM=1
JUSTIF=2

JTB(Db,X) ⬄ ∃ knowledge ∈ Db ( knowledge[CLAIM]=X ∧ knowledge[JUSTIF] )
```

The belief X is true justified when `JTB(T,X)` evaluates to true against the true knowledge tuples T.

The belief X is possibly true but possible also misguided when `JTB(S,X)` is evaluated against the personally-held beliefs S.

In the true knowledge database T, claim₁ and claim₂ are JTB beliefs:

```
JTB(T,claim₁)
=> true

JTB(T,claim₂)
=> true
```

However in Smith's incorrect database S, claim₁ and claim₂ are believed to be true but for the wrong reasons:

```
JTB(S,claim₁)
=> false

JTB(S,claim₂)
=> false
```


## 7. The source of the Gettier confusion

When there is a discrepancy between the true knowledge base T and the personally-held knowledge beliefs S:

```
∃ claimₓ ( JTB(T,claim) ∧ ⌐ JTB(S,claim) )
```

Then there exists at least one `claimₓ` that is justifiably true but not for the reasons personally believed. This is a Gettier case.

Smith's personally-held knowledge database contains true claims with false justifications for which there exist true justifications.


## 8. Tabular representation of the Gettier problem

T: truly justified beliefs

S: possibly misguided personally-held beliefs

```
Normal case
-----------
                T           S

belief          true        true

justification   true        true
```
versus:

```
Gettier case
-----------
                T           S

belief          true        true

justification   true        false
```

## 9. Alternative mathematical Gettier example

Say that Smith subscribes to the following personally-held knowledge belief:

```
0=1 ⇒ 2+5=7 
```

This is a Gettier problem.

Even though it is justifiably true that `2+5=7`, it is true for other reasons than because `0=1`.

## 10. Conclusion

In the personal belief of knowledge:

```
(claim, justification) = (Q, P)
```
The person truly believes that:
```
P => Q
```
However, even though `Q` is true for other reasons, his justification `P` is false.

