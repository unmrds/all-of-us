# Using R in Jupyter

This document provides an introduction to programming in python within a Jupyter
Notebook environment. It is a demonstration of an environment that is 
similar to the *All of Us* researcher workbench. A key difference is the
use within this tutorial of a dataset that originated within R, and was converted to a CSV
that can be imported into python for practice, *Undergraduate Statistics
Students Lifestyle Questionnaire* [^1]. Access to *All of Us* data is limited
to researchers who have completed the data use and registration agreement 
(DURA) process with *All of Us.*

This tutorial is designed to be accessible to researchers who are in the
process of completing, or who have not yet started, the DURA
process. It should be noted that there will be some differences 
between the tutorial environment and the researcher workbench, in 
terms of packages and features available to users. 

In this workshop, we will:

- Introduce the *All of Us* (AoU) research program and corresponding,
grant-funded opportunities available to UNM researchers.
- Describe the process for completing the DURA in order to gain access
to different tiers of AoU data.
- Provide an overview of the data using the public AoU data dashboard.
- Demonstrate how to execute python code in a Jupyter Notebook environment.

No experience with either Jupyter Notebooks or python is necessary. 

We will be using Google's Colab environment. No software installation or 
setup is needed, but learners will need a Google account.

## Using the  All of Us public data browser

As mentioned above, this introduction to R and Jupyter Notebooks does not
make use of *All of Us* data, for reasons relating to the DURA.

However, as a way of framing our analysis and getting a preview of the kinds
of data in *All of Us*, we will begin with a quick tour of the public
data browser:

