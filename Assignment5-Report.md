**SENG 438- Software Testing, Reliability, and Quality**

**Lab. Report \#5 – Software Reliability Assessment**

| Group 26         |          |                |
| ---------------- | -------- | -------------- |
| Liana Goodman    | 30089196 | LianaBG        |
| Amir Abdrakmanov | 30085827 | aabdrakmanov   |
| Jared Lundy      | 30086687 | jared840       |
| Jordan Lundy     | 30086686 | jordan427-prog |
|

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

# 3. Assessment Using Reliability Demonstration Chart
The assement done with the RDC produced varying results depending on our metrics. As shown in the 3 figures below, depending on the reliability metrics, the program may or may not be considered reliable.

![](media/2%20Failures.png)
*Figure 1: 2 Failures per 10,000 input events*

For an acceptable failure rate of 2 for every 10,000 input events, the software is clearly not reliable and should be rejected. All datapoints are firmly rooted in the *reject* zone indicating that much work still remains to be done to make the program reliable.

![](media/4%20Failures.png)
*Figure 2: 4 Failures per 10,000 input events*

For an acceptable failure rate of 4 for every 10,000 input events, the software is much more reliable and can be accepted. Though the graph varies into the *reject* zone, for the most part if has stayed in the *continue test* zone, and eventually entered the *accept* zone, indicating a positive trend. To ensure the reliability of the software, additional testing can still be done to see a more obvious trend into *accepting*.

![](media/8%20Failures.png)
*Figure 3: 8 Failures per 10,000 input events*

For an acceptable failure rate of 8 for every 10,000 input events, the software is quite clearly reliable. Though there is a brief instance of it entering the *reject* zone, it quite quickly becomes *acceptable* and stays in firmly in this zone for the rest of the data. No additional reliability data would be necessary to see that this software matches our criteria of 8/10,000.

# 4. Comparison of Results

# 5. Discussion on Similarity and Differences of the Two Techniques

# 6. How the team work/effort was divided and managed
Team work was divided into pairs to practice pair programming. Part 1 was given to Jared and Jordan while part 2 was given to Liana and Amir.

Each pair worked on the reliability testing before coming together to compare results. From here, the report was built together.

# 7. Difficulties encountered, challenges overcome, and lessons learned
In part 2, forming the charts was a little confusing when trying to find out which cells to modify and how to modify them so that the chart would appear properly. After some trial and error, we made it work.

# 8. Comments/feedback on the lab itself