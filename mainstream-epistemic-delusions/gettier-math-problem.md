# Gettier is a math problem

## 1. The idea of knowledge as a justified true belief

Knowledge is defined as a justified true belief (JTB):

* A particular belief happens to be true
* You believe that it is true
* You can justify that it is true

In that case, this belief is knowledge.

https://en.wikipedia.org/wiki/Belief#Justified_true_belief


## 2. What is the Gettier problem?


The JTB account holds that knowledge is equivalent to justified true belief.

https://en.wikipedia.org/wiki/Gettier_problem

Gettier attempts to illustrate by means of two counterexamples that there are cases where individuals can have a justified, true belief regarding a claim but still fail to know it because the reasons for the belief, while justified, turn out to be false. Thus, Gettier claims to have shown that the JTB account is inadequate; that it does not account for all of the necessary and sufficient conditions for knowledge. 

## 3. Gettier examples

### 3.1 The "job and 10 coins" example

Suppose that Smith and Jones have applied for a certain job. And suppose that Smith has strong evidence for the following conjunctive proposition: (d) Jones is the man who will get the job, and Jones has ten coins in his pocket. Smith's evidence for (d) might be that the president of the company assured him that Jones would, in the end, be selected and that he, Smith, had counted the coins in Jones's pocket ten minutes ago. Proposition (d) entails: (e) The man who will get the job has ten coins in his pocket. Let us suppose that Smith sees the entailment from (d) to (e), and accepts (e) on the grounds of (d), for which he has strong evidence. In this case, Smith is clearly justified in believing that (e) is true. But imagine, further, that unknown to Smith, he himself, not Jones, will get the job. And, also, unknown to Smith, he himself has ten coins in his pocket. Proposition (e) is true, though proposition (d), from which Smith inferred (e), is false. In our example, then, all of the following are true: (i) (e) is true, (ii) Smith believes that (e) is true, and (iii) Smith is justified in believing that (e) is true. But it is equally clear that Smith does not know that (e) is true; for (e) is true in virtue of the number of coins in Smith's pocket, while Smith does not know how many coins are in his pocket, and bases his belief in (e) on a count of the coins in Jones's pocket, whom he falsely believes to be the man who will get the job.

### 3.2 The "Ford and Barcelona" example

Smith, it is claimed by the hidden interlocutor, has a justified belief that "Jones owns a Ford". Smith therefore (justifiably) concludes (by the rule of disjunction introduction) that "Jones owns a Ford, or Brown is in Barcelona", even though Smith has no information whatsoever about the location of Brown. In fact, Jones does not own a Ford, but by sheer coincidence, Brown really is in Barcelona. Again, Smith had a belief that was true and justified, but not knowledge.

## 4. Knowledge database formalization

(ownsFord or BrownBarcelona,ownsFord)
(ownsFord or BrownBarcelona,BrownBarcelona)

(xJob and x10coins,JonesJob and Jones10coins)
(xJob and x10coins,SmithJob and Smith10coins)

        knowledgeClaim(justification,belief)
DBTruth
    {
        ("BrownBarcelona", "ownsFord or BrownBarcelona")
    }

DBSmith
    {
        ("ownsFord", "ownsFord or BrownBarcelona")
    }

## 5. Implementation of evaluation algorithm


aDB.justifiedTrueBelief(aBelief) {
    foreach(knowledgeClaim in aDB) {
        if( (knowledgeClaim.belief==aBelief) and (knowledgeClaim.justification => knowledgeClaim.belief))
            //successful justification
            return true;
    }
    //failure to justify
    return false;
}

## 6. Evaluation results

KnowledgeDBTruth.justifiedTrueBelief("ownsFord or BrownBarcelona")
-> true

KnowledgeDBSmith.justifiedTrueBelief("ownsFord or BrownBarcelona")
-> false


## 8. What is the source of the Gettier confusion?


justifiedTrueBelief(KnowledgeDBTruth, "ownsFord or BrownBarcelona")

justifiedTrueBelief("ownsFord or BrownBarcelona")

Missing parameter. It is a two-variable predicate instead of a one-variable one.


## 9. Implementation of the incorrect algorithm

## 10. The incorrect evaluation results


## 11. Why does the bug occur?

Impossible to debug the informal specification in natural language. Write a program and you see the problem immediately.


## 7. What is a Gettier case mathematically?

normal case

                dbTruth     dbSmith

belief          true        true

justification   true        true


Gettier case

                dbTruth     dbSmith

belief          true        true

justification   true        false

## 8. Other corner cases possible

Faulty implication function + faulty justification can cancel each other

There are undoubtedly other corner cases possible

## 12. Connection between Gettier and Gödel's incompleteness


Discrepancy between two or more theories/models ==> two or more distributed databases that are not in sync (inconsistent)

Two bugs with a slightly different structure.

