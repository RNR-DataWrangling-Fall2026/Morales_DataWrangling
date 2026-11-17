# Week 12 Assignment


# Assignment

### Purpose

The goal of this assignment is to practice writing and using conditional
statements, `if_else` and `case_when`, and `if`-`else` statements, and
to combine them with skills from earlier in the semester (joins,
strings, and plotting).

### Task

Write R code to successfully answer each question below.

### Criteria for Success

- Code is within the provided code chunks or new code chunks are created
  where necessary
- Code chunks run without errors
- Code chunks have brief comments indicating which code is answering
  which part of the question
- Code will be assessed as follows:
  - Produces the correct answer using the requested approach: 100%
  - Generally uses the right approach, but a minor mistake results in an
    incorrect answer: 90%
  - Attempts to solve the problem and makes some progress using the core
    concept, but returns the wrong answer and does not demonstrate
    comfort with the core concept: 50%
  - Answer demonstrates a lack of understanding of the core concept: 0%
- Any questions requiring written answers are answered with sufficient
  detail

### Due Date

November 17 before class

# Assignment Exercises

### 1. Choice Operators (10 pts)

Create the following variables by running the code chunk below.

``` r
w <- 10.2
x <- 1.3
y <- 2.8
z <- 17.5
colors <- c("red", "blue", "green")
masses <- c(45.2, 36.1, 27.8, 81.6, 42.4)

# 1a. Is green in colors?
"green" %in% colors
```

    [1] TRUE

``` r
# 1b. Is purple not in colors?
!("purple" %in% colors)
```

    [1] TRUE

``` r
# 1c. Is each mass greater than 40?
masses > 40
```

    [1]  TRUE FALSE FALSE  TRUE  TRUE

``` r
# 1d. Is w greater than x OR y greater than z?
w > x | y > z
```

    [1] TRUE

``` r
# 1e. Is x times w between 13.2 and 13.5?
x * w > 13.2 & x * w < 13.5
```

    [1] TRUE

Using the variables above, write code that determines whether the
following statements are `TRUE` or `FALSE`.

1.  `"green"` is in `colors`
2.  `"purple"` is not in `colors`
3.  Each value in `masses` is greater than 40.
4.  `w` is greater than `x`, or `y` is greater than `z`
5.  `x` times `w` is between 13.2 and 13.5

### 2. Using `dplyr` Choice Functions (20 points)

For this question, we will be using functions from `dplyr` (part of the
`tidyverse`) and data from the `lterdatasampler` package, so make sure
you load both of those packages with the `library()` function.

First, create an object called `crab_size` and assign the value 17 to
it.

1.  Use the `if_else` function from `dplyr` to say that a crab that is
    larger than or equal to 20 is “large” and a crab that is smaller
    than 20 is “small.”

2.  Use the `case_when` function to say that if a crab is greater than
    or equal to 20, it is “large;” if greater than or equal to 10 but
    less than 20, it is “medium;” and if it is smaller than 10, it is
    “small.” Make sure that your `crab_size` object is still set to 17.

3.  Take a look at the `pie_crab` dataset from the `lterdatasampler`
    package by running `head(pie_crab)`. We want to create a new column
    based on the `size` column. Using the `if_else` function inside of a
    `mutate` function, create a new column called `size_category` based
    on the same conditions as (a).

    I’ve placed my new column next to the size column for the sake of
    the answer key; you don’t need to do this.

4.  Now use the `case_when` function inside a `mutate` function to
    create a new column called `size_category3` in the `pie_crab` data
    frame that meets the same conditions as (b).

    I’ve placed my new column next to the size column for the sake of
    the answer key; you don’t need to do this.

``` r
# Load packages
library(tidyverse)
```

    ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ✔ dplyr     1.2.1     ✔ readr     2.2.0
    ✔ forcats   1.0.1     ✔ stringr   1.6.0
    ✔ ggplot2   4.0.3     ✔ tibble    3.3.1
    ✔ lubridate 1.9.5     ✔ tidyr     1.3.2
    ✔ purrr     1.2.2     
    ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ✖ dplyr::filter() masks stats::filter()
    ✖ dplyr::lag()    masks stats::lag()
    ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(lterdatasampler)
```

    Warning: package 'lterdatasampler' was built under R version 4.6.2

``` r
# Create crab size
crab_size <- 17

