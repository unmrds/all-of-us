# Using Python in Jupyter

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
ugss.describe()
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
help(ugss.describe)  # Help information about the describe() function. Note: no parentheses
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

The indexing method above returns all rows for a a subset of columns. Often,
we also want to subset by row. In pandas, this is accomplished using row
index positions. Alternatively, we can also use row index labels, though we 
note that in many cases the row labels will be the same as row index positions.

First let's view information about the row index.

```python
ugss.index
```
```
RangeIndex(start=0, stop=804, step=1)
```

The output indicates that the row index starts with 0 and goes up to 804, by
increments of 1. This means that there are 805 rows in our data. The first 
row has an index position of 0, the second has an index position of 1, and 
so on all the way up to 804.

We can select a subset of rows using the index positions of the starting row
and the ending row separated by a colon. Note that pandas will select all rows
from the starting position **up to but not including** the ending position. Keeping 
in mind that the first row  has an index position of 0, we can view the 
first five  rows with the following:

```python
ugss[0:5] # Output rows with index positions 0, 1, 2, 3, 4 BUT NOT 5.
```
```
      sex  age   eyes  piercings pierced  tattoos tattooed glasses  sleep  \
0    male   22  brown          0      No        0       No     Yes      7   
1  female   21  brown          2     Yes        0       No     Yes      8   
2    male   21  brown          0      No        0       No      No      7   
3    male   22  brown          0      No        0       No      No      7   
4  female   20  brown          4     Yes        0       No     Yes      7   

   study  ...  hair  tobacco smokes alcohol buy.alcohol sendtxt  receivetxt  \
0     40  ...    15        0     No       0          No      10          10   
1     12  ...    50        0     No      10         Yes      10          10   
2      2  ...    15        0     No       0          No      25          25   
3      2  ...    15        0     No       0          No      20          20   
4      3  ...    20        0     No      10         Yes       5           5   

   txts  country       status  
0   Yes    China   NZ.Citizen  
1   Yes       NZ   NZ.Citizen  
2   Yes       HK   NZ.Citizen  
3   Yes       NZ  NZ.Resident  
4   Yes       NZ   NZ.Citizen  

[5 rows x 29 columns]
```

When a subset begins with the first row of data, or ends with the last row, we
can exclude those index positions.


```python
ugss[:5] # Same result as running the ugss.head() function.
```

```python
ugss[799:804] # Same result as running the ugss.tail() function.
```

We can also use negative indexing. The below will also output
the last five rows of data, and is useful in cases where we may not know how
many rows of data we have.

```python
ugss[-5:] # Also the same result as running the ugss.tail() function.
```

If we want to select a single row based on its row index position, we need to
explicitly specify the index position label using ```iloc```:


```python
ugss.iloc[0]
```
```
sex                        male
age                          22
eyes                      brown
piercings                     0
pierced                      No
tattoos                       0
tattooed                     No
glasses                     Yes
sleep                         7
study                        40
tv                            0
movies                        0
movies3m                     No
sport                basketball
entertainment    comp.vid.games
fruit                     melon
income                      198
rent                        120
clothes                      20
hair                         15
tobacco                       0
smokes                       No
alcohol                       0
buy.alcohol                  No
sendtxt                      10
receivetxt                   10
txts                        Yes
country                   China
status               NZ.Citizen
Name: 0, dtype: object
```

Another way to select the first five rows of data:

```python
ugss.iloc[0:5]
```

### Subsetting by row and column

We can combine the indexing methods above to select by both row and column.
Let's say we interested in the values of the "sex" and "age" columns, for the
first five observations.

```python
ugss[:5][["sex", "age"]]
```
```
      sex  age
0    male   22
1  female   21
2    male   21
3    male   22
4  female   20
```

### Conditional subsetting

Often, we are most interested in subsetting data based on conditions. That is,
we are interested in the set of observations for which the values of certain
variables fall within specified parameters.

For example, perhaps we want to limit our analysis to respondents under the
age of 25:

```python
ugss["age"] > 25
```
```
0      True
1      True
2      True
3      True
4      True
       ... 
799    True
800    True
801    True
802    True
803    True
Name: age, Length: 804, dtype: bool
```

Note that the output of the above is not the subset we're interested in!
Instead, the output shows us the result of the evaluation of the condition
against each row of the dataset. 

In order to actually get the subset of rows where the value of the "age"
variable is less than 25, we need to use the condition as the row selector
in place of the slicing syntax demonstrated above.

If we are going to manipulate the subset, it's also good to explicitly
state that we want a copy of the data.

