**SENG 438- Software Testing, Reliability, and Quality**

**Lab. Report \#5 – Software Reliability Assessment**

| Group 26         |          |                |
| ---------------- | -------- | -------------- |
| Liana Goodman    | 30089196 | LianaBG        |
| Amir Abdrakmanov | 30085827 | aabdrakmanov   |
| Jared Lundy      | 30086687 | jared840       |
| Jordan Lundy     | 30086686 | jordan427-prog |

**Table of Contents**
1. [Introduction](#1-introduction)
2. [Assessment Using Reliability Growth Testing](#2-assessment-using-reliability-growth-testing)
3. [Assessment Using Reliability Demonstration Chart](#3-assessment-using-reliability-demonstration-chart)
4. [Comparison of Results](#4-comparison-of-results)
5. [Discussion on Similarity and Differences of the Two Techniques](#5-discussion-on-similarity-and-differences-of-the-two-techniques)
6. [How the team work/effort was divided and managed](#6-how-the-team-workeffort-was-divided-and-managed)
7. [Difficulties encountered, challenges overcome, and lessons learned](#7-difficulties-encountered-challenges-overcome-and-lessons-learned)
8. [Comments/feedback on the lab itself](#8-commentsfeedback-on-the-lab-itself)

# 1. Introduction
This lab looks at reliability testing of a program given failure data and a multitude of testing tools. In particular, we are looking at *reliability growth testing* and *reliability assesment using reliability demonstration chart*.

This lab also provides the opportunity to compare different reliability assessments to inspect the pros and cons of each and improve future decisions on tool usage.

# 2. Assessment Using Reliability Growth Testing 

The first step taken using the Reliability Growth Testing (vis SFRAT tool) was to plot all the models on all the 
covariates to get an overall view before further analysis. The Covariates tested were: E, F, C. The models were:
  - IFR Salvia & Bollinger
  - IFR Generalized Salvia & Bollinger
  - S Distribution
  - Discrete Weibull (Order 2)
  - Discrete Weibull (Type III)
  - Geometric
  - Negative Binomial (order 2)
  - Truncated Logistic <br />
The overall plot is observed below:

![](media/exported_part1_allmodels.png) 

The initial failure intensity was also plotted with these models as such:
![](media/failureIntensity_initial.PNG)

## Model Comparison 

The models were then compared based on their best fit using the model comaprison tool in C-SFRAT with equal metric weights (of 1.0 each) for LLF,AIC,BIC,SSE.
![](media/ModelComparisons.PNG)
The picture shows the models that have a critic of 1.0 or very close to 1.0 and therefore any choice of these models is good to use for our data. Specifically, the discrete weibull type 3 on covariate F has a 1.0 critic for mean and median and therefore is the best model to use for our data based on the model comparison. All other ran models had at most 0.99 Critic and thus were not as strong models according to the comparison tool.
Therefore, the two best models to be selected are: Discrete Weibull type III (DW3 on F), with a critic of 1.0, and any of the critics of 0.99 as the other. 
<br /> **So DW3(F) and Geometric (GM(F)) were selected as the top two models.**

## Range Analysis

<br />
Following the comparison of models, range analysis using laplace test or an equivalent method was to be used to determine the permissible, useful range of data to 
be used. Ideally, a laplace test would be run within the C-SFRAT application to determine what range of data is valid to use, and if the laplace test demonstrates 
reliabilitiy growth. However, since C-SFRAT was the only tool that was able to work for our group, we were limited to the functionalities of the C-SFRAT tool. 
As a result, since C-SFRAT has no range analysis or laplace test capabilities, it was impossible to perform such a test, and thus the entire range of failure
data must be treated as valid (since no rigorous test available). Thus, interval 0-32 given is treated as valid and thus the range of useful data for our testing (as limited by the provided C-SFRAT tool for the lab).
<br /> Ideally, a laplace test would be ran within the tool that would show the laplace plot. Any range for the data above +2 would be considered reliability decrease
, while any value below -2 for the laplace would be increasing reliability (and any reliability model may be used). 
In between, any value between -2 and +2 would be classified as stable reliability. Most importantly, any data where the laplace value is greater than -2 should be 
omitted in the range.
As previously mentioned, however, this is not possible with the tool provided in the lab that worked for our group, CSFRAT, and such the interval should remain
unchanged (assumed laplace >=-2).

## CSFRAT Plots

<br /> Next, the plots available in C-SFRAT were created using the best model selected previously. The two plots available via the tool are: fails/time-interval
and failure intensity per interval. Again, we were limited by the functionality of the tool provided for the lab, and as such these are the only graphs available
by the tool to be analyzed.
The following two figures are the failures per interval graph using the best model (DW3 on F) and the failure intensity using the best model(DW3 onF) <br />
![](media/failsperinterval_dw3.PNG)
![](media/failureintensity_DW3.PNG)

<br /> The first plot plots the failure number versus the time interval. As seen in the plot, it increases until we hit the end of the testing interval. From here, it 
is difficult to comment on reliability growth since it does not appear to plateau as the interval increases.
As a result, the predictive tool of C-SFRAT was used to verify whether the failures plateaued as the time intervals increased beyond the testing interval given.
The first plot was taken for double the testing interval, ie. 33 additional intervals:
![](media/FailsInterval33Predicted.PNG)
And the second plot was taken for the maximum additional interval to verify the results (99 additional intervals):
![](media/99_predicted.PNG)

The first of these graphs show a relatively declining or plateauing curve (in terms of the line of best fit). This indicates reliability growth, since the amounts
of failures starts to happen less and less as time increases. The second graph confirms this, as it shows a much less steep curve going to 99 additional intervals. 
Therefore, the system does exhibit some reliability growth, as the failures over time intervals is predicted by C-SFRAT to be plateauing.

## Discussion on decision making for target failure intensity
Due to the limitations of the CFRAT tool, we will do discussion on the decision making of a target failure intensity, rather than a failure rate. SFRAT doesn't have a failure rate plot, but it does have a failure intensity, which we can analyze.

The second graph plots the failure intensity with the default target failure intensity of 1.0 (default to C-SFRAT tool). From this plot it appears that the failure 
intensity is quite large and does not show promise in hitting the 1.0 target. Thus, adjusting and additional testing is needed, or features must be deferred until 
later. 
Adjusting the target failure intensity to half of the default (0.5) was plotted as such:
![](media/FailureIntensity_Target0.5.PNG)
C-SFRAT thus indicates that the software will reasonably hit the new target failure intensity rate of 0.5, using the predictive tool of C-SFRAT. Specifically, 
C-SFRAT indicates that the system will hit the target failure intensity rate at an interval of 52. Note, however, that this only occurs after the original testing
intervals is finished, but the trend appears close enough (decreasing close to the target) immediately after the 32 initial intervals. Thus, it reasonably meets
the 0.5 target.
<br />
Thus, based on a relatively high failure target intensity rate, the system under test does not appear to meet the threshold based on the failure intensity plot. 
However, for lower values for the target failure intensity rate, the system does appear to reasonably hit the target based on C-SFRAT's predictions. Therefore, a range
around 0.5 or lower for the target failure intensity rate is sufficient, while anything near 1.0 or above is too large.

## Advantages and Disadvantages of Reliability Growth Analysis
One advantage of reliability growth analysis is the number of models available to analyze. For example, logarithmic Poisson, Geometric, Discrete Weibull, etc. 
This provides us with many models to compare, contrast and analyze our data to find specifically how reliable our system is. 
One disadvantage of reliability growth testing is the differences in the models. For example, basic exponential is optimistic, while Poisson is pessimistic when
estimating the lamba/lambdaF ratio. This may cause an issue if these models are very different from eachother, as they could contradict eachother and lead to confusion
rather than reliability evidence for data.
Another advantage of reliability growth analysis is that it helps to estimate when to release a product (based on reliability) and to estimate the required fixes to 
reach an optimal reliability growth. 
A disadvantage of reliability growth analysis is also the best fit for the models determination, which can be very difficult if no tools are available, and using
a model that doesn't have the best fit is suboptimal for analysis purposes.
Another advantage is that it measures and plots improvements in the system over time, which helps to guide testing for the project, as well as release scheduling.
Overall, the main advantage of reliability growth testing is it allows us to measure the trend of reliability with the system (does it display growth?), and lets us 
know whether additional testing or deferring should be done (if no growth observed). It provides an easy to observe decision based on if the data shows reliability
growth or not, and then allows developers to make an informed decision on the release of the system based on its growth.



# 3. Assessment Using Reliability Demonstration Chart
The assement done with the RDC produced varying results depending on our metrics. As shown in the 3 figures below, depending on the reliability metrics, the program may or may not be considered reliable.

![](media/2%20Failures.png)
*Figure 1: 2 Failures per 10,000 seconds*

For an acceptable failure rate of 2 for every 10,000 seconds, the software is clearly not reliable and should be rejected. All datapoints are firmly rooted in the *reject* zone indicating that much work still remains to be done to make the program reliable.

![](media/4%20Failures.png)
*Figure 2: 4 Failures per 10,000 seconds*

For an acceptable failure rate of 4 for every 10,000 seconds, the software is much more reliable and can be accepted. Though the graph varies into the *reject* zone, for the most part if has stayed in the *continue test* zone, and eventually entered the *accept* zone, indicating a positive trend. To ensure the reliability of the software, additional testing can still be done to see a more obvious trend into *accepting*. This MTTF was chosen because it is reasonable based on the data, the RDC reamins mostly in the continue testing range and the other two graphs show the affects very clearly of halfing and doubling it. 

![](media/8%20Failures.png)
*Figure 3: 8 Failures per 10,000 seconds*

For an acceptable failure rate of 8 for every 10,000 seconds, the software is quite clearly reliable. Though there is a brief instance of it entering the *reject* zone, it quite quickly becomes *acceptable* and stays in firmly in this zone for the rest of the data. No additional reliability data would be necessary to see that this software matches our criteria of 8/10,000.

# 4. Comparison of Results
For the RDC the software is acceptable if the failure rate is 4 per 10,000 seconds or higher. Other wise this software is unacceptable. Similarily, for reliability growth analysis, the software will be come acceptable at failure intesity of 0.5, any higher will mean that the software is unacceptable for release. Though both of these methods provide different kinds of results, we can see from both that depending on our minimal tolerance for error, the software can be accepted.

# 5. Discussion on Similarity and Differences of the Two Techniques
Both of these techniques are used to understand the reliablility of the system using failure data. Using RDC, the system can be analyzed upto the lastest failure and whether or not the system needs more testing, whereas using reliability growth analysis the trend of the system's relability can be determined and whether or not this is an acceptable goal given the failure data. 

# 6. How the team work/effort was divided and managed
Team work was divided into pairs to practice pair programming. Part 1 was given to Jared and Jordan while part 2 was given to Liana and Amir.

Each pair worked on the reliability testing before coming together to compare results. From here, the report was built together.

# 7. Difficulties encountered, challenges overcome, and lessons learned
For part 1, the actual tool softwares provided for the lab was a challenge. STRAT was not runnable for its part one functionality, and we had to resort to C-SFRAT
instead. C-SFRAT was limited, however, in its graphical displays for part one. Specifically, C-SFRAT does not support a Time-Between-Failures graph, or a reliability
plot, and thus could not be included in the report. Additionally, C-SFRAT does not provide a laplace test functionality, so this part of part one was also omitted
from our report. Since C-SFRAT was the only tool that worked for part one, we were limited to only C-SFRAT's functionalities, which resulted in us having to omit
the functionalities (Laplace Test), and graphs (Time between failures and Reliability) since C-SFRAT did not support them.

In part 2, forming the charts was a little confusing when trying to find out which cells to modify and how to modify them so that the chart would appear properly. After some trial and error, we made it work.

# 8. Comments/feedback on the lab itself
One comment regarding this lab was the limitations the provided tools caused for part one. Part one is limited by the functionality of the tools provided. For example,
since C-SFRAT was the tool that worked for part one, we were limited to the graphs and functions of this tool, which unfortunately did not include laplace tests
and reliability graph, for example. 