# 2a. Large or small
if_else(crab_size >= 20, "large", "small")
```

    [1] "small"

``` r
# 2b. Large, medium, or small
case_when(
  crab_size >= 20 ~ "large",
  crab_size >= 10 & crab_size < 20 ~ "medium",
  crab_size < 10 ~ "small"
)
```

    [1] "medium"

``` r
# 2c. Create size_category
head(pie_crab)
```

    # A tibble: 6 × 9
      date       latitude site   size air_temp air_temp_sd water_temp water_temp_sd
      <date>        <dbl> <chr> <dbl>    <dbl>       <dbl>      <dbl>         <dbl>
    1 2016-07-24       30 GTM    12.4     21.8        6.39       24.5          6.12
    2 2016-07-24       30 GTM    14.2     21.8        6.39       24.5          6.12
    3 2016-07-24       30 GTM    14.5     21.8        6.39       24.5          6.12
    4 2016-07-24       30 GTM    12.9     21.8        6.39       24.5          6.12
    5 2016-07-24       30 GTM    12.4     21.8        6.39       24.5          6.12
    6 2016-07-24       30 GTM    13.0     21.8        6.39       24.5          6.12
    # ℹ 1 more variable: name <chr>

``` r
pie_crab <- pie_crab |>
  mutate(size_category = if_else(size >= 20, "large", "small"))

head(pie_crab)
```

    # A tibble: 6 × 10
      date       latitude site   size air_temp air_temp_sd water_temp water_temp_sd
      <date>        <dbl> <chr> <dbl>    <dbl>       <dbl>      <dbl>         <dbl>
    1 2016-07-24       30 GTM    12.4     21.8        6.39       24.5          6.12
    2 2016-07-24       30 GTM    14.2     21.8        6.39       24.5          6.12
    3 2016-07-24       30 GTM    14.5     21.8        6.39       24.5          6.12
    4 2016-07-24       30 GTM    12.9     21.8        6.39       24.5          6.12
    5 2016-07-24       30 GTM    12.4     21.8        6.39       24.5          6.12
    6 2016-07-24       30 GTM    13.0     21.8        6.39       24.5          6.12
    # ℹ 2 more variables: name <chr>, size_category <chr>

``` r
# 2d. Create size_category3
pie_crab <- pie_crab |>
  mutate(size_category3 = case_when(
    size >= 20 ~ "large",
    size >= 10 & size < 20 ~ "medium",
    size < 10 ~ "small"
  ))

head(pie_crab)
```

    # A tibble: 6 × 11
      date       latitude site   size air_temp air_temp_sd water_temp water_temp_sd
      <date>        <dbl> <chr> <dbl>    <dbl>       <dbl>      <dbl>         <dbl>
    1 2016-07-24       30 GTM    12.4     21.8        6.39       24.5          6.12
    2 2016-07-24       30 GTM    14.2     21.8        6.39       24.5          6.12
    3 2016-07-24       30 GTM    14.5     21.8        6.39       24.5          6.12
    4 2016-07-24       30 GTM    12.9     21.8        6.39       24.5          6.12
    5 2016-07-24       30 GTM    12.4     21.8        6.39       24.5          6.12
    6 2016-07-24       30 GTM    13.0     21.8        6.39       24.5          6.12
    # ℹ 3 more variables: name <chr>, size_category <chr>, size_category3 <chr>

### 3. If/Else Statements (20 points)

1.  Complete the following `if` statement so that if `age_class` is
    equal to “sapling” it sets `y` to 10, if `age_class` is equal to
    “seedling” it sets `y` to 5, and if `age_class` is something else it
    sets `y` to 0.

``` r
age_class <- "adult"

# 3a. Assign y based on age class
age_class <- "adult"

if (age_class == "sapling") {
  y <- 10
} else if (age_class == "seedling") {
  y <- 5
} else {
  y <- 0
}

y
```

    [1] 0

``` r
# 3b. Function for age class
get_age_value <- function(age_class) {
  if (age_class == "sapling") {
    y <- 10
  } else if (age_class == "seedling") {
    y <- 5
  } else {
    y <- 0
  }
  
  return(y)
}

