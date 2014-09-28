DC Code Update Chart
====================

The DC Code Update Chart is a machine-readable set of instructions for how the Code of the District of Columbia has been updated by each codified act. The update chart repository also acts as a public audit log for all changes to the DC Code.

Organization of the update chart
--------------------------------

The DC Code changes in virtue of acts of the Council becoming effective, technical corrections made by Council staff, and, rarely, Congress passing federal statutes. Council staff codify these changes into the DC Code by creating machine-readable update instructions in this repository. The instructions are then applied to the DC Code by computer program in order to arrive at the Official Code of the District of Columbia.

The code update instructions are stored in effective date order. By re-playing the instructions but stopping at a particular date, it is possible to re-create what the DC Code looked like on any date since the DC Code Update Chart was first used.

Relationship to the DC Code repository
--------------------------------------

The DC Code repository at ___ is the result of applying the code update instructions stored here. That repository, and not this one, is where we recommend data consumers go first for accessing the DC Code in XML.

But this code update repository, including the `base-code` branch containing the initial contents of the code before the electronic code update chart came into use, is the data store of record. The difference becomes apparent in cases of technical corrections (see below).

As a convenience to data users, each code update instruction is saved as a separate git commit in the DC Code repository. The DC Code repository not only captures the current contents of the DC Code but also its history. Each commit has a log message indicating the DC Act or other change that is represented by the commit, and the the date on each commit is the effective date of that law or other change.

Technical corrections
---------------------

From time to time Council staff make technical corrections to the DC Code. A technical correction most often adds to or updates the Council's annotations beneath each section of the Code, but technical corrections may also change how an act was codified if it was originally codified incorrectly. In each of these cases, the machine-readable code update instructions in this repository are revised.

In the past, printed leaflets were inserted into old bound volumes of the code to indicate changes in historical material. Now, instead, the electronic code update chart is itself updated. And just as each printed leaflet in the past provided a record for how the DC Code changed, this electronic code update chart is tracked in a version control repository so that each change to the code update chart is recorded in perpetuity. You may also think of the code update chart as an audit log for the DC Code.

A technical correction will affect how past laws were codified. As a result, the commit history of the DC Code repository (at ____) will be rewritten and the HEAD hash will change. Note, again, that that repository is provided as a convenience for data users. If a repository is needed without history rewriting, use this repository instead.

File layout
-----------

Changes to the DC Code are grouped into directories at the root of this repository. A directory will typically represent changes to the DC Code due to a single act, and directories are often named according to act numbers. Each directory has a single effective date that applies to all changes to the DC Code described within it.

The contents of each directory is one or more `.patch` files. Each `.patch` file has a path (subdirectory + file name minus `.patch`) that matches a file path in the DC Code repository. The `.patch` file contains a unified diff representing update instructions to its corresponding file in the DC Code repository.

A `metadata.yaml` file at the root of this directory contains information about the changes in the directory, including whether the changes are due to a Council act (and its number) and always an effective date.

The `index.yaml` file at the root of the repository lists the directories in order of effective date.

Executing the patches
---------------------

To create the DC Code XML, we follow these steps:

1. We start with the DC Code XML in the `base-code` branch of this repository. This branch contains the state of the DC Code prior to the adoption of this electronic code update chart system. The commit hash of the base code is also stored in `index.yaml`.

2. We then take each directory one at a time following the order of the directories in `index.yaml`. For each directory:

3. Each `.patch` file in the directory is applied to the corresponding DC Code XML file.

4. After applying all `.patch` files in the directory, a detached git commit is made.

5. After working through all directories, a new tag is made and is pushed to the DC Code repository.