```python
under_25 = ugss[ugss["age"] < 25].copy()
print(under_25)
```
```
        sex  age   eyes  piercings pierced  tattoos tattooed glasses  sleep  \
0      male   22  brown          0      No        0       No     Yes      7   
1    female   21  brown          2     Yes        0       No     Yes      8   
2      male   21  brown          0      No        0       No      No      7   
3      male   22  brown          0      No        0       No      No      7   
4    female   20  brown          4     Yes        0       No     Yes      7   
..      ...  ...    ...        ...     ...      ...      ...     ...    ...   
799  female   21   blue          2     Yes        0       No      No      8   
800    male   19   blue          0      No        0       No      No      7   
801    male   24  brown          0      No        0       No     Yes      9   
802  female   20  brown          2     Yes        0       No      No      5   
803    male   22  brown          0      No        0       No     Yes      7   

     study  ...  hair  tobacco smokes alcohol buy.alcohol sendtxt  receivetxt  \
0       40  ...    15        0     No       0          No      10          10   
1       12  ...    50        0     No      10         Yes      10          10   
2        2  ...    15        0     No       0          No      25          25   
3        2  ...    15        0     No       0          No      20          20   
4        3  ...    20        0     No      10         Yes       5           5   
..     ...  ...   ...      ...    ...     ...         ...     ...         ...   
799      2  ...   230        0     No      50         Yes      30          40   
800      3  ...    15        0     No      30         Yes      20          20   
801     15  ...    30        0     No       0          No      10          10   
802      6  ...    30        0     No       0          No      60          50   
803      8  ...    40       20    Yes      60         Yes      50          30   

     txts  country         status  
0     Yes    China     NZ.Citizen  
1     Yes       NZ     NZ.Citizen  
2     Yes       HK     NZ.Citizen  
3     Yes       NZ    NZ.Resident  
4     Yes       NZ     NZ.Citizen  
..    ...      ...            ...  
799   Yes       NZ     NZ.Citizen  
800   Yes       NZ     NZ.Citizen  
801   Yes   SKorea     NZ.Citizen  
802   Yes    India     NZ.Citizen  
803   Yes    China  International  
```

Though we included every column in our subset above, we can also specify the
columns to include in the subset. If we are interested in analyzing a
(hypothetical!) correlation between eye color and use of eyeglasses among 
non-smokers,  we could exclude any variables that are not of interest.

Note that we are including two conditions below:

```python
under_25_eyes_glasses = ugss[(ugss["age"] < 25) & (ugss["smokes"] == "No")][["sex", "age", "eyes", "glasses"]].copy()
print(under_25_eyes_glasses)
```
```
        sex  age   eyes glasses
0      male   22  brown     Yes
1    female   21  brown     Yes
2      male   21  brown      No
3      male   22  brown      No
4    female   20  brown     Yes
..      ...  ...    ...     ...
797    male   24  brown      No
799  female   21   blue      No
800    male   19   blue      No
801    male   24  brown     Yes
802  female   20  brown      No

[661 rows x 4 columns]
```

The above can be difficult to read! Another, more verbose way to 
arrive at the same result would be:

```python
under_25 = ugss[ugss["age"] < 25].copy()
under_25_ns = under_25[under_25["smokes"] == "No"].copy()
under_25_eyes_glasses = under_25_ns[["sex", "age", "eyes", "glasses"]].copy()
print(under_25_eyes_glasses)
```
```
        sex  age   eyes glasses
0      male   22  brown     Yes
1    female   21  brown     Yes
2      male   21  brown      No
3      male   22  brown      No
4    female   20  brown     Yes
..      ...  ...    ...     ...
797    male   24  brown      No
799  female   21   blue      No
800    male   19   blue      No
801    male   24  brown     Yes
802  female   20  brown      No

[661 rows x 4 columns]
```

This alternative approach requires more lines of code, but may be easier to
understand when you come back to your script later.


### Grouping and summarizing data

The data in the *All of US* public data browser are aggregated at different
levels - sex, age, etc. In order to arrive at similar statistics with the
```ugss``` dataset, we need to group the data using the ```groupby()```
function. Statistics can then be calculated by group.

For example, we may be interested in analyzing study habits by age group. For a
general overview, we can calculate the average hours per week that respondents
spend studying, broken down by age.

As note above, we can accomplish a lot in python with one line of code. From
here on, however, we are going to stick with the verbose approach. Since you
may want to refer to this tutorial later, we want the code to be as clear as
possible!

```python
# subset to roughly college age respondents (18-22)
college_age = ugss[(ugss["age"] >= 18) & (ugss["age"] <= 22)].copy()

# group by age
college_age_groups = college_age.groupby("age")

# for each group, calculate the average time spent studying per week
print(college_age_groups["study"].mean())
```
```
age
18    15.425926
19    12.938547
20    13.481283
21    14.338028
22    15.862500
Name: study, dtype: float64
```

Once we have created our groups, we can calculate statistics for any numeric
column.

```python
# get the averahe number of piercing and tattoos per group
college_age_groups[["piercings", "tattoos"]].mean()
```
```
     piercings   tattoos
age                     
18    0.944444  0.037037
19    1.273743  0.106145
20    1.577540  0.096257
21    1.345070  0.140845
22    1.087500  0.137500
```

We can group by multiple variables. Perhaps we want to break our analysis 
down by both age and sex.

