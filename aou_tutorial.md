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

## Create a Jupyter Notebook in Colab

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
```[1] 144```

A cell can contain multiple lines of code. Note that in the next code cell,
we are using the ```<-``` symbol as the assignment operator. This is the
conventional syntax for object and variable assignments in R.

~~~r
a <- 5
b <- 3
print(a ** b)
~~~
```[1] 125```

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
>```125```  
>```243```

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
```
'.GlobalEnv''package:VGAMdata''package:VGAM''package:splines''package:stats4'
'package:lubridate''package:forcats''package:stringr''package:dplyr'
'package:purrr''package:readr''package:tidyr''package:tibble''package:ggplot2'
'package:tidyverse''package:varhandle''jupyter:irkernel''package:stats'
'package:graphics''package:grDevices''package:utils''package:datasets'
'package:methods''Autoloads''package:base'
```

## Load the data

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


## Resources

[^1]: Thomas W. Yee (2015). Vector Generalized Linear and Additive Models: 
With an Implementation in R. New York, USA: Springer.



