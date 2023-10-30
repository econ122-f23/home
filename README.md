Course schedule for ECON 122 (F23)
================

Michael Gelman (<mgelman@cmc.edu>), Claremont McKenna College

Office hours:

- Mo/We 1:00-2:00 PM Bauer 216

Tutor sessions:

- **Mo 08:00-10:00 PM (BC 24)** - Jen Lim
- **We 08:00-10:00 PM (BC 22)** - Abizer Mamnoon


Textbook 1: [Modern Data Science with R](https://mdsr-book.github.io/) (1st edition)  
Textbook 2: [An Introduction to Statistical Learning](https://link.springer.com/book/10.1007/978-1-4614-7138-7)

-   [Syllabus](ECON122_F2023_DataScience_StatisticalLearning.pdf)
-   [GitHub reference quick guide](https://github.com/econ122-f23/github-classroom-for-students)
-   [GitHub reference full guide ](https://happygitwithr.com/index.html)
-   Additional free resource: [R for Data Science](http://r4ds.had.co.nz/)

[This week](#currentweek)
------------------------------------------------------------------------
### Assignments due

- [Test assignment](https://classroom.github.com/a/c6lpvr3V) (due **09/01**) 
- [Problem Set 1](https://classroom.github.com/a/6XoT-RdY) (due **09/11**)
  - Solutions [.Rmd](PS/PS1-solution.Rmd) [.md](PS/PS1-solution.md)
- [Problem Set 2](https://classroom.github.com/a/ndYeKIXF) (due **09/22**)
  - Solutions [.Rmd](PS/PS2-solution.Rmd) [.md](PS/PS2-solution.md)
- [Team Project 1](https://classroom.github.com/a/K62vxRzC) (due **09/27**)
  - Example [.md](PS/Team-Project-1.md)
- [Problem Set 3](https://classroom.github.com/a/g9mbGLHa) (due **10/04**)
  - Solutions [.Rmd](PS/PS3-solution.Rmd) [.md](PS/PS3-solution.md)
- [Problem Set 4](https://classroom.github.com/a/wjWMNFm6) (due **10/09**)
  - Solutions [.Rmd](PS/PS4-solution.Rmd) [.md](PS/PS4-solution.md)
- [Problem Set 5](https://classroom.github.com/a/hKb4xybW) (due **11/10**)
- [Team Project 2](https://classroom.github.com/a/I0xMnmkh) (due **11/20**) [[Description]](https://github.com/econ122-f23/teamproject2)
- [Problem Set 6](https://classroom.github.com/a/AmBx7PPT) (due **11/27**)
- [Final Project]() (due **12/15**) [[Description]](FinalProject.md)

------------------------------------------------------------------------
### Week 1 (08/28)

**Monday** (intro, GitHub, test assignment) 
-   before class:
    - Try to set up R, RStudio, Git, GitHub account (See [GitHub reference quick guide](https://github.com/econ122-f23/github-classroom-for-students) and See [GitHub reference full guide](https://happygitwithr.com/index.html))
-   in class: 
    -   day 1 slides: [.Rmd](docs/day1_IntroSlides.Rmd) [.html](https://econ122-f23.github.io/home/day1_IntroSlides.html)
    -   continue setting up software
    -   [test assignment](https://classroom.github.com/a/c6lpvr3V)

**Wednesday** (reproducibility, R Markdown)
-   before class:
    -   complete test assignment and push **both** .rmd and .md files to GitHub.
    -   read MDSR Chapter 1 and Appendix D
    -   Start looking at PS 1
-   in class: 
    -   day 2 slides: [.Rmd](docs/day2_RMarkdownSlides.Rmd) [.html](https://econ122-f23.github.io/home/day2_RMarkdownSlides.html)
    -   day 2 activity: [.Rmd](activities/day2_MarkdownActivity.Rmd) [.md](activities/day2_MarkdownActivity.md)
    
------------------------------------------------------------------------
### Week 2 (09/04)

**Monday** 

- Labor day!!

**Wednesday** (R objects, R functions)

-   before class:
    -   read MDSR Appendix sections B.4, B.5 and C.2
    -   read Grolemund/Wickham sections [20.2 Vector Basics](http://r4ds.had.co.nz/vectors.html#vector-basics), [20.3 Types of Vectors (focus on logical, numeric)](http://r4ds.had.co.nz/vectors.html#important-types-of-atomic-vector), and [20.5 Lists](http://r4ds.had.co.nz/vectors.html#lists)
    -   Reminder: PS 1 due on Monday
-   in class: 
    -   day 3 slides [.Rmd](docs/day3_RObjectsSlides.Rmd) [.html](https://econ122-f23.github.io/home/day3_RObjectsSlides.html)
    -   day 3 activity: [.Rmd](activities/day3_RObjectsActivity.Rmd) [.md](activities/day3_RObjectsActivity.md)
        -  solutions: [.Rmd](activities/solutions/day3_RObjectsActivity_Solution.Rmd) [.md](activities/solutions/day3_RObjectsActivity_Solution.md)

------------------------------------------------------------------------
### Week 3 (09/11)

**Monday** (`ggplot2` graphics)

-   before class:
    -   read MDSR sections 3.1 and 3.2. Section 3.3 contains some `dplyr` work that I will save for discussion in chapter 4.
    -   read Grolemund/Wickham [sections 3.1 - 3.5](http://r4ds.had.co.nz/data-visualisation.html)    
-   in class: 
    -   day 4 slides: [.Rmd](docs/day4_ggplotSlides.Rmd) [.html](https://econ122-f23.github.io/home/day4_ggplotSlides.html)
    -   day 4 activity: [.Rmd](activities/day4_ggplotActivity.Rmd) [.md](activities/day4_ggplotActivity.md)
        -  solutions: [.Rmd](activities/solutions/day4_ggplotActivity_solution.Rmd) [.md](activities/solutions/day4_ggplotActivity_solution.md)

**Wednesday** (more `ggplot2` and interactive graphics)

-   before class:
    -   little more ggplot: read Grolemund/Wickham [sections 3.6 - 3.10](http://r4ds.had.co.nz/data-visualisation.html)
    -   just read pages 324-325 in MDSR to get a feel for map projections. For now we will just be working with simple maps that only need lat/long and build-in map boundaries.
    -   quick read MDSR sections 11.1-11.3 in chapter 11 to get a "big picture" idea of some of the interactive graphing options in R.
    -   Start on PS 2 
-   in class: 
    -   discuss [team project 1](https://github.com/econ122-f23/teamproject1)
    -   day 5 slides: [.Rmd](docs/day5_moreggplotsSlides.Rmd) [.html](https://econ122-f23.github.io/home/day5_moreggplotsSlides.html)
    -   day 5 interactive graphics slides: [.Rmd](docs/day5_IntroInteractive.Rmd) 
    -   day 5 activity: [.Rmd](activities/day5_ggplotActivity_2.Rmd) [.md](activities/day5_ggplotActivity_2.md)
        -  solutions: [.Rmd](activities/solutions/day5_ggplotActivity_2_solution.Rmd) [.md](activities/solutions/day5_ggplotActivity_2_solution.md)

------------------------------------------------------------------------
### Week 4 (09/18)

**Monday** (Introduction to `dplyr`)

-   before class:
    -   read MDSR sections 4.1 and 4.2
-   in class: basic data wrangling with `dplyr`
    -   day 6 slides: [.Rmd](docs/day6_DataWrangling1Slides.Rmd) [.html](https://econ122-f23.github.io/home/day6_DataWrangling1Slides.html)
    -   day 6 activity: [.Rmd](activities/day6_DataWrangling1Activity.Rmd) [.md](activities/day6_DataWrangling1Activity.md)
        -  solutions: [.Rmd](activities/solutions/day6_DataWrangling1Activity_Solution.Rmd) [.md](activities/solutions/day6_DataWrangling1Activity_Solution.md)
        

**Wednesday** (Work on Team Project 1)

-   before class:
    -   Make sure you have your Team Project 1 partners
-   in class: 
    -   Work with partners on Team Project 1
    -   Ask any questions related to material up to this point

------------------------------------------------------------------------
### Week 5 (09/25)

**Monday** (Joins in `dplyr`)

-   before class:
    -   read MDSR section 4.3 and 4.4
    -   get started with PS 3
-   in class:
    -   day 7 slides: [.Rmd](docs/day7_DataWrangling2Slides.Rmd)  [.html](https://econ122-f23.github.io/home/day7_DataWrangling2Slides.html)
    -   day 7 activity: [.Rmd](activities/day7_DataWrangling2Activity.Rmd) [.md](activities/day7_DataWrangling2Activity.md)
          - solutions: [.Rmd](activities/solutions/day7_DataWrangling2Activity_Solution.Rmd) [.md](activities/solutions/day7_DataWrangling2Activity_Solution.md)
    
**Wednesday** (Data intake)

-   before class
    -   read MDSR sections 5.5.3 and 5.5.4 (we'll come back to the other sections after the exam)
    -   read Grolemund/Wickham [chapter 16](http://r4ds.had.co.nz/dates-and-times.html#introduction-10) - focus on sections 16.2 and 16.3.
-   in class
    -   day 8 slides: [.Rmd](docs/day8_DataIntakeSlides.Rmd) [.html](https://econ122-f23.github.io/home/day8_DataIntakeSlides.html)
    -   day 8/9 activity: [.Rmd](activities/day0809_TidyDataActivity.Rmd) [.md](activities/day0809_TidyDataActivity.md)
          - solutions: [.Rmd](activities/solutions/day08_TidyDataActivity_Solution.Rmd) [.md](activities/solutions/day08_TidyDataActivity_Solution.md)
------------------------------------------------------------------------
### Week 6 (10/02) 

**Monday** (`tidy` data: reshaping with `gather` and `spread`)

-   before class:
    -   read MDSR sections 5.1-5.3
-   in class:
    -   [exam explanation](exam1.md)
    -   day 9 slides: [.Rmd](docs/day9_TidyDataSlides.Rmd) [.html](https://econ122-f23.github.io/home/day9_TidyDataSlides.html)
    -   continue day 8/9 activity
          - solutions: [.Rmd](activities/solutions/day0809_TidyDataActivity_Solution.Rmd) [.md](activities/solutions/day0809_TidyDataActivity_Solution.md)

**Wednesday** (Strings and regular expressions)

-   before class:
    -   read Grolemund/Wickham [chapter 14](http://r4ds.had.co.nz/strings.html) on strings and regular expressions
    -   finish up homework 4 - due Monday
        -   to tackle problem 4 Q2, make sure to review the `lubridate` examples in the day 8 slides and [WG section 16.2.2](http://r4ds.had.co.nz/dates-and-times.html#from-individual-components).
-   in class: 
    -   day 10 slides: [.Rmd](docs/day10_StringsSlides.Rmd) [.html](https://econ122-f23.github.io/home/day10_StringsSlides.html)
    -   day 10 activity: [.Rmd](activities/day10_stringsActivity.Rmd) [.md](activities/day10_stringsActivity.md)
        - solutions: [.Rmd](activities/solutions/day10_stringsActivity_Solution.Rmd) [.html](https://econ122-f22.github.io/home/day10_stringsActivity_Solution.html)
        
------------------------------------------------------------------------
### Week 7 (10/09)
        
**Monday** (Iteration)
-   before class:
    -   read MDSR section 5.4
-   in class:
    -   day 11 slides: [.Rmd](docs/day11_IterationsSlides.Rmd)  [.html](https://econ122-f23.github.io/home/day11_IterationsSlides.html)
    -   day 11 activity: [.Rmd](activities/day11_IterationActivity.Rmd) [.md](activities/day11_IterationActivity.md)
        - solutions: [.Rmd](activities/solutions/day11_IterationActivity_Solution.Rmd) [.md](activities/solutions/day11_IterationActivity_Solution.md)

**Wednesday**
-   before class:
    -   study for exam 1
-   in class:
    -   take [exam 1](MT1_scores.md)

------------------------------------------------------------------------
### Week 8 (10/16)

**Monday**
  - Fall Break!!
  
**Wednesday** (Statistical Learning)
-   before class:
    -   read [ISLR](https://link.springer.com/book/10.1007/978-1-4614-7138-7) section 2.1-2.2, 3.1
-   in class:
    -   day 12 slides: [.Rmd](docs/day12_StatLearning.Rmd)  [.html](https://econ122-f23.github.io/home/day12_StatLearning.html)
    -   day 12 activity: [.Rmd](activities/day12_StatLearningActivity.Rmd) [.md](activities/day12_StatLearningActivity.md)
        - solutions: [.Rmd](activities/solutions/day12_StatLearningActivity_Solution.Rmd) [.md](activities/solutions/day12_StatLearningActivity_Solution.md)

------------------------------------------------------------------------
### Week 9 (10/23)

**Monday** (Intro to Classifiers)

-   before class:  
    -  Read ISLR section 4.1-4.2
    -  Read [this](https://www.dataschool.io/simple-guide-to-confusion-matrix-terminology/) article explaining what a confusion matrix is
    -  Read [this](https://towardsdatascience.com/accuracy-recall-precision-f-score-specificity-which-to-optimize-on-867d3f11124) helpful article on evaluating classification models
-   in class:
    -   day 13 slides: [.Rmd](docs/day13_IntroClassifiers.Rmd)  [.html](https://econ122-f23.github.io/home/day13_IntroClassifiers.html)
    -   day 13 activity: [.Rmd](activities/day13_IntroClassifiersActivity.Rmd) [.md](activities/day13_IntroClassifiersActivity.md)
         - solutions: [.Rmd](activities/solutions/day13_IntroClassifiersActivity_Solution.Rmd) [.md](activities/solutions/day13_IntroClassifiersActivity_Solution.md)

**Wednesday** (Logistic regression)
-   before class:
    -   Read ISLR section 4.3
    -   Read MDSR section 8.4.4 on ROC curves
-   in class:
    -   day 14 slides: [.Rmd](docs/day14_LogisticRegressionSlides.Rmd)  [.html](https://econ122-f23.github.io/home/day14_LogisticRegressionSlides.html)
    -   day 14 activity: [.Rmd](activities/day14_LogisticRegressionActivity.Rmd) [.md](activities/day14_LogisticRegressionActivity.md)
         - solutions: [.Rmd](activities/solutions/day14_LogisticRegressionActivity_Solution.Rmd) [.md](activities/solutions/day14_LogisticRegressionActivity_Solution.md)

------------------------------------------------------------------------
### <a name="currentweek"></a>Week 10 (10/30)       

**Monday** (Cross Validation)
-   before class:
    - Read ISLR section 5.1
    - Read MDSR section 8.4.1 (10.3.2)
    - Read [this blog](https://www.r-bloggers.com/whats-the-difference-between-machine-learning-statistics-and-data-mining/) on statistical learning vs. machine learning
-   in class:
    -   day 15 slides: [.Rmd](docs/day15_CrossValidationSlides.Rmd)  [.html](https://econ122-f23.github.io/home/day15_CrossValidationSlides.html)
    -   day 15 activity: [.Rmd](activities/day15_CrossValidationActivity.Rmd) [.md](activities/day15_CrossValidationActivity.md)
        - solutions: [.Rmd](activities/solutions/day15_CrossValidationActivity_Solution.Rmd) [.md](activities/solutions/day15_CrossValidationActivity_Solution.md)
        
**Wednesday** 
  - No class: Professor going to conference to present research

------------------------------------------------------------------------
### Week 11 (11/06)

**Monday** (Decision Trees)

-   before class:
    - Read MDSR section 8.2.1-8.2.3 (11.1.1)
    - Read ISLR section 8.1
-   in class:
    -   quick note on [TeamProject2](https://github.com/econ122-f22/teamproject2)
    -   day 16 slides: [.Rmd](docs/day16_DecisionTreeSlides.Rmd)  [.html](https://econ122-f23.github.io/home/day16_DecisionTreeSlides.html)
    -   day 16 activity: [.Rmd](activities/day16_DecisionTreeActivity.Rmd) [.md](activities/day16_DecisionTreeActivity.md)
        - solutions: [.Rmd](activities/solutions/day16_DecisionTreeActivity_Solution.Rmd) [.md](activities/solutions/day16_DecisionTreeActivity_Solution.md)
        
**Wednesday** (Other classifiers)

-   before class:
    - Read MDSR section 8.2.4-8.2.5 (11.1.2-11.1.3)
    - Read ISLR section 2.2.3 (`k-nn`), 8.2.1-8.2.2 (`bagging\random forest`)
-   in class:
    -   day 17 slides: [.Rmd](docs/day17_OtherClassifiersSlides.Rmd)  [.html](https://econ122-f23.github.io/home/day17_OtherClassifiersSlides.html)
    -   day 17 activity: [.Rmd](activities/day17_OtherClassifiersActivity.Rmd) [.md](activities/day17_OtherClassifiersActivity.md)
        - solutions: [.Rmd](activities/solutions/day17_OtherClassifiersActivity_Solution.Rmd) [.md](activities/solutions/day17_OtherClassifiersActivity_Solution.md)

------------------------------------------------------------------------
### Week 12 (11/13)

**Monday** (k-means clustering)
-   before class:
    - Read ISLR section 10.3-10.3.1
    - Read MDSR section 9.1,9.1.2 (12.1,12.1.2)
-   in class:
    -   day 18 slides: [.Rmd](docs/day18_KmeansClusteringSlides.Rmd)  [.html](https://econ122-f23.github.io/home/day18_KmeansClusteringSlides.html)
    -   day 18 activity: [.Rmd](activities/day18_KmeansClusteringActivity.Rmd) [.md](activities/day18_KmeansClusteringActivity.md)
        - solutions: [.Rmd](activities/solutions/day18_KmeansClusteringActivity_Solution.Rmd) [.md](activities/solutions/day18_KmeansClusteringActivity_Solution.md)


**Wednesday** (Hierarchical clustering)
-   before class:
    - Read ISLR section 10.3.2 
    - Read MDSR section 9.1.1 (12.1.1)
-   in class:
    -   day 19 slides: [.Rmd](docs/day19_HierarchicalClusteringSlides.Rmd)  [.html](https://econ122-f23.github.io/home/day19_HierarchicalClusteringSlides.html)
    -   day 19 activity: [.Rmd](activities/day19_HierarchicalClusteringActivity.Rmd) [.md](activities/day19_HierarchicalClusteringActivity.md)
        - solutions: [.Rmd](activities/solutions/day19_HierarchicalClusteringActivity_Solution.Rmd) [.md](activities/solutions/day19_HierarchicalClusteringActivity_Solution.md)

------------------------------------------------------------------------

### Week 13 (11/20)

**Monday** (Networks Intro)
-   before class:
    - Read MDSR section 16.1-16.2 (20.1,20.2)
-   in class:
    -   [Final project proposal](FinalProject.md)
    -   [exam 2 explanation](exam2.md)
    -   day 20 slides: [.Rmd](docs/day20_NetworkGraphsSlides.Rmd)  [.html](https://econ122-f22.github.io/home/day20_NetworkGraphsSlides.html)
    -   day 20 activity: [.Rmd](activities/day20_NetworkGraphsActivity.Rmd) [.md](activities/day20_NetworkGraphsActivity.md)
         - solutions: [.Rmd](activities/solutions/day20_NetworkGraphsActivity_Solution.Rmd) [.md](activities/solutions/day20_NetworkGraphsActivity_Solution.md)

**Wednesday** (Thanksgiving!)
-  Prepare Thanksgiving meal
-  Eat Thanksgiving meal
-  Sleep

------------------------------------------------------------------------
### Week 14 (11/27)

**Monday** (Networks Statistics)
-   before class:
    -   Finish up `PS6`
-   in class:
    -   [Team Project 2 results](projects/results.csv)
          - [past results](projects/results_2021.csv)
    -   Discuss `Final Project` proposals
    -   day 21 slides: [.Rmd](docs/day21_NetworkStatsSlides.Rmd)  [.html](https://econ122-f23.github.io/home/day21_NetworkStatsSlides.html)
    -   day 21 activity: [.Rmd](activities/day21_NetworkStatsActivity.Rmd) [.md](activities/day21_NetworkStatsActivity.md)
         - solutions: [.Rmd](activities/solutions/day21_NetworkStatsActivity_Solution.Rmd) [.md](activities/solutions/day21_NetworkStatsActivity_Solution.md)

**Wednesday** (Exam 2)
-   before class:
    -   study for exam 2
    -   bring a calculator
-   in class:
    -   take [exam 2]
    
------------------------------------------------------------------------  

### Week 15 (12/04)

**Monday** (Networks Activity)
-   before class 
    -   read MDSR 16.3 and 16.4 (20.3,20.4)
    -   read [this article](https://www.maa.org/sites/default/files/pdf/Mathhorizons/NetworkofThrones%20%281%29.pdf) on the Game of Thrones network
-   in class
    -   day 22 slides: [.Rmd](docs/day23_NetworkGoTSlides.Rmd)  [.html](https://econ122-f23.github.io/home/day22_NetworkGoTSlides.html)
    -   day 22 activity: [.Rmd](activities/day22_GoTActivity.Rmd) [.md](activities/day22_GoTActivity.md)
           - solutions: [.Rmd](activities/solutions/day22_GoTActivity_Solution.Rmd) [.md](activities/solutions/day22_GoTActivity_Solution.md)

**Wednesday** (Work on Final Project)
-   before class:
    -   Start to make progress on Final Project
-   in class: 
    -   Work with partners on Final Project
    -   Fill out evaluations
    -   Celebrate end of classes!! 