[*All of Us* public data browser](https://databrowser.researchallofus.org/)

Note that most indicators are broken down by:

- Age
- Sex assigned at birth

We will reproduce similar, high level aggregations in this tutorial, using the
*Undergraduate Statistics Students Lifestyle Questionnaire* (ugss).

Some documentation for this dataset is provided by
[CRAN VGAMdata Package (PDF documentation pg. 89)](https://cran.r-project.org/web/packages/VGAMdata/VGAMdata.pdf)

>
>This data was collected online and anonymously in 2010. The respondents were students studying an undergraduate statistics course at a New Zealand university. Possibly there are duplicate students (due to failing and re-enrolling). All monies are in NZD. Note the data has had minimal checking. Most numerical variables tend to have measurement error, and all of them happen to be all integer-valued.[^2]
>

**ONE FINAL CAVEAT**

In this workshop, we will be using a publicly available dataset to generate
demographic descriptions of variables at a very high level of granularity. We
note that the AoU research workbench provides access to data at the level of
individual observations. Many analyses at a much more granular level are 
available to researchers using the AoU workbench, using a wide array of modeling
and clinical research methodologies. Nothing in this workshop is
intended to imply that researchers using the AoU workbench will be limited to
only generating descriptive statistics. 

## Creating a Jupyter Notebook in Colab

1. Log into Google Drive.
1. Click on the **+ New** button and select **More -> Google Colaboratory**.
1. Welcome to your Jupyter Notebook! The default name will be something like
*Untitled.ipynb*. You can change this by clicking on the title in the top
left of the window.


New notebooks run Python 3 by default.  


>
> #### Tip: Getting back to your notebook
>
>You may want to return to your notebook after this workshop. If you return
>to *My Drive*, your default space in Google Drive, you should see your notebook
>listed with your other files. If you don't see your notebook in the top level
>of your Drive you can also check the *Colab Notebooks* directory if it exists
>as this is where Colab creates new notebooks by default if you don't create
>them from a specific location in *My Drive*. 
>
>Let's check this now and verify that everyone can find their notebook.
>


## Executing commands in a Jupyter Notebook

Jupyter is an interactive environment. Rather than writing out an entire 
script and running it all at once, we can develop a workflow incrementally
by running commands one at a time.

There are three ways to execute a cell of code in a notebook:

1. Click the arrow shaped "run" button next to the code cell. This will
execute the code and create a new, empty code cell.
1. Press **SHIFT + ENTER** in order to run the code and create a new,
empty code cell.
1. Press **CONTROL + ENTER** to execute the code without creating a new
cell.

Try it! Copy the command below into your notebook and use one of the above
methods to run it. 

```python
print(12 ** 2)
```
```
144
```

A cell can contain multiple lines of code. Note that in the next code cell,
we are using the ```=``` symbol as the assignment operator. This is the
conventional syntax for object and variable assignments in Python.

```python
a = 5
b = 3
print(a ** b)
```
```
125
```

>
> #### Tip: Viewing output
>Using ```print()``` is a good way to make sure that the result of a command
>is displayed in the output. Only the output of the last executed command will
>be displayed in the output of an executed cell (this is different from the 
>behavior of Collab with R notebooks):
>
>```python
>a ** b
>b ** a
>```
>```
>243
>```

## Installing packages

The Python environment in Colab comes with many useful packages already 
installed. However, if we need to install a package that is not already
installed we can use the "pip magic" command ```%pip install <package name>```
to install the needed package. 

We will be using the Python *pandas* package for reading, viewing and interacting with
tabular data in our demonstration. It is already installed in the Colab 
environment, but if we needed to install it we could execute the following
command in a cell in the notebook:

```python
%pip install pandas
```

## Using packages

*Packages* are sets of functions and methods that extend the functionality
of the base set of packages included in Python. Very often, packages are developed
around accomplishing a specific set of tasks.

In general is only necessary to install packages once, after which they
are available to load any time we use the local Python environment. However, in order 
to use packages we need to load them into our current environment.

Now let's load the *pandas* package for use in loading and interacting with
our demonstration dataset. This command demonstrates the base command ```import pandas```
with the addition of the ```as pd``` option to define a short name reference
to the *pandas* package. ```pd``` is a commonly used short reference to the *pandas*
package and you will commonly see it referenced in documentation demonstrating
use of the package. 

```python
import pandas as pd
```

## Reading data

We're almost ready to analyze our sample data, which was selected for its
similarity to some indicators included in the AoU data.

There are different ways to load data in Python, depending on whether the data
are stored in a file, accessible from the web, saved in particular file
formats, etc. We note that loading data in the AoU researcher workbench will
probably require some different commands.

The dataset that we will be working with was originally shared as a dataset
as part of the R ```VGAMdata``` package. For this demonstration it was exported
as a Comma-separated-value (CSV) file and placed in a web-accessible location 
for download and use in Python. 

The *pandas* package can read both local and remote CSV files to create a local
pandas *dataframe* with which we can work. To read the remote file we need to
provide the URL of the remote file to the ```read_csv``` *pandas* function. 

```python
file_url = "https://raw.githubusercontent.com/unmrds/all-of-us/main/data/uggs.csv"
ugss = pd.read_csv(file_url)
```
>
> #### Tip: Checking your environment
>
>While working in Jupyter, we may want to view information about the
>ojects - variables and dataframes - that are active in our current
>environment. We can use the ```dir()``` and ```display()``` functions
>to do this.
>
>```dir() # Lists the objects in our current environment. Note this includes packages.```
>
>```display(ugss) # Prints the current value of an object.```
>
>```display(file_url)```


## Inspecting data

A moment ago we used the ```diplay()``` function to open a tabular representation
of the ```ugss``` data. This provided some information about the structure of
the data.

We can also inspect a dataframe's attributes. The syntax for viewing
attributes is the name of the dataframe, followed by the attribute (with no
parenthesis). The dataframe and and the requested attribute are separated by
a dot.

- ```ugss.shape```: The number of rows and columns.
- ```ugss.columns```: Column names.
- ```ugss.size```: The number of observations.
- ```ugss.dtypes```: Data types for each column.


In addition to attributes, there are several functions we can use to inspect
dataframes. The syntax is similar to the above, with the difference that we
do need to use parenthesis after the name of the function.

- ```ugss.info()```: Information about the structure of the dataframe.
- ```ugss.head()```: Prints the first five rows.
- ```ugss.tail()```: Prints the last five rows.


Another useful function is ```describe()```, which provides a default set
of descriptive statistics about numeric columns in a dataframe.

```python
ugss.desc()
```
```
              age   piercings     tattoos       sleep       study          tv  \
count  804.000000  804.000000  804.000000  804.000000  804.000000  804.000000   
mean    21.383085    1.294776    0.115672    7.565920   14.712687    7.330846   
std      3.896866    1.977186    0.509245    1.178632   12.900647    7.917067   
min     17.000000    0.000000    0.000000    4.000000    0.000000    0.000000   
25%     19.000000    0.000000    0.000000    7.000000    5.000000    2.000000   
50%     20.000000    0.000000    0.000000    8.000000   10.000000    5.000000   
75%     22.000000    2.000000    0.000000    8.000000   20.000000   10.000000   
max     59.000000   14.000000    5.000000   12.000000   80.000000   90.000000   

           movies        income         rent      clothes        hair  \
count  804.000000    804.000000   804.000000   804.000000  804.000000   
mean     3.187811    329.351990    86.093284    95.737562   31.829602   
std      3.167519   1259.158928   110.652182   129.735451   37.229617   
min      0.000000      0.000000     0.000000     0.000000    0.000000   
25%      1.000000    126.000000     0.000000    20.000000   15.000000   
50%      2.000000    200.000000    46.500000    50.000000   25.000000   
75%      4.000000    300.000000   150.000000   100.000000   40.000000   
max     20.000000  25000.000000  1000.000000  1000.000000  350.000000   

          tobacco     alcohol     sendtxt  receivetxt  
count  804.000000  804.000000  804.000000  804.000000  
mean     2.062189   11.832090   28.736318   29.361940  
std      9.641061   21.355333   28.677754   29.118166  
min      0.000000    0.000000    0.000000    0.000000  
25%      0.000000    0.000000   10.000000   10.000000  
50%      0.000000    0.000000   20.000000   20.000000  
75%      0.000000   20.000000   40.000000   40.000000  
max    150.000000  200.000000  127.000000  127.000000  

```

## Getting help

We may not always know enough about a function to use it correctly. 
In these cases a useful tool for learning more about a function 
or an object is ```help()```.

```python
help(ugss)   # Help information about dataframes. 'ugss' is an instance of a dataframe object.
```

```python
help(ugss.describe())  # Help information about the describe() function.
```


## Manipulating data

Pandas is a powerful data manipulation library for python. It is designed to
work efficiently with large datasets.

A full demonstration of pandas is beyond the scope of this tutorial. Here
we will focus on some commonly used functions.

### Subsetting data by column

Dataframes in pandas are indexed for fast retrieval. Indexing is done on rows
and columns. We can view information about the indices using the ```info()```
function or the ```axes``` attribute.

```python
ugss.axes
```
```
[RangeIndex(start=0, stop=804, step=1),
 Index(['sex', 'age', 'eyes', 'piercings', 'pierced', 'tattoos', 'tattooed',
        'glasses', 'sleep', 'study', 'tv', 'movies', 'movies3m', 'sport',
        'entertainment', 'fruit', 'income', 'rent', 'clothes', 'hair',
        'tobacco', 'smokes', 'alcohol', 'buy.alcohol', 'sendtxt', 'receivetxt',
        'txts', 'country', 'status'],
       dtype='object')]
```

To subset data to a single column, use the column name in square brackets after
the name of the dataframe.

```python
ugss["age"]
```
```
0      22
1      21
2      21
3      22
4      20
       ..
799    21
800    19
801    24
802    20
803    22
Name: age, Length: 804, dtype: int64
```

To subset by more than one column, use a list of column names. Note that lists
in python are defined using square brackets, so we need to use a double set
of square brackets when we subset by multiple columns.

```python
ugss[["age", "eyes"]]
```
```
 	age 	eyes
0 	22 	brown
1 	21 	brown
2 	21 	brown
3 	22 	brown
4 	20 	brown
... 	... 	...
799 	21 	blue
800 	19 	blue
801 	24 	brown
802 	20 	brown
803 	22 	brown

804 rows × 2 columns
```

### Subsetting data by row

The indexing method above returns all columns for a a subset of rows. Often,
we also want to subset by row. In pandas, this is accomplished using row
index positions. Alternatively, we can also use row index labels, though we 
note that in many cases the row labels will be the same as row index positions.




### Grouping and summarizing data

The data in the *All of US* public data browser are aggregated at different
levels - sex, age, etc. In order to arrive at similar statistics with the
```ugss``` dataset, we need to group the data using the ```group_by()```
function. Statistics can then be calculated by group.

Let's group our age and hours spent studying subset by age.

```python
ugss %>%
  filter(age >= 18 & age <= 22) %>%
  select(age, study) %>%
  group_by(age)
```

You may notice that the output is no different from before we grouped the data!
Groups exist logically. In order to "see" them, we need to calculate some
statistic based on group membership. We use the ```summarize()``` function to
do this.

```python
ugss %>%
  filter(age >= 18 & age <= 22) %>%
  select(age, study) %>%
  group_by(age) %>%
  summarise(average_time_studying = mean(study))
```

It's worth highlighting that throughout this process of data manipulation we
have not altered the underlying raw data. We want to leave our data intact,
but we may also be interested in saving our aggregations. Once we are happy
with the result, we can do that by assigning the output to a new object.

```python
age_study <- ugss %>%
  filter(age >= 18 & age <= 22) %>%
  select(age, study) %>%
  group_by(age) %>%
  summarise(average_time_studying = mean(study))
```

To see the output, we call the new object

```python
age_study
```

We can quickly inspect the ```age_study``` object with ```var.info()```.

```python
var.info()
```

Data can be grouped according to multiple variables. It may make sense to group
our tattoo subset by sex and age. We will also generate a count statistics
for each group. 

```python
ugss %>%
  select(sex, age, tattoos, tattooed) %>%
  filter(tattooed == "Yes") %>%
  group_by(sex, age) %>%
  summarize(count = n())
```

If this looks good, we will save to a new object.

```python
age_sex_tattoos <- ugss %>%
  select(sex, age, tattoos, tattooed) %>%
  filter(tattooed == "Yes") %>%
  group_by(sex, age) %>%
  summarize(count = n())
```

### More about dplyr

```dpyr()``` includes many other functions and methods for working with data.
Some functions we recommend learning about include ```mutate()```, 
```rename()```, and different kinds of joins.

More information can be found at the ```dplyr``` documentation [^3]. The 
documentation page includes a helpful cheat sheet.

## Visualizing data with ggplot

The final topic of this introduction to using R in Jupyter is visualizing
data.

```ggplot()``` is designed for iterative development of publication-ready 
plots. As such, for the most part we will develop each plot within a single
code cell. For future reference, the step-by-step process is included in the
copy of this tutorial online [^4].

The overall process for developing plots with ```ggplot()``` is

1. Define plot axes and global aesthetics in a plot object.
1. Set layers of plot styles and aesthetics using geometries.
1. Customize labels and themes.

Let's create a plot object.

```python
ggplot(age_study, aes(x = age, y = average_time_studying))
```

When we execute this code cell, the output is an empty plot. The axes are
labeled, but the data haven't actually been plotted. This is because
```ggplot()``` needs to know how we intend to represent the data. We use
geometries to do this.

Let's use a "count" plot.

```python
ggplot(age_study, aes(x = age, y = average_time_studying)) +
  geom_col()
```

The output is a plot of average time spent studying by age, for study
participants between 18-22 years of age. 

By way of demonstration, we can also combine ```dplyr``` and ```ggplot``` 
functions for a bigger picture  view. This time we will include
all of the observations.

```python
ugss %>%
  select(age, study) %>%
  ggplot(aes(x = age, y = study)) +
  geom_point()
```

This gives us a different sense of the distribution across the full dataset.
We can make the plot a little more informative by setting some of the style
arguments in the ```geom_point()``` layer.

```python
ugss %>%
  select(age, study) %>%
  ggplot(aes(x = age, y = study)) +
  geom_point(alpha = 0.5, size = 3.0, color = "blue")
```

We will also visualize our tattoo data. Since we grouped by both age and sex,
it makes sense to add a facet layer to separate the plots by groups.

```python
ggplot(age_sex_tattoos, aes(x = age, y = count))
```

Add a geometry. 

```python
ggplot(age_sex_tattoos, aes(x = age, y = count)) +
  geom_col()
```

Note that the resulting plot does not include information about respondents'
sex, even though that data is included in our subset. One way to represent
those data in the plots is to facet by sex.

```python
ggplot(age_sex_tattoos, aes(x = age, y = count)) +
  geom_col() +
  facet_wrap(~ sex)
```

### Customizing plot layout

Once we have arrived at an informative plot, we can change the default layout
and labels.

```python
ggplot(age_sex_tattoos, aes(x = age, y = count)) +
  geom_col(fill = "blue") +
  facet_wrap(~ sex) +
  labs(title = "Count of respondents with tattoos",
  subtitle = "By sex and age",
  x = "Age",
  y = "Count")
```

We can also change the default theme.

```python
ggplot(age_sex_tattoos, aes(x = age, y = count)) +
  geom_col(fill = "blue") +
  facet_wrap(~ sex) +
  labs(title = "Count of respondents with tattoos",
  subtitle = "By sex and age",
  x = "Age",
  y = "Count") +
  theme_light()
```

#### More about ggplot

For more information, see the ```ggplot()``` documentation [^5]. The 
documentation page likewise includes a link to a PDF cheat sheet.

## Resources

[^1]: Thomas W. Yee (2015). Vector Generalized Linear and Additive Models: 
With an Implementation in R. New York, USA: Springer.

[^2]: RDocumentation.
*VGAMdata: ugss: Undergraduate Statistics Students Lifestyle Questionnaire*.
Version 1.1-9. Accessed 2024-02-12.

[^3]: Wickham H, François R, Henry L, Müller K, Vaughan D (2023). _dplyr: A Grammar of
  Data Manipulation_. R package version 1.1.4,
  <https://CRAN.R-project.org/package=dplyr>.
  
[^4]: This tutorial: <https://github.com/unmrds/all-of-us/blob/main/aou_tutorial.md>

[^5]: <https://ggplot2.tidyverse.org/>




