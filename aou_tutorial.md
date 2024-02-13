# Using R in Jupyter

This document provides an introduction to programming R within a Jupyter
Notebook environment. It is a demonstration of an environment that is 
similar to the *All of Us* researcher workbench. A key difference is the
use within this tutorial of an R dataset, *Undergraduate Statistics
Students Lifestyle Questionnaire* [^1]. Access to *All of Us* data is limited
to researchers who have completed the data use and registration agreement 
(DURA) process with *All of Us.*

This tutorial is designed to be accessible to researchers who are in the
process of completing, or who have not yet completed, the DURA
process. It should be noted that there will be some differences 
between the tutorial environment and the researcher workbench, in 
terms of packages and features available to users. 

In this workshop, we will:

- Introduce the *All of Us* (AoU) research program and corresponding,
grant-funded opportunities available to UNM researchers.
- Describe the process for completing the DURA in order to gain access
to different tiers of AoU data.
- Provide an overview of the data using the public AoU data dashboard.
- Demonstrate how to execute R code in a Jupyter Notebook environment.

No experience with either Jupyter Notebooks or R is necessary. 

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
[RDocumentation](https://www.rdocumentation.org/packages/VGAMdata/versions/1.1-9/topics/ugss)

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
1. New notebooks run Python by default. To change this, select
**Runtime -> Change runtime type**. A window will open with some runtime
options. Under the **Runtime type** menu, select **R**. Keep the default
value for the hardware accelerator. Click **Save** to update.

>
> #### Tip: Getting back to your notebook
>
>You may want to return to your notebook after this workshop. If you return
>to *My Drive*, your default space in Google Drive, you should see your notebook
>listed with your other files. 
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

~~~r
print(12 ** 2)
~~~
~~~
[1] 144
~~~

A cell can contain multiple lines of code. Note that in the next code cell,
we are using the ```<-``` symbol as the assignment operator. This is the
conventional syntax for object and variable assignments in R.

~~~r
a <- 5
b <- 3
print(a ** b)
~~~
~~~
[1] 125
~~~

>
> #### Tip: Viewing output
>Using ```print()``` is a good way to make sure that the result of a command
>is displayed in the output. It is required in some environments, but not in
>Colab:
>
>~~~r
>a ** b
>b ** a
>~~~
>~~~
>125  
>243
>~~~

## Installing packages

The R environment in Colab comes with several useful packages already 
installed. However, we need to install the package that includes the dataset
we will use for our sample analysis.

The package is called "VGAMdata."

~~~r
install.packages("VGAMdata")
~~~

A difference between a Jupyter Notebook and other development environments
is that notebooks don't by default provide any kind of quick-access view
of objects, variables, or datasets currently stored in memory. There may
be other ways to accomplish this, but for this workshop we will install and
use a package called "varhandle."

~~~r
install.packages("varhandle")
~~~

## Using packages

*Packages* are sets of functions and methods that extend the functionality
of the base set of packages included in R. Very often, packages are developed
around accomplishing a specific set of tasks. For example, there is a package
called ```lubridate``` that includes methods for working with dates.

In general is only necessary to install packages once, after which they
are available any time we use R. However, in order to use packages we need to
load them into our current environment.

Let's see which packages are currently loaded in our environment.

~~~r
search()
~~~

Now let's load the packages we just installed so the new functionality will
be available to our current environment. We will also load the ```tidyverse```,
which provides a useful set of tools for data cleaning and analysis.

~~~r
library(VGAMdata)
library(varhandle)
library(tidyverse)
~~~

Re-run the ```search()``` command. Note the difference between the previous
output of this command, which now includes the packages we just loaded.

~~~r
search()
~~~
~~~
'.GlobalEnv''package:VGAMdata''package:VGAM''package:splines''package:stats4'
'package:lubridate''package:forcats''package:stringr''package:dplyr'
'package:purrr''package:readr''package:tidyr''package:tibble''package:ggplot2'
'package:tidyverse''package:varhandle''jupyter:irkernel''package:stats'
'package:graphics''package:grDevices''package:utils''package:datasets'
'package:methods''Autoloads''package:base'
~~~

## Reading data

We're almost ready to analyze our sample data, which was selected for its
similarity to some indicators included in the AoU data.

There are different ways to load data in R, depending on whether the data
are stored in a file, accessible from the web, saved in particular file
formats, etc. We note that loading data in the AoU researcher workbench will
probably require some different commands.

That said, there are many sample datasets available within R, either through
packages like the "VGAMdata" package we just installed or included with the
base R packages. These datasets are great for learning R, or for trying
new things. They can be loaded using the ```data()``` function.

~~~r
data(ugss)
~~~

The result of the above command is a *promise* to load the data. In order to
make it fully accessible to our environment, we need to do something with the
data. In this case, we will open up a spreadsheet like view using the
```View()``` function.

~~~r
View(ugss)  # note that is a capital V
~~~

>
> #### Tip: Checking your environment
>
>We have demonstrated use of the ```search()``` function to check which
>packages have been loaded into our environment.
>
>In addition to packages, we may also want to view information about the
>ojects - variables and dataframes - that are active in our current
>environment. We can use the ```var.info()``` function to do this.
>
>```var.info()```

## Inspecting data

A moment ago we used the ```View()``` function to open a tabular representation
of the ```ugss``` data. This provided some information about the structure of
the data, as did the output of the ```var.info()``` function, above.

Other helpful functions for inspecting dataframes are listed below. 
Note that each of these functions has a required argument, which is the name 
of the dataframe about which we are asking for information. 
(For example ```dim(ugss)```, etc.)

- ```dim()```: The number of rows and columns.
- ```nrow()```:  The number of rows.
- ```ncol()```: The number of columns.
- ```names()```: Column names.
- ```str()```: Structure infoamtion.
- ```head()```: The first six rows.
- ```tail()```: The last six rows.

Another useful function is ```summary()```, which provides a default set
of descriptive statistics about factors and numeric columns in a dataframe.

~~~r
summary(ugss)
~~~
~~~
     sex           age           eyes       piercings      pierced  
 female:438   Min.   :17.00   blue : 98   Min.   : 0.000   No :430  
 male  :366   1st Qu.:19.00   brown:523   1st Qu.: 0.000   Yes:374  
              Median :20.00   green: 39   Median : 0.000            
              Mean   :21.38   hazel: 48   Mean   : 1.295            
              3rd Qu.:22.00   other: 96   3rd Qu.: 2.000            
              Max.   :59.00               Max.   :14.000            
                                                                    
    tattoos       tattooed  glasses       sleep            study      
 Min.   :0.0000   No :751   No :354   Min.   : 4.000   Min.   : 0.00  
 1st Qu.:0.0000   Yes: 53   Yes:450   1st Qu.: 7.000   1st Qu.: 5.00  
 Median :0.0000                       Median : 8.000   Median :10.00  
 Mean   :0.1157                       Mean   : 7.566   Mean   :14.71  
 3rd Qu.:0.0000                       3rd Qu.: 8.000   3rd Qu.:20.00  
 Max.   :5.0000                       Max.   :12.000   Max.   :80.00  
                                                                      
       tv             movies       movies3m         sport    
 Min.   : 0.000   Min.   : 0.000   No :125   other     :132  
 1st Qu.: 2.000   1st Qu.: 1.000   Yes:679   soccer    :126  
 Median : 5.000   Median : 2.000             basketball:101  
 Mean   : 7.331   Mean   : 3.188             badminton : 99  
 3rd Qu.:10.000   3rd Qu.: 4.000             none      : 62  
 Max.   :90.000   Max.   :20.000             tennis    : 49  
                                             (Other)   :235  
        entertainment        fruit         income             rent        
 meet.friends  :244   strawberry:146   Min.   :    0.0   Min.   :   0.00  
 comp.vid.games:141   other     :121   1st Qu.:  126.0   1st Qu.:   0.00  
 movies        :101   melon     : 99   Median :  200.0   Median :  46.50  
 other         : 63   apple     : 79   Mean   :  329.4   Mean   :  86.09  
 surf.web      : 63   banana    : 76   3rd Qu.:  300.0   3rd Qu.: 150.00  
 parties       : 56   grapes    : 72   Max.   :25000.0   Max.   :1000.00  
 (Other)       :136   (Other)   :211                                      
    clothes             hair           tobacco        smokes   
 Min.   :   0.00   Min.   :  0.00   Min.   :  0.000   No :742  
 1st Qu.:  20.00   1st Qu.: 15.00   1st Qu.:  0.000   Yes: 62  
 Median :  50.00   Median : 25.00   Median :  0.000            
 Mean   :  95.74   Mean   : 31.83   Mean   :  2.062            
 3rd Qu.: 100.00   3rd Qu.: 40.00   3rd Qu.:  0.000            
 Max.   :1000.00   Max.   :350.00   Max.   :150.000            
                                                               
    alcohol       buy.alcohol    sendtxt         receivetxt      txts    
 Min.   :  0.00   No :439     Min.   :  0.00   Min.   :  0.00   No : 13  
 1st Qu.:  0.00   Yes:365     1st Qu.: 10.00   1st Qu.: 10.00   Yes:791  
 Median :  0.00               Median : 20.00   Median : 20.00            
 Mean   : 11.83               Mean   : 28.74   Mean   : 29.36            
 3rd Qu.: 20.00               3rd Qu.: 40.00   3rd Qu.: 40.00            
 Max.   :200.00               Max.   :127.00   Max.   :127.00            
                                                                         
     country              status   
 NZ      :248   International:132  
 China   :182   NZ.Citizen   :484  
 SKorea  : 54   NZ.Resident  :188  
 HK      : 39                      
 Malaysia: 38                      
 S.Korea : 34                      
 (Other) :209
~~~

## Getting help

As noted, all of the functions used above have one required argument. We may
not always know enough about a function to use it correctly. In these cases
two useful tools for learning more about a function are ```args()``` and
```help()```.

~~~r
args(summary)
~~~
~~~
function (object, ...) 
NULL
~~~

For more detailed information, use ```help()```, which opens the help
page for the function used as the argument. Help pages often include example
code for using a function.

~~~r
help(summary)
~~~

## Manipulating data with dplyr

```dplyr``` is a package that is included with the ```tidyverse```, and which
provides robust features for manipulating data. A strength of ```dplyr``` is
its human-readability.

A full demonstration of ```dplyr``` is beyond the scope of this tutorial. Here
we will focus on some commonly used functions.

### Selecting data

The ```select()``` function allows us to subset data by columns. Let's say
we want to subset the data by sex, age, and whether or not the individuals 
surveyed have tattoos. 

~~~r
ugss %>%
  select(sex, age, tattoos, tattooed)
~~~

Alternatively, we may be interested in the number of hours spent studying per
week, by age.

~~~r
ugss %>%
  select(age, study)
~~~

### Filtering data

the ```select()``` method by itself returns all columns for a a subset of rows.
The ```filter()``` function allows us to subset data by rows, where the values
of a specified variable across rows meet a given condition.

For example, we may want to subset the data to survey respondents under the age
of 25.

~~~r
ugss %>%
  filter(age < 25)
~~~

We can specify multiple conditions. For everyone between the ages of 20 and 25, 
we can add a second condition:

~~~r
ugss %>%
  filter(age >= 20 & age < 25)
~~~

Using ```select()``` and ```filter()``` together provides powerful data
subsetting capabilities.

For example, depending on our research question we may want to exclude people
without tattoos from a demographic description of the tattoo data.

~~~r
ugss %>%
  select(sex, age, tattoos, tattooed) %>%
  filter(tattooed == "Yes")
~~~

Or maybe we are most interested in the study habits of adults aged 18-22, which
(may) capture the majority of undergrads in the study population. (Note that 
without more information about the population of study, we don't know if this 
is an accurate assumption!)

~~~r
ugss %>%
  filter(age >= 18 & age <= 22) %>%
  select(age, study)
~~~

### Grouping and summarizing data

The data in the *All of US* public data browser are aggregated at different
levels - sex, age, etc. In order to arrive at similar statistics with the
```ugss``` dataset, we need to group the data using the ```group_by()```
function. Statistics can then be calculated by group.

Let's group our age and hours spent studying subset by age.

~~~r
ugss %>%
  filter(age >= 18 & age <= 22) %>%
  select(age, study) %>%
  group_by(age)
~~~

You may notice that the output is no different from before we grouped the data!
Groups exist logically. In order to "see" them, we need to calculate some
statistic based on group membership. We use the ```summarize()``` function to
do this.

~~~r
ugss %>%
  filter(age >= 18 & age <= 22) %>%
  select(age, study) %>%
  group_by(age) %>%
  summarise(average_time_studying = mean(study))
~~~

It's worth highlighting that throughout this process of data manipulation we
have not altered the underlying raw data. We want to leave our data intact,
but we may also be interested in saving our aggregations. Once we are happy
with the result, we can do that by assigning the output to a new object.

~~~r
age_study <- ugss %>%
  filter(age >= 18 & age <= 22) %>%
  select(age, study) %>%
  group_by(age) %>%
  summarise(average_time_studying = mean(study))
~~~

To see the output, we call the new object

~~~r
age_study
~~~

We can quickly inspect the ```age_study``` object with ```var.info()```.

~~~r
var.info()
~~~

Data can be grouped according to multiple variables. It may make sense to group
our tattoo subset by sex and age. We will also generate a count statistics
for each group. 

~~~r
ugss %>%
  select(sex, age, tattoos, tattooed) %>%
  filter(tattooed == "Yes") %>%
  group_by(sex, age) %>%
  summarize(count = n())
~~~

If this looks good, we will save to a new object.

~~~r
age_sex_tattoos <- ugss %>%
  select(sex, age, tattoos, tattooed) %>%
  filter(tattooed == "Yes") %>%
  group_by(sex, age) %>%
  summarize(count = n())
~~~

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

~~~r
ggplot(age_study, aes(x = age, y = average_time_studying))
~~~

When we execute this code cell, the output is an empty plot. The axes are
labeled, but the data haven't actually been plotted. This is because
```ggplot()``` needs to know how we intend to represent the data. We use
geometries to do this.

Let's use a "count" plot.

~~~r
ggplot(age_study, aes(x = age, y = average_time_studying)) +
  geom_col()
~~~

The output is a plot of average time spent studying by age, for study
participants between 18-22 years of age. 

By way of demonstration, we can also combine ```dplyr``` and ```ggplot``` 
functions for a bigger picture  view. This time we will include
all of the observations.

~~~r
ugss %>%
  select(age, study) %>%
  ggplot(aes(x = age, y = study)) +
  geom_point()
~~~

This gives us a different sense of the distribution across the full dataset.
We can make the plot a little more informative by setting some of the style
arguments in the ```geom_point()``` layer.

~~~r
ugss %>%
  select(age, study) %>%
  ggplot(aes(x = age, y = study)) +
  geom_point(alpha = 0.5, size = 3.0, color = "blue")
~~~

We will also visualize our tattoo data. Since we grouped by both age and sex,
it makes sense to add a facet layer to separate the plots by groups.

~~~r
ggplot(age_sex_tattoos, aes(x = age, y = count))
~~~

Add a geometry. 

~~~r
ggplot(age_sex_tattoos, aes(x = age, y = count)) +
  geom_col()
~~~

Note that the resulting plot does not include information about respondents'
sex, even though that data is included in our subset. One way to represent
those data in the plots is to facet by sex.

~~~r
ggplot(age_sex_tattoos, aes(x = age, y = count)) +
  geom_col() +
  facet_wrap(~ sex)
~~~

### Customizing plot layout

Once we have arrived at an informative plot, we can change the default layout
and labels.

~~~r
ggplot(age_sex_tattoos, aes(x = age, y = count)) +
  geom_col(fill = "blue") +
  facet_wrap(~ sex) +
  labs(title = "Count of respondents with tattoos",
  subtitle = "By sex and age",
  x = "Age",
  y = "Count")
~~~

We can also change the default theme.

~~~r
ggplot(age_sex_tattoos, aes(x = age, y = count)) +
  geom_col(fill = "blue") +
  facet_wrap(~ sex) +
  labs(title = "Count of respondents with tattoos",
  subtitle = "By sex and age",
  x = "Age",
  y = "Count") +
  theme_light()
~~~

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




