# Motivation 
In general, operating in academia means most projects will be geared towards eventual publication. Our goal is not just to share results, however, but to help people understand the analyses we did. All publications from our group will therefore include some way of accessing the associated data and scripts. However, this gets us only partway towards our goal of **replicable** and **understandable** analyses. Project materials need to be well organized and thoroughly documented (not just "accessible") in order for other people to follow what was done. This will also help other lab members, if at some point someone wants to follow up on your project, expand the scope of data you collected, or apply similar analyses to their data sets. This goal of making your work accessible, replicable, and understandable shapes the workflow I will ask you to use.  

# Workflow
I suggest that you organize background material, data, scripts, outputs, etc. in a "project folder" - a collection of all materials used for a project, contained within a single directory. This concept is described [in these slides](https://djnavarro.net/slides-project-structure/#1) and [here](https://martinctc.github.io/blog/rstudio-projects-and-working-directories-a-beginner%27s-guide/). I've set up a [template project folder](https://github.com/ZoopEcoEvo/project_template) that we'll generally use to get your work started. As you can probably already tell, we'll use Git and GitHub to version control your work, to collaborate and review code, as well as share data and results. Project folders and GitHub integrate nicely, and we'll use a specific workflow while developing projects and writing code based on "GitHub flow".
- See [here](https://docs.github.com/en/get-started/quickstart/github-flow) for the GitHub description of this approach and [here](https://www.djmannion.net/code_review/) for more details on how it's applied in a research lab setting.

## Initial Setup
This workflow tends to "just work" once everything is set up. However, there's a fair amount of stuff to work out before you get to that point. Luckily, these are generally a one-time investment (per machine, that is). 
- You should already be added to the organization as a member, but if not, remind me.
- Install [R and RStudio](https://posit.co/download/rstudio-desktop/).
- Make sure you have [git](https://git-scm.com) installed on your local machine by this point. There are some helpful instructions [here](https://happygitwithr.com/install-git.html) if needed. 
- Make sure you've got the connections between Git, GitHub, and RStudio worked out. See [here](https://happygitwithr.com/connect-intro.html) for a nice walk-through. We will generally use HTTPS when working with GitHub in RStudio.
- It's a good idea to have a basic familiarity with the terminology of Git and GitHub before you really dive in. See:
    - [Here](https://github.com/git-guides) for the GitHub documentation, including separate pages for [commits](https://github.com/git-guides/git-commit), [pulling](https://github.com/git-guides/git-pull), and [pushing](https://github.com/git-guides/git-push). Note that while these pages assume you'll be working with Git in the command line, rather than RStudio, the general descriptions still apply.
    - [Here](https://dx.doi.org/10.7287%2Fpeerj.preprints.3159v2) for a very in-depth written intro.
    - [Here](https://www.youtube.com/watch?v=eWxxfttcMts&t=82s) for a quick video introduction (starts at ~1:20).
    - [Here](https://www.youtube.com/watch?v=KjLycV1IWqc) for a nice visual representation of some of the basis Git/GitHub actions.
    - [Here](https://youtu.be/sxErFMF7BJY) for a walk-through of a fairly similar Git/GitHub/RStudio workflow. There's some differences (or things you won't have to worry about because I will take care of it for you), but the sections on 'Creating an RStudio project from version control' and 'Working with Git from within RStudio' are definitely relevant. 
    
## Project Setup  
- Typically, we'll work together to design a project from background justification to experimental design (always feel free to come to me with new project ideas at any stage though!). When setting up a project, it’s recommended to follow a **GitHub first, RProject second** approach. I will set up a repo for the project on GitHub as part of the ZoopEcoEvo organization. The main benefits of this are that: 
    1. The project_template repo includes a pre-determined directory structure, appropriate file paths, .Rmd YAMLs, etc. to help minimize how much set-up time is required from you. 
    2. This will keep all projects in a central location to make it easier to find relevant code and data.
- To clone the repo onto your local machine, copy the site path by clicking the green “< > Code” button in the top right corner of the repo structure. Typically, we’ll use HTTPS, so make sure this option is selected. The link can be copied by clicking the overlapping squares icon to the right of the text.
- Open RStudio and make a new project. **Select version control** (not new directory). In “Repository URL”, paste the URL for the GitHub repository that you copied above. Make sure that you keep your project folders organized on your local machine - I recommend having a single directory called “Lab_Projects” or something similar that you use to store all project folders.
- You’ve now got a copy of the repo downloaded onto your local machine, which is linked to GitHub. The main branch of every project is read only (i.e. - you likely won't be able to directly modify the content). This is because the main branch represents the official “up to date” record of your project. To make changes, you’ll do all active development of the project on a separate branch, which can then be merged into the main branch. This adds a little complexity to the workflow, but means that you can freely explore any direction without worrying about losing progress you’ve already made; you can always just restore to the most recent stable version.

## Project Development  
- There's many (many, many, many) resources out there that can help you learn R, brush up on what you already know, and build up new skills. I see developing your R coding skills as an important part of your training, and feel that time and energy devoted to this is a good investment. As discussed below, your coding style is mostly up to you. You should know, however, that I primarily work with the "tidyverse", and recommend that you do too. There's an excellent resource for learning to code in R using this approach [here](https://r4ds.had.co.nz).
- When you’re ready to start working on the project, open RStudio **via the .Rproj file**. This will open an RStudio session with the correct settings and (most importantly) the correct working directory. This makes it easier to transfer your project across machines without breaking file paths. 
- Make a new branch (purple connected-square icon in the top right corner of the Git pane of RStudio). Give this branch an informative name about the goal you’re working towards - exp_design, data_carpentry, linear_model, etc. This will help me keep track of the project status). You should see this branch appear on the GitHub repo as well.
- Begin populating the project with code and text. As you work on the development of the project, you can take snapshots of the code progress using "commits", and store these snapshots on the virtual copy of your branch by "pushing" to GitHub. A good rule of thumb is to commit whenever you finish something you’d be annoyed to lose. Make sure your commit messages are concise but useful (see [here](https://cbea.ms/git-commit/) for a nice approach).
- If you're the only one working on your code, you can focus on just your working branch. If other people are working on this project as well, however, **make sure you keep your branch up-to-date** with what’s happening on the main branch (if you don’t, you risk ending up with major conflicts when you go to merge your branch back into main). It’s a good idea to "pull" the up-to-date code from the GitHub repo at the beginning of every session to keep the local and virtual copies of your working branch in sync. 
    - If others are working on the code as well, enter this into the **terminal** (not the console) at regular intervals to update your working branch with the contents of the main branch: **git pull origin main**

## Coding Style and Documentation
- Opening up an unfamiliar data set or script and attempting to understand what was done during an analysis can be a daunting task (almost as daunting as writing the script in the first place). As you work on your code, keep its "legibility" in mind - not only will this help other people understand your code, but it will help *you* understand the code if you return to a project and find you've forgotten what's been done (and trust me, you will forget). 

#### Style
- As you code more, you will develop your own "coding style" (a series of decisions you make about alignment and spacing of code, naming of variables and functions, commenting strategies, script structuring, etc. with the goal of promoting code clarity and interpretability). Developing your own style is a *good thing*, as it makes coding feel more natural. I will generally not, therefore, dictate minor stylistic decisions; so long as your code is understandable, feel free to write however you'd like. That being said, there are two levels of consistency you need to consider: 
    - **Internal consistency** - Your code needs to be consistent within each project (and especially within each script). Changing up how variables are named, indentation strategies, etc. can make it more difficult to follow the overall flow of an analysis. 
    - **General coding style** - At some point, you may find yourself working on several projects at the same time. Having a consistent coding style will make it easier to switch between projects. Keeping track of the small style details for each project quickly becomes frustrating, and can keep you from reaching your "flow state" (that state of mind where you are fully immersed in the problem you're trying to solve). Sometimes it's helpful to keep a "style guide" document where you can keep track of your naming conventions and other stylistic decisions until they become second nature. 
- For some in depth examples of what goes into a "coding style" see [here](https://www.r-bloggers.com/2019/01/🖊-r-coding-style-guide/) and [here](https://style.tidyverse.org/index.html).

#### Commenting 
- There is a fine line between over- and under-commenting on code. How you choose to comment on your code is part of your personal coding style, but there are some best practices you should keep in mind (see [here](https://stackoverflow.blog/2021/12/23/best-practices-for-writing-code-comments/) for some useful non-R-specific tips). 
    - Comments should most often detail *why* something was done, and only rarely *how* it was done. Keep in mind that good comments do not excuse unclear code.
    - Similarly, comments shouldn't duplicate the code. Not every line needs a comment associated with it detailing what it's doing.
    - If you're pulling code from elsewhere, cite it! This might be from a paper's supplemental materials, a StackOverflow post, or a tutorial. In all cases, give clear attribution.
    - Rules are meant to be broken. These best practices are aimed at making code interpretable. Part of this is avoiding visual clutter. However, if you find it helps to comment more frequently as you start out, do that. 

#### README Files
- README files are crucial. These act as a roadmap for the project, which is especially important for the project folder setup we will generally use - keeping track of which scripts do what, and how they're connected is going to be a big help for anyone trying to understand your analyses. These files require substantial effort, and should not be treated as an afterthought. 
- There are many different examples of how a README could be compiled and structured. The general format I recommend using is [here](https://github.com/ZoopEcoEvo/project_template/blob/main/README.md) (this is what is included in the project folder template). This reflects information, suggestions, and advice from the American Naturalist ([here](https://www.journals.uchicago.edu/journals/an/instruct) and [here](http://comments.amnat.org/2021/12/)), [Dryad](https://datadryad.org/stash/best_practices) (a popular data repository), and [Cornell](https://data.research.cornell.edu/content/readme).

## Pull Requests
- When you’re ready for feedback on the code, you will initiate a pull request (PR). This starts the Code Review process. I will automatically be notified, but mention any other lab member in the PR that you’d like to look over your code (just be mindful about how much time you’re asking from other lab members).
- Before you initiate the PR, make sure your local branch is up to date by doing one last pull-push cycle from RStudio. This will make sure that:
    1. your local code reflects the most up-to-date version on the repo to catch any last merge conflicts, and
    2. that your branch on the virtual repo reflects all the changes you've made. 
- To initiate the PR, click “New Pull Request” **on GitHub**. This should be visible when viewing the active branches tab. Doing this manually on GitHub rather than through RStudio is the easiest way to start the PR.
- During code review, we will typically start by looking over the output (either the HTML or the github doc/markdown in the Reports directory) since this should include both code and graphical outputs. Be sure to specify if there are other additional files you're looking for feedback on. Depending on time available and complexity of the code, we may also review the scripts involved (data processing, .Rmd, etc.). We’ll make comments and suggestions for changes, or accept the PR and merge the development branch into the main branch. Once merged, this now stands as the new official version, and you can start a new branch to work on the next project development goal.

## Publishing Projects
- Project folders are also set up to help integrate figures, statistical results, etc. into the manuscript writing process. By keeping all relevant files in the same project folder, and using the controller script to weave different components together, it should be easier to write (and then update) a manuscript draft with the correct results. For example, smart usage of inline code will save you from having to manually update statistical results in tables and text throughout the draft when changes are made (saving time and helping to avoid confusion down the road!). 
- There should be a directory entitled "Manuscript" within each project folder, which includes a .Rmd file (the manuscript file), along with .sty and .bib files (containing formatting details and the bibliography, respectively). By default, these will produce a PDF formated in the Arxiv style and a word document when the .Rmd file is knit. This is different from the report .Rmd file (which by default outputs an HTML and special markdown file) - the main difference here being that code chunks do not appear in the PDF or word documents, while they do in the HTML and markdown outputs.  
- The .Rmd file name should be updated to reflect the manuscript. Typically we will format the file name as it would be referred to in an in-text citation (ex - LeadAuthor_et_al_2022, Author1_and_Author2_2022, etc.).
- Keep the use of code within the manuscript .Rmd file to a minimum. All major data analysis and figure generation should be performed in other scripts within the project folder. When placing figures, for example, it will be substantially faster to use the image files output by the Report.Rmd file than to create the figures from code. Given the number of times you'll likely knit a manuscript during the writing and revision process, this saved time adds up. It is therefore in your best interest to ensure that the report.Rmd file (or whichever script is outputting the image files) reflects publication-ready figures whenever possible. 
- The use of a reference manager is strongly recommended. RStudio has a built in citation function, but the ability to store and organize references outside of the project is also useful. [Zotero](https://www.zotero.org) is an open source reference manager that integrates nicely with RStudio and markdown documents. This is the program I use/recommend. There's a useful write up of how citations work in .Rmd files [here](https://posit.co/blog/rstudio-1-4-preview-citations/). Note, you'll need to be using RStudio version 1.4 or later to access these features. 
- The workflow for writing the manuscript draft will be similar to that used during the Project Development phase, at least while putting together the initial versions. Changes are made on a working branch, which are reviewed via Pull Request. If comments are required from co-authors who do not use GitHub, it is the responsibility of the lead author to ensure they are sent an up-to-date word document (or Google Doc version) and that their comments are properly integrated into the GitHub repo. 
- Once the manuscript is drafted, the repo can be archived with Zenodo in order to establish a Version of Record with an associated DOI. See [here](https://docs.github.com/en/repositories/archiving-a-github-repository/referencing-and-citing-content) for more details. 
- Once the new repo DOI is included in a Data Availability statement in the manuscript, it's ready for submission. The .Rmd file is knit and the resulting PDF and word documents are prepared for submission to a preprint server and journal, respectively.  
 
## General Notes
This process is iterative! And while it might take some time and effort to get the code worked out, this will hopefully help to develop your coding skills and catch potential mistakes before they get embedded in papers and presentations. Equally important, it distributes the responsibility for checking the code across the group - If we all benefit from your work, we should all share some of this burden. 

In addition to the development of projects through code, you can contribute valuable insights to the development of the lab as a whole by writing up the “invisible” work that you did - what did it take to get to a point where you could begin to engage with the project work flow? Did you find any useful resources that helped you? Are there aspects that were confusing or poorly explained to you? Were there obstacles that could be removed? After working with these systems for a while, it's difficult to accurately remember what it’s really like to be faced with these challenges for the first time - your insights here can help design as smooth an onboarding experience as possible!
- See [here](https://www.catharsisinsight.com/reports) for the initial inspiration for this.