get_age_value("sapling")
```

    [1] 10

``` r
get_age_value("seedling")
```

    [1] 5

``` r
get_age_value("adult")
```

    [1] 0

``` r
get_age_value("mature")
```

    [1] 0

``` r
get_age_value("established")
```

    [1] 0

``` r
# 3c. Predict value based on x
predict_value <- function(x) {
  if (x > 0 & x < 15) {
    y <- 6 + 0.8 * x
  } else if (x >= 15 & x < 30) {
    y <- 5 + 0.75 * x
  } else {
    y <- NA
  }
  
  return(y)
}

predict_value(5)
```

    [1] 10

``` r
predict_value(26)
```

    [1] 24.5

``` r
predict_value(-2)
```

    [1] NA

2.  Convert your conditional statement from (a) into a function that
    takes `age_class` as an argument and returns `y`. Call this function
    5 times, once with each of the following values for `age_class`:
    “sapling”, “seedling”, “adult”, “mature”, “established”.

3.  Write a function called `predict_value` that takes a single argument
    `x`. If `x` is greater than 0 and less than 15, return
    `y = 6 + 0.8 * x`. If `x` is greater than or equal to 15 and less
    than 30, return `y = 5 + 0.75 * x`. In all other cases, return
    `y = NA`. Call the function three times, with `5`, `26`, and `-2` as
    the input.

### 4. Size Estimates by Name (20 points)

This is a follow up to “Use and Modify” from Assignment 11.

To make it even easier to work with your dinosaur size estimation
functions you decide to create a function that lets you specify which
dinosaur group you need to estimate the size of by name and then have
the function automatically choose the right parameters.

Remember the general form of the equation is:

mass \<- a \* length ^ b

Create a new function `get_mass_from_length_by_name()` that takes two
arguments: the `length` and the name of the dinosaur group.

Inside this function use `if`/`else if`/`else` statements to check to
see if the name is one of the following values and if so use the
associated `a` and `b` values to estimate the species mass using these
equations:

- *Stegosauria*: `mass = 10.95 * length ^ 2.64`
- *Theropoda*: `mass = 0.73 * length ^ 3.63`
- *Sauropoda*: `mass = 214.44 * length ^ 1.46`

If the name is not any of these values the function should return `NA`.

Run the function for the following:

1.  A *Stegosauria* that is 10 meters long.
2.  A *Theropoda* that is 8 meters long.
3.  A *Sauropoda* that is 12 meters long.
4.  An *Ankylosauria* that is 13 meters long.

*Challenge 1 (optional)*: If the name is not one of values that have a
and b values print warning that it doesn’t know how to convert that
group that includes that groups name in a message like “No known
estimation for Ankylosauria.” You can use the function
`warning("your warning text")` to print a warning and the function
`paste()` to combine text with a value from a variable such as
`paste("My name is", name)`. Doing this successfully will modify your
answer to (d), which is fine.

*Challenge 2 (optional)*: Change your function so that it uses two
different values of `a` and `b` for *Stegosauria*. When *Stegosauria* is
greater than 8 meters long use the equation above. When it is 8 meters
long or less, use `a = 8.5` and `b = 2.8`. Run the function for a
*Stegosauria* that is 6 meters long.

Hint: you can put an `if`-`else` statement inside another `if`
statement, like this:

``` r
# 4. Estimate dinosaur mass based on group
get_mass_from_length_by_name <- function(length, name) {
  if (name == "Stegosauria") {
    mass <- 10.95 * length^2.64
  } else if (name == "Theropoda") {
    mass <- 0.73 * length^3.63
  } else if (name == "Sauropoda") {
    mass <- 214.44 * length^1.46
  } else {
    mass <- NA
  }
  
  return(mass)
}

# 4a. Stegosauria, 10 meters
get_mass_from_length_by_name(10, "Stegosauria")

# 4b. Theropoda, 8 meters
get_mass_from_length_by_name(8, "Theropoda")

# 4c. Sauropoda, 12 meters
get_mass_from_length_by_name(12, "Sauropoda")

