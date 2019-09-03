---
title: Activity 2.1
output: html_document
---

# Exploratory Data Analysis: Summarizing and Manipulating

Requirements:

- GitHub account
- RStudio Cloud account

Goals:

- Explore a data set by creating summary tables
- Explore a data set by manipulating or creating new variables
- Team collaboration using R/RStudio and GitHub

**Pick a lead**:
This person is not soley responsible for doing the activity, but they are responsible for organizing the team effort, making sure all parts are in there, etc.
This role should change during each activity so that each of you gain this experience.

**Tips**:

- Be ready to troubleshoot.
  Errors will more than likely be a knit issue.
  Read the error message carefully and take note of which line is preventing a successful knit.
- Keep track of the various code chunks and keep your text and code in the right place.
- Remember that your R Markdown document file is not aware of your project's global environment (e.g., the *Console*) and can only make use of variables, functions, etc. that you have loaded or defined in the document.
- This lab relies heavily on the pipe operator (`%>%`).
- If you are unsure of how a function works or what its arguments are, type `?` and the function in the *Console* and press enter (e.g., `?read_csv`).
  The *Help* tab will provide a summary of the function as well as some examples.

## Introduction

In this activity, we will turn information into knowledge.
We will do this by summarizing and describing the raw information - data.
Specifically, we will explore data on college majors and earnings from the data behind the FiveThirtyEight story [The Economic Guide To Picking A College Major](https://fivethirtyeight.com/features/the-economic-guide-to-picking-a-college-major/).

As we progress through this activity, remember that there are many considerations that go into picking a major.
Earning potential and employment prospects are two (important) of these considerations, but they do not tell the entire story.
Keep this in mind as we analyze the data.


### Pipes

This activity relies heavily on pipes `%>%`.
Pipes from the `magrittr` function are a way to take nested functions and make them more informative to read and write.
Consider the following "to do" statement:

> Once I find my keys, I can start my car, drive to campus, and then park.

One way to write this out is with nested functions:

```
park(drive(start_car(find(“keys”)), to = “campus”))
```

If we start in the inner-most function, we can then work our way out to see what we are trying to do.
Pipes, however, clean this up:

```
find(“keys”) %>%
  start_car() %>% 
  drive(to = "campus") %>% 
  park()

```

Writing this using pipes give the to-do statement a more natural structure.

## Getting started

These instructions will switch between every Team Member and just one of you completing steps.
When only one Team Member is completing steps, the others are expected to contribute to the discussion and help the individual member complete the step, but not actually touch the files on their computer.

1. The Lead Team Member will:
  - Go to the Documents section on [Bb](https://mybb.gvsu.edu)
  - Click on the link titled `activity0201-summarize-manipulate`
  - **Create a new team** by typing your team name (use lower-case letters for consistency) then clicking on the green button "+ Create team"
  - Once the your screen says "You are ready to go!" have all other team members follow Step 2.
2. *All other* Team Members now will:
  - Go to the Documents section on [Bb](https://mybb.gvsu.edu)
  - Click on the link titled `activity0201-summarize-manipulate`
  - Click on the "Join" button next to your corresponding team name in the **Join an existing team** section
3. *All* Team Members now will:
  - In your team repo, click the green **Clone or download** button, select "Use HTTPS" if this isn't the default option, and click on the clipboard icon to copy the repo URL
  - Go to RStudio Cloud and into the course workspace.  Create a **New Project from Git Repo** - remember that you need to click on the down arrow next to the **New Project** button to see this option.
  - Paste the URL of your activity repo into the dialogue box.
  - Click "OK".
4. *All* Team Members now will Load Packages:
  - In this lab, we will work with the `tidyverse` package so we need to install and load it.  Type the following code into your *Console*:
  
    ```
    install.packages("tidyverse")
    library(tidyverse)
    ```
    
  - Note that this package is also loaded in your R Markdown document.
5. *All* Team Members now will configure Git:
  - Go to the *Terminal* pane and type the following two lines of code, replacing the information inside the quotation marks with your GitHub account information:
  
    ```
    git config --global user.email "your email"
    git config --global user.name "your name"
    ```
    
  - Confirm that these changes have been implemented, run the following code:
  
    ```
    git config --global user.email
    git config --global user.name
    ```
    
5. *All* Team Members will now name their RStudio project:
  - Currently your RStudio project is called *Untitled Project*.  Update the name of your project to be "Activity 2-1 - Summarizing and Manipulating"
6. The Lead Team Member will do the following in RStudio:
  - Open the `.Rmd` file and update the **YAML** by changing the author name to your **Team** name and date to today, then knit the document.
  - Go to the *Git* pane and click on **Diff** to confirm that you are happy with the changes.
  - *Stage* just your Rmd file, add a commit message like "Updated team name" in the *Commit Message* dialogue box and click **Commit**
  - Click on **Push**.  This will prompt a dialogue where you first need to enter your GitHub user name, and then your password.
  - Verify that your changes have been made to your GitHub repo.
7. *All other* Team Members now will do the following in RStudio:
  - Go to the *Git* pane and click on **Pull** button
  - Observe that the changes are now reflected in their project!

**Thought Question 1**:
Why did I instruction only one Team Member edit the YAML information?

### Collaboration: merge conflicts

When collaborators make changes to a file and push the file to their repo, git merges these two files.
However, recall from Activity 1.1 that a **merge conflict** occurs when a merge has conflicting content on the same line.
We previously saw how to handle this individually, but let's explore this in a more pratical situation.

1. Every Team Member should have the activity's `.Rmd` file open.
2. Assign a number 1, 2, 3, 4, 5 (or 6 if you have 6 members) to each Team Member.
3. Take turns completing these next steps, one member at a time.
  Help each other out!
  - *Member 1*: Change the team name to your actual name.
    Knit, commit, push.
  - *Member 2*: Change the team name to some other word.
    Knit, commit, push - you should get an error.
    Pull.
    Take a look at the document with the merge conflict.
    Clear the merge conflict by choosing the correct/preferred change.
    Commit, push.
  - *Member 3*: Change the name of the first code chunk (i.e., the `load-packages` portion of `{r load-packages, message=FALSE}`).
    Knit, commit, push.
    You should get an error.
    Pull.
    No merge conflicts should occur.
    Now push.
  - *Member 4*: Add a different name to the first code chunk.
    Knit, commit, push.
    You should get an error.
    Pull.
    Take a look at the document with the merge conflict.
    Clear the merge conflict by choosing the correct/preferred change.
    Commit, push.
  - *Member 5*:  Change the "Excercise 1" header to "Exercise 01".
    Knit, commit, push.
    You should get an error.
    Pull.
    No merge conflicts should occur.
    Now push.
  - *Member 6*: Change the "Excercise 1" header to "Exercise One".
    Knit, commit, push.
    You should get an error.
    Pull.
    Take a look at the document with the merge conflict.
    Clear the merge conflict by choosing the correct/preferred change.

**Thought Question 2**:
Based on these previous tasks, what would be your recommended workflow for collaborating with git/GitHub?

## The data

These data originally come from the American Community Survey (ACS) 2010-2012 Public Use Microdata Series.
If you are curious about how the raw data from the ACS were cleaned and prepared (not a requirement), see the FiveThirtyEight author's [code](https://github.com/fivethirtyeight/data/blob/master/college-majors/college-majors-rscript.R).

### Load The data

Unlike the previous activities and your Application Task, we will read data into R from an external file - a comma separated values (CSV) file.

We will use the `read_csv` function to do this:

```
college_recent_grads <- read_csv("data/recent-grads.csv")
```

Notice that this dataset is in a folder called `data`.  We read it in with the `read_csv` function, then saved the results as a new data frame called `college_recent_grads`.
This data frame is a tidy data frame.
To view the data, you can click on the name of the data frame in the *Environment* tab.

You can also take a quick peek at the data frame and view its dimensions with the `glimpse` function:

```
glimpse(college_recent_grads)
```

**Thought Question 3**:
What is meant by **tidy data**? 
Briefly explain what a tidy data frame is, then use those characteristics to explain why `college_recent_grads` is an example of a tidy data frame.

### The data codebook

Descriptions of the variables are provided below.

| Header                        |  Description
|:----------------|:--------------------------------
|`rank`                         | Rank by median earnings
|`major_code`                   | Major code, FO1DP in ACS PUMS
|`major`                        | Major description
|`major_category`               | Category of major from Carnevale et al
|`total`                        | Total number of people with major
|`sample_size`                  | Sample size (unweighted) of full-time, year-round ONLY (used for earnings)
|`men`                          | Male graduates
|`women`                        | Female graduates
|`sharewomen`                   | Women as share of total
|`employed`                     | Number employed (ESR == 1 or 2)
|`employed_full_time`           | Employed 35 hours or more
|`employed_part_time`           | Employed less than 35 hours
|`employed_full_time_yearround` | Employed at least 50 weeks (WKW == 1) and at least 35 hours (WKHP >= 35)
|`unemployed`                   | Number unemployed (ESR == 3)
|`unemployment_rate`            | Unemployed / (Unemployed + Employed)
|`median`                       | Median earnings of full-time, year-round workers
|`p25th`                        | 25th percentile of earnings
|`p75th`                        | 75th percentile of earnings
|`college_jobs`                 | Number with job requiring a college degree
|`non_college_jobs`             | Number with job not requiring a college degree
|`low_wage_jobs`                | Number in low-wage service jobs

We can see that this data frame has a lot of useful information.
Some questions we may want to answer include:

- Which major has the lowest unemployment rate?
- Which major has the highest percentage of women?
- How do the distributions of median income compare across major categories?
- Do women tend to choose majors with lower or higher earnings?

Please note that the ACS only asks [one question](https://www.census.gov/acs/www/about/why-we-ask-each-question/sex/) about a person's sexual identity.

## Exploratory data analysis

For each exercise and on your own question you answer include any relevant output (tables, summary statistics, plots) in your answer.
To do this, remember that you can place any relevant R code in a code chunk, and hit Knit HTML.

### Which major has the lowest unemployment rate?

**Though Question 4**:
What information (variables) do we need to answer this question?
Describe the process you believe that your Team should do in order to answer this question.
You can describe this using a different software (e.g., Excel, SAS, Python) or just your general process.

***
**Stop Point**

***

This last *TQ* would be a great habit to get into when researching questions.
Once you know what information you need, think of how you currently know how to do it.


In dplyr, we use the `arrange` function to sort the data.
So we will sort `college_recent_grads` by the `unemployment_rate` variable.
By default `arrange` sorts in ascending order, which is what we want here - we are interested in the major with the *lowest* unemployment rate.

```
college_recent_grads %>%
  arrange(unemployment_rate)
```

We get the information that we want, but it is not in an effective format.
The names of the majors barely fits on the page, some of the variables are not that useful (e.g. `major_code`, `major_category`), and some variables that we might want front and center are not easily viewed (e.g. `unemployment_rate`).

The `select` function will let us choose which variables to display, and in which order:

```
college_recent_grads %>%
  arrange(unemployment_rate) %>%
  select(rank, major, unemployment_rate)
```

First, notice how easily we can expand our code with adding another step to our pipeline with the pipe operator: `%>%`.
Second, this output is starting to look better, but there are a lot of decimal places in the unemployment variable.
There are a couple of ways that we can clean this up.

One way is to round the `unemployment_rate` variable in the dataset.
The other way is to change the number of digits displayed without touching the input data.

I will provide you with instructions for how you would do both of these below, but you do not need to do both of these.
That would be redundant.
In your first exercise, you and your Team Members are asked to choose one and explain your choice.

- *Round `unemployment_rate`*: We create a new variable with the `mutate` function.
  In this case, we're overwriting the existing `unemployment_rate` variable, by rounding (`round`) it to four (`4`) decimal places.

```
college_recent_grads %>%
  arrange(unemployment_rate) %>%
  select(rank, major, unemployment_rate) %>%
  mutate(unemployment_rate = round(unemployment_rate, digits = 4))
```

- *Change displayed number of digits without touching data*: We can add an option to our R Markdown document to change the displayed number of digits in the output. 
  To do so, add a new chunk, and set:

```
options(digits = 2)
```

Note that the `digits` in `options` is scientific digits, and in `round` they are decimal places.
If you are thinking, "Wouldn't it be nice if they were consistent?", yes, but...

***
**Exercise 1**:
Which of these options, changing the input data or altering the number of digits displayed without touching the input data, is the better option?
Explain your reasoning, then implement the option you chose.

***

### Which major has the highest proportion of women?

To answer this question, we need to arrange the data in descending order.
For example, if earlier we were instead interested in the major with the highest unemployment rate, we would use the following code:

```
college_recent_grads %>%
  arrange(desc(unemployment_rate)) %>%
  select(rank, major, unemployment_rate)
```

The `desc` function specifies that we want `unemployment_rate` in descending order.

***
**Exercise 2**:
Using what you've learned so far, arrange the data in descending order with respect to proportion of women in a major.
Display only the major, the total number of people with major, and proportion of women.
Show only the top 3 majors by adding `head(3)` at the end of the pipeline.

***

### How do the distributions of median income compare across major categories?

There are three types of incomes reported in this data frame: `p25th`, `median`, and `p75th`.
These correspond to the 25th, 50th, and 75th percentiles of the income distribution of sampled individuals for a given major.
Remember that a percentile is a measure used to indicate the value below which a given percentage of observations in a group of observations fall.
For example, the 60th percentile is the value below which 60% of the observations may be found.

***
**Exercise 3**:
Why do we often choose the median, rather than the mean, to describe the typical income of a group of people?

***

To answer “How do the distributions of median income compare across major categories?” we need to do a few things.
First, we need to group the data by `major_category`.
Then, we need a way to summarize the distributions of median income within these groups.
This decision will depend on the shapes of these distributions.
So first, we need to visualize the data.

So far we have only used the `ggplot` function to plot scatterplots.
However, we can use this function to produce different plots.
The first argument of `ggplot` is the data frame and the next argument gives the mapping of the variables of the data to the aesthetic (`aes`) elements of the plot.

Here is how we can look at the distribution of all `median` incomes, without considering `major_category`.

```
ggplot(data = college_recent_grads, mapping = aes(x = median)) +
  geom_histogram()
```

Notice that we only have `x`, instead of both `x` and `y`, since histograms are used for uni-variate distributions.

When you run the code for this plot, we get a message

```
`stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

This informs us that we may wish to reconsider the binwidth we chose (or didn't specify) for our histogram.
It is good practice to think in the context of the data and try out a few binwidths before settling on one.
You might ask yourself, "what would be a meaningful difference in median incomes?"
&dollar;1 is obviously too little, but &dollar;10,000 might be too high.

***
**Exercise 4**:
Try binwidths of &dollar;1,000 and &dollar;5,000 and choose one.
Explain your reasoning for your choice.
Note that the binwidth is an argument for the `geom_histogram` function.
So to specify a binwidth of &dollar;1,000, you would use `geom_histogram(binwidth = 1000)`.

***

We can also calculate summary statistics for this distribution using the `summarise` function:

```
college_recent_grads %>%
  summarise(min = min(median), 
            max = max(median),
            mean = mean(median),
            med = median(median),
            sd = sd(median), 
            q1 = quantile(median, probs = 0.25),
            q3 = quantile(median, probs = 0.75))
```

***
**Exercise 5**:
Based on the shape of the histogram you created in the previous exercise, determine which of these summary statistics is useful for describing the distribution.
Write up your description (remember shape, center, spread, any unusual observations) and include the summary statistic output as well.

***

Next, we facet the plot by major category.

```
ggplot(data = college_recent_grads, mapping = aes(x = median)) +
  geom_histogram() +
  facet_wrap( ~ major_category, ncol = 4)
```


***
**Exercise 6**:
Plot the distribution of `median` income using a histogram, faceted by `major_category`.
Use the `binwidth` you chose in the earlier exercise.

***

Now that we've seen the shapes of the distributions of median incomes for each major category, we should have a better idea for which summary statistic to use to quantify the typical median income.


***
**Exercise 7**:
Which major category has the highest typical (you'll need to decide what this means) median income? Use the partial code below, filling it in with the appropriate statistic and function.
Also note that we are looking for the highest statistic, so make sure to arrange in the correct direction. 

***

```
college_recent_grads %>%
  group_by(major_category) %>%
  summarise(___ = ___(median)) %>%
  arrange(___)
```

***
**Exercise 8**:
Which major category is the least popular in this sample?
To answer this question we use a new function called `count`, which first groups the data and then counts the number of observations in each category (see below).
Add to the pipeline appropriately to arrange the results so that the major with the lowest observations is on top.

***

```
college_recent_grads %>%
  count(major_category)
```

## All STEM fields aren't the same

One of the sections of the [FiveThirtyEight story](https://fivethirtyeight.com/features/the-economic-guide-to-picking-a-college-major/) is "All STEM fields aren't the same".
We will see if this is true.

First, we will create a new vector called `stem_categories` that lists the major categories that are considered STEM fields.

```
stem_categories <- c("Biology & Life Science",
                     "Computers & Mathematics",
                     "Engineering",
                     "Physical Sciences")
```

Then, we can use this to create a new variable in our data frame indicating whether a major is STEM or not.

```
college_recent_grads <- college_recent_grads %>%
  mutate(major_type = ifelse(major_category %in% stem_categories, "stem", "not stem"))
```

Let's unpack this.
With `mutate` we create a new variable called `major_type`, which is defined as `"stem"` if the `major_category` is in the vector called `stem_categories` we created earlier, and as `"not stem"` otherwise.

`%in%` is a **logical operator**.
Other logical operators that are commonly used are

| Operator                   | Operation
|:----------------|:--------------
|`x < y`                     | less than
| `x > y`                    | greater than
| `x <= y`                   | less than or equal to
| `x >= y`                   | greater than or equal to
| `x != y`                   | not equal to
| `x == y`                   | equal to
| `x %in% y`                 | contains
| <code>x &#124; y</code>    | or
| `x & y`                    | and
| `!x`                       | not

We can use the logical operators to also `filter` our data for STEM majors whose median earnings is less than median for all majors' median earnings, which we found to be &dollar;36,000 earlier.

```
college_recent_grads %>%
  filter(
    major_type == "stem",
    median < 36000
  )
```


***
**Exercise 9**:
Which STEM majors have median salaries equal to or less than the median for all majors' median earnings?
Your output should only show the major name and median, 25th percentile, and 75th percentile earning for that major as and should be sorted such that the major with the highest median earning is on top.

***

## What types of majors do women tend to major in?

***
**Exercise 10**:
Create a scatterplot of median income vs. proportion of women in that major, colored by whether the major is in a STEM field or not.
Describe the association between these three variables.
