# Design

In this chapter we discuss the structure of our application suite, introduce some key features and go over certain technical and design challenges we had to overcome.

## Goal

The goal of our research is to create a virtual reality visualization environment that is accessible for everyone, is easily extensible by outside developers and works on 3DOF and 6DOF HMDs, no matter whether they are connected to a personal computer or standalone. Different control styles should be taken into an account when designing interactions.

## Feature selection

We have selected a number of features to implement for our first prototype, which was made in the space of 4 months (one academic semester). These include the ability to load comma-delimited csv files into the environment, ability to update existing datasets by either overwriting the existing copy or appending a new copy (*version*), letting the user perform basic editing operations such as renaming dataset attributes, setting their data type and missing values setting and a basic dataset sharing feature.

The user should also be able to create scatter plots, position them freely around the virtual environment, adjust their rotation and scale, specify bounds for each spatial axis (*slicing*), assign dataset attributes onto spatial axes and non-spatial features such as color and size and view basic dataset metadata and statistics of attributes contained within said dataset.

Lastly, there should be integration support for popular programming languages that allows programmers to create or update datasets from their programming environment of choice. Since we cannot cater to all, we should provide the ability for outside developers to build their own integrations for other programming languages or environments.

## Component design

We have decided to divide our environment into three distinct components - Plugins, Manager and Navigator. Plugins are API integrations written for different programming languages that allow the user to create a new dataset or update an existing one. Manager enables the user to view and edit all of their datasets and also facilitates uploading files from a local computer. Navigator allows the user to interact with their data in virtual reality. The following visualization pipeline shows the distribution of tasks among our components:

![Adapted version of Haber–McNabb dataflow model for scientific visualization.](images/pipeline.pdf)[1]

### Plugins

Plugins are intended for developers or power users to incorporate dataset creation and updating functionality into their applications and scripts. We have implemented integrations for Python and R, as they are the most common programming languages used by data scientists. Manager provides a set of APIs that enable outside developers to create their own integrations and as both Manager and official plugins are open-source, it is a very straightforward process.

![Guide for adding a dataset using Python.](images/manager_python.png)

From the user's perspective, the workflow to add or update a dataset are as follows:

1. Log into Manager.
2. Access the create/update dataset modal.
3. Select programming language or environment.
4. Copy API key that is unique for user (when creating a dataset) or dataset (when updating an existing dataset).
5. Import a library in the programming environment of choice.
6. Insert an applicable command.
7. Run your program.

The following code snippet showcases the use of plugins for adding a new dataset and updating an existing one in R.

```r
cyberplot.new(swiss, id = "304a87cff875bc23522557e5beda11ff", name = "Swiss Dataset")
cyberplot.update(iris3, id = "09fee44cff6a79cdf2a6176b2ffb1008")
```

### Manager

### Navigator

![User interface of Manager.](images/manager.png)
![Options for adding a dataset.](images/manager_add.png)
![Dataset addition wizard.](images/manager_labels.png)
![Version management in Manager.](images/manager_versions.png)
![Navigator's 3DOF interface.](images/cyberplot_3dof.png)
![Navigator's 6DOF interface.](images/cyberplot_6dof.png)
![Left: Pairing prompt in Navigator. Right: Adding a new headset in Manager.](images/pairing.png)

1. https://www.sciencedirect.com/science/article/pii/S0097849304000251