# 4d. Ankylosauria, 13 meters
get_mass_from_length_by_name(13, "Ankylosauria")
```

### 5. Putting It All Together: Portal Rodents (30 points)

In this question, you will combine choice functions with joins, strings,
and plotting. Load the `tidyverse` if you haven’t already.

Download the following Portal data tables using code below (modify the
`destfile` arguments to point to the correct sub-directory) to get
started.

``` r
# download.file(url = "https://ndownloader.figshare.com/files/2292172",
#   destfile = "surveys.csv")
# download.file(url = "https://ndownloader.figshare.com/files/3299483",
#   destfile = "species.csv")
```

1.  Join `surveys` and `species` together so that each survey record has
    the genus, species, and taxa information. Keep only rodents (`taxa`
    is “Rodent”). Then, use a `stringr` function to add a column called
    `scientific_name` that combines `genus` and `species` with a space
    between them (e.g., “Dipodomys merriami”). Save the result as an
    object called `rodents`.

2.  Some individuals could only be identified to genus, so their
    `species` is “sp.” (e.g., “Dipodomys sp.”). Use `if_else` and
    `str_detect` inside a `mutate` to add a column called `id_level`
    that is “genus only” if `scientific_name` contains “sp.” and
    “species” otherwise. Then use `count()` to show how many records
    fall into each `id_level`.

    Hint: Remember that `.` is a special character in regular
    expressions! If you don’t account for this, some species names (like
    *Dipodomys spectabilis*) will be counted incorrectly.

3.  Use `if_else` and the `%in%` operator inside a `mutate` to add a
    column called `season` that is “warm” if the `month` is April
    through September (months 4-9) and “cool” otherwise.

4.  Use `case_when` inside a `mutate` to add a column called
    `weight_class` with the following categories:

    - “unknown” if `weight` is `NA`
    - “small” if `weight` is less than 20
    - “medium” if `weight` is greater than or equal to 20 and less than
      50
    - “large” for everything else (use the `.default` argument)

    Save the results of (b), (c), and (d) back into your `rodents`
    object.

    In a sentence or two, answer the following: what would happen to
    individuals with missing weights if you left out the “unknown” line?
    Why?

5.  Using `rodents`, remove the individuals with an “unknown” weight
    class and count the number of individuals in each `year`, `season`,
    and `weight_class`. Then, make a line plot with `year` on the
    x-axis, the count on the y-axis, lines colored by `weight_class`,
    and a separate panel for each `season`. Give your plot informative
    axis labels and use a theme of your choice.

    In a sentence or two, describe one pattern you see in the plot.

``` r
surveys <- read_csv("data_raw/surveys.csv")
```

    Rows: 35549 Columns: 9
    ── Column specification ────────────────────────────────────────────────────────
    Delimiter: ","
    chr (2): species_id, sex
    dbl (7): record_id, month, day, year, plot_id, hindfoot_length, weight

    ℹ Use `spec()` to retrieve the full column specification for this data.
    ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
species <- read_csv("data_raw/species.csv")
```

    Rows: 54 Columns: 4
    ── Column specification ────────────────────────────────────────────────────────
    Delimiter: ","
    chr (4): species_id, genus, species, taxa

    ℹ Use `spec()` to retrieve the full column specification for this data.
    ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
# 5a. Load the Portal datasets
surveys <- read_csv("data_raw/surveys.csv")
```

    Rows: 35549 Columns: 9
    ── Column specification ────────────────────────────────────────────────────────
    Delimiter: ","
    chr (2): species_id, sex
    dbl (7): record_id, month, day, year, plot_id, hindfoot_length, weight

    ℹ Use `spec()` to retrieve the full column specification for this data.
    ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
species <- read_csv("data_raw/species.csv")
```

    Rows: 54 Columns: 4
    ── Column specification ────────────────────────────────────────────────────────
    Delimiter: ","
    chr (4): species_id, genus, species, taxa

    ℹ Use `spec()` to retrieve the full column specification for this data.
    ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
# Join datasets and keep rodents
rodents <- surveys |>
  inner_join(species, by = "species_id") |>
  filter(taxa == "Rodent") |>
  mutate(scientific_name = str_c(genus, species, sep = " "))

head(rodents)
```

    # A tibble: 6 × 13
      record_id month   day  year plot_id species_id sex   hindfoot_length weight
          <dbl> <dbl> <dbl> <dbl>   <dbl> <chr>      <chr>           <dbl>  <dbl>
    1         1     7    16  1977       2 NL         M                  32     NA
    2         2     7    16  1977       3 NL         M                  33     NA
    3         3     7    16  1977       2 DM         F                  37     NA
    4         4     7    16  1977       7 DM         M                  36     NA
    5         5     7    16  1977       3 DM         M                  35     NA
    6         6     7    16  1977       1 PF         M                  14     NA
    # ℹ 4 more variables: genus <chr>, species <chr>, taxa <chr>,
    #   scientific_name <chr>

``` r
# 5b. Classify identification level
rodents <- rodents |>
  mutate(id_level = if_else(
    str_detect(scientific_name, "sp\\."),
    "genus only",
    "species"
  ))