```python
# regroup college_age subset by age and sex
college_age_gender_groups = college_age.groupby(["age", "sex"])

# for each group, calculate the average time spend studying per week
print(college_age_gender_groups["study"].mean())
```
```
age  sex   
18   female    15.761905
     male      15.212121
19   female    14.924731
     male      10.790698
20   female    14.796610
     male      11.231884
21   female    15.123457
     male      13.295082
22   female    17.219512
     male      14.435897
Name: study, dtype: float64
```

Again, we can calculate statistics on multiple columns.

```python
college_age_gender_groups[["piercings", "tattoos", "study"]].mean()
```
```
            piercings   tattoos      study
age sex                                   
18  female   2.047619  0.095238  15.761905
    male     0.242424  0.000000  15.212121
19  female   2.182796  0.129032  14.924731
    male     0.290698  0.081395  10.790698
20  female   2.398305  0.118644  14.796610
    male     0.173913  0.057971  11.231884
21  female   2.160494  0.111111  15.123457
    male     0.262295  0.180328  13.295082
22  female   1.804878  0.121951  17.219512
    male     0.333333  0.153846  14.435897
```


## Visualizing data with plotnine

The final topic of this introduction to using Python in Jupyter is visualizing
data.

```plotnine``` is a python library designed for iterative development of 
publication-ready plots. It is a python port of the popular ```ggplot()```
package in R. For the most part we will develop each plot within a single
code cell. For future reference, the step-by-step process is included in the
copy of this tutorial online [^3].

The overall process for developing plots with ```plotnine``` is

1. Define plot axes and global aesthetics in a plot object.
1. Set layers of plot styles and aesthetics using geometries.
1. Customize labels and themes.

Let's get plotting! First we have to import the ```plotnine```
library.

```python
import plotnine as p9
```

Following the process described above, the first step is to define a plot
object. 

```python
p9.ggplot(data=ugss, mapping = p9.aes(x = "age", y = "study"))
```

When we execute this code cell, the output is an empty plot. The axes are
labeled, but the data haven't actually been plotted. This is because
```plotnine``` needs to know how we intend to represent the data. We use
geometries to do this.

Since we are plotting two continuous variables, a scatter plot may be
informative. 

```python
p9.ggplot(data=ugss, mapping = p9.aes(x = "age", y = "study")) + \
p9.geom_point()
```

The plot gives us a sense of the distribution of time spent studying
across the full dataset. We can make the plot a little more informative by 
setting some of the style arguments in the ```geom_point()``` layer.

```python
p9.ggplot(data=ugss, mapping = p9.aes(x = "age", y = "study")) + \
p9.geom_point(alpha = 0.5, size = 3.0, color = "blue")
```

We can refine the above by adding a layer aesthetic to include information about
whether or not respondents wear glasses.

```python
p9.ggplot(data=ugss, mapping = p9.aes(x = "age", y = "study")) + \
p9.geom_point(alpha = 0.5, size = 3.0, mapping = p9.aes(color = "glasses"))
```

Faceting plots allows us to include even more information. In this case, we
can separate the plots by sex.

```python
p9.ggplot(data=ugss, mapping = p9.aes(x = "age", y = "study")) + \
p9.geom_point(alpha = 0.5, size = 3.0, mapping = p9.aes(color = "glasses"))  + \
p9.facet_wrap("sex")
```

### Customizing plot layout

Once we have arrived at an informative plot, we can change the default layout
and labels.

```python
p9.ggplot(data=ugss, mapping = p9.aes(x = "age", y = "study")) + \
p9.geom_point(alpha = 0.5, size = 3.0, mapping = p9.aes(color = "glasses"))  + \
p9.facet_wrap("sex") + \
p9.labs(title = "Time spent studying by age", \
       subtitle = "Per sex and eyeglass use", \
       x = "Age", \
       y = "Hours spent studying per week")
```

We can also change the default theme.

```python
p9.ggplot(data=ugss, mapping = p9.aes(x = "age", y = "study")) + \
p9.geom_point(alpha = 0.5, size = 3.0, mapping = p9.aes(color = "glasses"))  + \
p9.facet_wrap("sex") + \
p9.labs(title = "Time spent studying by age", \
       subtitle = "Per sex and eyeglass use", \
       x = "Age", \
       y = "Hours spent studying per week") + \
p9.theme_light()
```

#### More about plotnine

For more information, see the ```plotnine``` documentation [^4]. 

## Resources

[^1]: Thomas W. Yee (2015). Vector Generalized Linear and Additive Models: 
With an Implementation in R. New York, USA: Springer.

[^2]: RDocumentation.
*VGAMdata: ugss: Undergraduate Statistics Students Lifestyle Questionnaire*.
Version 1.1-9. Accessed 2024-02-12.

  
[^3]: This tutorial: <https://github.com/unmrds/all-of-us/blob/main/aou_tutorial-python.md>

[^4]: <https://plotnine.readthedocs.io/en/stable/index.html>




