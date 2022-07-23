# SUMMARY

## Category Notes
- Age-Sex-cat
    - 0 : child
    - 1 : female
    - 2 : male
- Ticket_bool
    - 0 : not 3
    - 1: 3
- Pclass
    - 1 : 1st class
    - 2 : 2nd class
    - 3 : 3rd class
- Survived
    - 0 : Did not survive
    - 1 : Survived

## Promising Correlations based on Pearson's

- Survived: Pclass and Sex
    - The plot shows that more percentage of female survived, and more female survived than male
    - 3rd class holders were more likely to die than the rest
        - More 1st class holders survived than didn't
        - For 2nd class holders, it's equal
        - Biggest percentage of survivors was from first class, but the difference was not that huge compared to third class

- Age: Pclass and ParchSibSp
    - The plot shows that 1st class holders range from 30-50, while 2nd class ranges from 25-35, and 3rd class ranges from 20-30
        - aka, ticket class tend to get higher with age
        - young people were more likely to survive, led by 26-35 yrs olds
        - Those who have 4 SibSp and above are all in 3rd class

- Sex: Pclass and ParchSibSp
    - The plot shows that all classes were dominated by male but the difference is the largest in 3rd class
    - Males were more likely to have come without ParchSibSp
        
## Feature Engineering
- Through countplot and pearson's r, I found that Parch and SibSp are correlated so I merged them into a single feature by getting their sum and putting it in a variable "ParchSibSp"
    - Furthermore, I categorized ParchSibSp into 3 categories since those with 1-3 ParchSibSp had more likelihood of survival
- No correlation was found for the variables Embarked and Ticket except that certain tickets are dominated by 1st class or 3rd class holders, thus affecting their probability of survival because of Pclass correlation with Survived
    - a lot of passengers had an unknown cabin letter but most of them are 2nd class and 3rd class
    - I've decided to drop both variables
- I tried to analyze those who had unknown cabins and by filtering it and looking at the value counts of "Survived" against different Ticket codes, I discovered that more 3rd class holders with ticket that starts with 3 died than survived (died = 215, survived = 59) so I created a variable Ticket-bool which is 1 if ticket starts with 3 and 0 if not
- Since there were no found correlation between Age and Survival (using pearson's r), I looked at the countplots and found that in all age levels, it's just the same that there were more people who didn't survive than those who survived (the only exception is the ages 0-6 who were more likely to survive). With that, it's not useful to segment them according to all the age groups. So I created a new variable MW which just categorizes them into child, male, female.
- Upon investigating the variable ParchSibSp, I found that the categories that had more likelihood of death were dominated by 3rd class and males (category 0 was dominated by males and 3rd class, category 2 was dominated by 3rd class). With that, there were no correlation found between PS_cat and survival (even in Pearson's r) so I removed the variable.