# Count records by identification level
rodents |>
  count(id_level)
```

    # A tibble: 2 × 2
      id_level       n
      <chr>      <int>
    1 genus only    70
    2 species    34177

``` r
# 5c. Classify warm and cool seasons
rodents <- rodents |>
  mutate(season = if_else(
    month %in% 4:9,
    "warm",
    "cool"
  ))

rodents |>
  count(season)
```

    # A tibble: 2 × 2
      season     n
      <chr>  <int>
    1 cool   16913
    2 warm   17334

``` r
# 5d. Create weight categories
rodents <- rodents |>
  mutate(weight_class = case_when(
    is.na(weight) ~ "unknown",
    weight < 20 ~ "small",
    weight >= 20 & weight < 50 ~ "medium",
    .default = "large"
  ))

rodents |>
  count(weight_class)
```

    # A tibble: 4 × 2
      weight_class     n
      <chr>        <int>
    1 large         6721
    2 medium       17958
    3 small         7604
    4 unknown       1964

``` r
#If I left out the "unknown" condition, individuals with missing weights would be classified as "large" because of the default argument. This would make the results inaccurate because their weights were not recorded.

# 5e. Remove unknown weights and count individuals
rodent_counts <- rodents |>
  filter(weight_class != "unknown") |>
  count(year, season, weight_class)

# Make line plot
rodent_plot <- ggplot(
  rodent_counts,
  aes(x = year, y = n, color = weight_class)
) +
  geom_line() +
  facet_wrap(~ season) +
  labs(
    x = "Year",
    y = "Number of Individuals",
    color = "Weight Class"
  ) +
  theme_bw()

rodent_plot
```

![](Week12_Assignment_files/figure-commonmark/unnamed-chunk-6-1.png)

``` r
#Medium-sized rodents generally had the highest number of observations in both seasons. Their numbers changed from year to year, with some noticeable increases during the late 1990s and early 2000s.
```

### 6. Challenge: A “Safe” Tidyverse Function (OPTIONAL)

In the lesson, we talked about how `if` statements can control your
workflow, such as stopping your code with a helpful error message when
something is wrong. Let’s try it!

Write a function called `categorize_by_threshold()` that takes three
arguments: (1) a data frame, (2) a column in that data frame, and (3) a
`threshold` value. (Remember `{ }` from Week 11!)

The function should:

- Use an `if` statement to check whether the column is numeric. If it is
  not, use `stop()` to end the function with the error message “Column
  must be numeric.”
- Use an `else if` statement to check whether `threshold` is outside the
  range of values in the column (ignoring `NA`s). If it is, use `stop()`
  and `paste()` to end the function with an error message that includes
  the minimum and maximum values of the column, like “Threshold must be
  between 4 and 280.”
- Otherwise, use `mutate()` and `if_else()` to add a new column called
  `category` that is “above” when the column value is greater than or
  equal to `threshold` and “below” when it is less than `threshold`.

Hint: `pull(df, {{ col }})` will pull out a column as a vector, which
you can then use with functions like `is.numeric()` and `range()`.

Test your function on the `rodents` data frame from Question 5 four
times:

1.  with the `weight` column and a threshold of 50
2.  with the `hindfoot_length` column and a threshold of 30
3.  with the `genus` column and a threshold of 50 (this should give an
    error)
4.  with the `weight` column and a threshold of 500 (this should give an
    error)

Note: code chunks that produce an error will stop your document from
rendering. Add `#| error: true` as the first line of the code chunks for
(c) and (d) so the document will render and show the error messages.

## Turning in Your Assignment

As with the last few weeks, you will be submitting your assignment by
submitting the link to your GitHub repository.

**NOTE**: While I won’t take points off for not doing this, it is very
helpful for grading if you can “Render” your assignments to markdown
(.md) files and push the .md files to GitHub.

That way, I (a) know that your code runs successfully and (b) can go to
your .md file on GitHub and easily see everything in your assignment,
including your outputs, much like in the PDFs you submitted earlier in
the semester.
