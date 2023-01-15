Part 6 - Project Folders and Data Carpentry
================
Matthew Sasaki

- <a href="#project-folders" id="toc-project-folders">Project Folders</a>
  - <a href="#project-principles" id="toc-project-principles">Project
    Principles</a>
  - <a href="#the-rproj-file" id="toc-the-rproj-file">The .Rproj file</a>
  - <a href="#key-settings" id="toc-key-settings">Key Settings</a>
- <a href="#useful-tricks" id="toc-useful-tricks">Useful Tricks</a>
  - <a href="#splitting-scripts" id="toc-splitting-scripts">Splitting
    Scripts</a>
  - <a href="#dating-your-markdown" id="toc-dating-your-markdown">Dating
    your markdown</a>
  - <a href="#markdown--local-version-control"
    id="toc-markdown--local-version-control">Markdown &amp; Local “Version
    Control”</a>
  - <a href="#project-folders-and-actual-version-control"
    id="toc-project-folders-and-actual-version-control">Project Folders and
    <strong>Actual</strong> Version Control</a>

By now, you’ve had some experience importing, working with, and
visualizing data in R. Most applications will follow a similar workflow.
At the surface, this seems straightforward, but in reality analyses
often produce multiple versions of processed data, tables, and figures.
Let’s quickly walk through what might be produced in a relatively simple
analysis.

You have a set of raw data, straight from an experiment. You import this
data, and realize it needs to be cleaned up and rearranged in order for
you to do the analyses you’re interested in (new file count = 1). You
quickly make a summary table of the number of data points per group
(file count = 2). From there, you start making figures and produce a box
plot and scatter plot with regression lines (file count = 4). You need
to append a table to numerically summarize the results of the linear
regression (file count = 5). Finally, you produce a written summary of
the experiment that can be shared with collaborators (file count = 6).
After the summary is sent to your collaborators, however, someone has
suggestions for ways you could improve the figures and some of the text.
So you repeat the process (file count = 8, now with multiple versions of
some of the files). Scale this up to a full project or manuscript, and
you can see how analyses can quickly become overwhelming, and how easy
it might be to lose track of files.

By combining a standardized file structure with a .Rproj file, an R
Project folder can help organize your analyses, and makes them easier
for other people to replicate. As such, R Project Folders can also be
useful when a journal requires all code and scripts to repeat analyses
be made available.

# Project Folders

Below is a schematic of an R Project Folder called Project_A. Contained
within the project folder directory are the .RProj file, a directory for
**raw** data, a directory for your scripts, and a directory for outputs,
within which are separate directories for **processed** data and for
figures. Other directories (for Background materials and useful papers,
Presentations related to the project, or the files for the manuscript,
for example) or configurations can also be useful, depending on what
your project needs and how you like to handle your workflows. We’ll use
this skeleton project folder organization to go over the principles of
using a project folder, allowing you to more efficiently tailor this set
up to your needs. An example of a “full scale” project folder
arrangement is described at the end of this tuturial.  
![](Figures/R_Project%20Folder%20Outline.png)

## Project Principles

The main principle for a project folder is that your workflow is
**one-directional**. Raw data is processed by scripts and saved in the
Output / Data directory. This processed data is used to generate
figures, which are stored in the Output / Figures directory. These
figures are then used in reports, manuscripts, and presentations. Note
that at no time is the raw data overwritten. **This is absolutely
essential**.

## The .Rproj file

The inclusion of the .Rproj file in the home directory is essential for
the functioning of an R Project Folder. The .Rproj file serves two main
purposes, to ensure general settings are correct, and to act as an
‘anchor’ for your analyses. This file anchors the folder by setting all
file paths relative to the project folder (meaning that file paths will
be always be correct, even when the folder is shared with someone else).
You’ll notice that you rarely (if ever) will have to check or set the
working directory when using a project folder. In order for RStudio to
“know” you’re working in a specific project, the **first** thing you
will need to do when starting your session is open the .Rproj file,
which should start a new RStudio session. You will know the project is
active when you see the project name in the top right corner of RStudio.

## Key Settings

As the goal of an R Project Folder is to help, there are several default
settings in R that you will want to change. These setting changes are
one of the components organized by the .Rproj file.

1.  Never save .Rdata when closing your session. Open up your
    Preferences \> General, and make sure “Restore .Rdata into workspace
    at startup” is **not** checked. This will ensure that variables and
    other objects from your Environment are not carried over from one
    session to the next. Also ensure that “Save workspace to .Rdata on
    exit” is set to “Never”.
2.  In Preferences \> R Markdown, make sure that “Evaluate chunks in
    directory” is set to “Project”. This will make it easier to navigate
    through the component folders when setting file paths.
3.  In the drop-down menu next to the “Knit” button, ensure that “Knit
    directory” is set to “Project”.

# Useful Tricks

## Splitting Scripts

## Dating your markdown

Often, you may want to put the current date onto the output of your
markdown rather than use a fixed date. To do this, put a “date” object
in your YAML (typically after the title and author lines), and then
specify “r Sys.Date()”. This is technically in-line r code, so be sure
to replace the ” with \`.

## Markdown & Local “Version Control”

## Project Folders and **Actual** Version Control
