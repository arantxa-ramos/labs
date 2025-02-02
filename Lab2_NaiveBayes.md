# Lab 2: Naive Bayes, Sentiment, and Harms of Classification (Week 3)

## Part 1: Naive Bayes review

First, form a group of 3 students to work together!

We want to build a naive bayes sentiment classifier using add-1 smoothing, as described in the lecture (not binary naive bayes, regular naive bayes). Our training and testing data consist of comments on a social media platform. Here is our training and testing corpus:

**Training Set**

    - a cat ruined my sweater
    - hate that cat
    + my friends rock

**Test Set**

    adore my cat

Answer the questions below given the sets above.

1. Compute the prior for the two classes + and -, and the likelihood for each word that appears in the test sentence given either class.

**Answer:**

        P(-) = 2/3
        P(+) = 1/3
        
        |V| = 9
        We get rid of adore, because it is not in the training set.
        
        p("my"|-) = 2/(8+9)=2/17
        p("my"|+) = 2/(3+9)=2/12
        
        p("cat"|-) = 3/(8+9)=3/17
        p("cat"|+) = 1/(3+9)=1/12

2. Then compute whether the sentence in the test set is of class positive or negative (you may need a computer for this final computation).

**Answer:**

        P(-|"adore my cat") = P(-)P("adore my cat"|-) = p(-)p("adore"|-)p("my"|-)p("cat"|-)=2/3*(2/17*3/17)=4/289=0.01384
        
        P(+|"adore my cat") = P(+)P("adore my cat"|+) = p(+)p("adore"|+)p("my"|+)p("cat"|+)=1/3*(2/12*1/12)=1/216=0.00463

3. Do you think that the predicted class is the correct sentiment of this sentence? Explain, in your own words, what about the Naïve Bayes classifier led it to the correct or incorrect answer. What assumptions made by Naïve Bayes led to this result? Identify a specific assumption and be prepared to justify.

**Answer:**

        I don't think it is correct. The training set is too small, so there is not an example of the word adore (that has a very strong positive connotation). Also, all the negative sentences in the training set are related to cat, which makes it seem as if it was a negative word. 

4. Why do you add |V| to the denominator of add-1 smoothing, instead of just counting the words in one class?

**Answer:**

        We add smoothig to having 0 probabilities that would cancel the other probabilities.

5. Suppose "cat" was a demographic attribute like "woman" or "engineer" or "Asian”. What harms from the lecture could this result in, and why?

**Answer:**

        The results we obtain are very dependant of the training set, so it is important to avoid this attributes to be related with negative.
        We will now go back to the whole class and discuss group answers for Part 1 in a plenary session.

## Part 2: Naive Bayes Toxicity Classification

For the following problem, please choose a group facilitator/representative who will also take notes on your discussion.

6. Imagine you’re working for Reddit. Toxic comments are a real problem, so you decide to build a sentiment classifier using Naive Bayes and an automoderator that deletes negative comments. Your classifier trains on these examples:

**Training Set**

    - the dangerous bears
    - bears destroyed the yard
    + beautiful redwood trees

   The week after training, the Big Game (between Stanford and Cal) happens. Users on /r/bayarea are excited. Alice, a Cal student, wants to support her team and comments `“Go bears!”`. Bob, a Stanford student, wants to support his team and comments `“Go trees!”`. Answer the following questions:

a. Is Alice’s comment deleted by your automoderator?
   
**Answer**
       
        P(-) = 2/3
        P(+) = 1/3
        |V| = 8
        We get rid of "go", because it is not in the training set.

        p("bears"|-) = 3/(7+8)=3/15
        p("bears"|+) = 1/(3+8)=1/11
        
        P(-|"go bears") = P(-)P("go bears"|-) = p(-)p("bears"|-)=2/3*3/15=2/15=0.13333
    
        P(+|"go bears") = P(+)P("go bears"|+) = p(+)p("bears"|+)=1/3*1/11=1/33=0.03030
    
        It is getting deleted.
        
b. Is Bob’s comment deleted by your automoderator?
    
**Answer:**
        
        We get rid of "go", because it is not in the training set.
        
        p("trees"|-) = 1/(7+8)=1/15
        p("trees"|+) = 2/(3+8)=2/11

        P(-|"go trees") = P(-)P("go trees"|-) = p(-)p("trees"|-)=2/3*1/15=2/15=0.04444

        P(+|"go trees") = P(+)P("go trees"|+) = p(+)p("trees"|+)=1/3*2/11=2/33=0.06060

        It is not getting deleted.

      
c. Which two groups of people is your automoderator treating differently, even though membership in these groups doesn’t have a clear connection to comment toxicity?
        
**Answer:**

        Cal students, since the word bears is related to negative sentences.
      
d. What kind of harm from the lecture is experienced by the group whose comments are getting deleted?</li>
      
  **Answer:**

      They are getting sensored.
      
  e. Having realized the harm from part (d) that your automoderator is causing, you change it so that negative comments are not deleted. Instead, they are just highlighted in red and marked “negative”. Now, what kind of harm from lecture is the aforementioned group experiencing?</li>
  
  f. You are now trying to improve the automoderator to reduce this type of harm from occurring in the future. As a group, describe 3 distinct problems in the automoderator that led to this harm.</li>
  
  g. As a group, describe a plan for how you might fix one of the problems you described in part f. If you don’t have any ideas, explain why this seems hard. For whatever question you answer, be prepared to share.</li>


   We will now go back to the whole class and discuss group answers for Part 2 in a plenary session.

## Part 3: Performance Disparities

For the last problem, please continue taking notes on your discussion.

7. Your manager at Reddit comes to you and asks you to completely scrap the Naïve Bayes sentiment classifier in the automoderation system. Instead, you are to use an entirely new, state of the art, *toxicity* classifier that is trained on the entire internet. Your manager believes this will solve all the harms introduced by the Naïve Bayes classifier. But you know otherwise. To convince your manager that things aren’t so simple, find a subreddit where harm might be more likely to occur because of a performance disparity in the general classifier and explain why. Be prepared to share. 

We will now go back to the whole class and discuss group answers for Part 3 in a final plenary session.
