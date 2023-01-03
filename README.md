# Workflow
Project folders and GitHub integrate nicely. We use a specific workflow while developing projects and writing code based on "GitHub flow".
- See [here](https://docs.github.com/en/get-started/quickstart/github-flow) and [here](https://www.djmannion.net/code_review/) for more details.

## Project Setup  
- Typically, we'll work together to design a project, from background justification to experimental design. When setting up a new project, it’s recommended to follow a **GitHub first, RProject second** approach. I will set up a repo on GitHub, as part of the ZoopEcoEvo organization (the main benefit here is that the project_template repo includes a pre-determined directory structure, appropriate file paths, .Rmd YAMLs, etc. to help minimize how much set-up time is required from you)
    - You should already be added to the organization as a member, but if not, remind me.
    - Make sure you have git installed on your local machine by this point.
- Copy a link to the clone of this repo to your clipboard by clicking the green “< > Code” button in the top right corner of the repo structure. Typically, we’ll use HTTPS, so make sure this option is selected first. The link can be copied by clicking the overlapping squares icon to the right of the text.
- Open RStudio and make a new project. **Select version control** (not new directory). In “Repository URL”, paste the URL of your new GitHub repository that you copied above. Make sure that you keep your project folders organized on your local machine - I recommend having a single directory called “Lab_Projects” or something similar that you use to store all local copies of the GitHub repos.
- You’ve now got a copy of the repo downloaded onto your local machine, which is linked to GitHub. The main branch of every project is read only - in practice, this means that it should be the most “up to date” official record of your project. You’ll do all active development of the project on a separate branch, which can then be merged into the main branch. This adds a little complexity to the workflow, but means that you can freely explore any direction without worrying about losing progress you’ve already made; you can always just restore to the most recent stable version.

## Project Development  
- When you’re ready to start working on the project, make a new branch (purple connected-square icon in the top right corner of the Git pane of RStudio). Give this branch an informative name about the goal you’re working towards - exp_design, data_carpentry, linear_model, etc. This will help me keep track of the project status). You should see this branch appear on the GitHub repo as well.
- Begin populating the project with code and text. As you work on the development of the project, commit and push to your branch as you would normally work. A good rule of thumb is commit whenever you finish something you’d be annoyed to lose. Make sure your commit messages are concise but useful (think email subject headers).
- If you're the only one working on your code, you can focus just on your working branch. If other people are working on this project as well, however, **make sure you keep your branch up-to-date** with what’s happening on the main branch (if you don’t, you risk ending up with major conflicts when you go to merge your branch back into main). It’s a good idea to pull at the beginning of every session to keep the local and virtual copies of your working branch up to date. If others are working on the code as well, enter this into the terminal at regular intervals to update your working branch with the contents of the main branch: **git pull origin main**

## Pull Requests
- When you’re ready for feedback on the code, you will initiate a pull request (PR). This starts the Code Review process. I will automatically be notified, but mention any other lab member in the PR that you’d like to look over your code (just be mindful about how much time you’re asking from other lab members).
- To initiate the PR, make sure your local branch is up to date and then click “New Pull Request” **on GitHub**. This should be visible when viewing the active branches tab. Doing this manually on GitHub rather than through RStudio is the easiest way to start the PR.
- During code review, we will typically start by looking over the output (either the HTML or the github doc/markdown in the Reports directory), so make sure this is a good summary of what you want feedback on. Depending on time available and complexity of the code, we’ll also review the scripts involved (data processing, .Rmd, etc.). We’ll make comments and suggestions for changes, or accept the PR and merge the development branch into the main branch. This now stands as the new official version, and you can start a new branch to work on the next project development goal.

## Publishing Projects
- Once the project has been completed and is ready for publication, the repo can be archived with Zenodo in order to establish a Version of Record with an associated DOI. 
    - See [here](https://docs.github.com/en/repositories/archiving-a-github-repository/referencing-and-citing-content) for more details. 
- Project folders are also set up for seamless integration of figures, statistical results, etc. into the manuscript writing process. By keeping all relevant files in the same project folder, and using the controller script to weave difference components together, it should be easier to write (and then update) a manuscript draft. For example, when done properly, it should save you from having to update statistical results in tables and text throughout the draft when changes are made (saving time and helping to avoid confusion down the road!). Within each project folder should be a directory entitled "Manuscript", which includes a .Rmd file, along with .sty and .bib files. By default, these will produce a PDF (formated in the Arxiv style) and a word document. 
- Once the project has reached the publication preparation stage, update the name of the .Rmd file (typically we will format the file name as it would be referred to in an in-text citation (ex - LeadAuthor_et_al_2022, Author1_and_Author2_2022, etc.).
- Keep the use of code within the manuscript .Rmd file to a minimum. All major data analysis and figure generation should be performed in other scripts within the project folder. When placing figures, for example, it will be substantially faster to use the image files output by the Report.Rmd file than to create the figures from code. Given the number of times you'll likely knit a manuscript file, this saved time adds up. It is therefore in your best interest to ensure that the report.Rmd file reflects publication-ready figures whenever possible. 
- The use of a reference manager is strongly recommended. RStudio has a built in citation function, but the ability to store and organize references outside of the project is also useful. [Zotero](https://www.zotero.org) is an open source reference manager that integrates nicely with RStudio and markdown documents, and is the recommended program. 
 
## General Notes
This process is iterative! And while it might take some time and effort to get the code worked out, this will help to develop your coding skills and catch potential mistakes before they get embedded in papers and presentations. More importantly, it distributes the responsibility for checking the code across the group - If we all benefit from your work, we should all share some of this burden. 

In addition to the development of projects through code, you can contribute valuable insights to the development of the lab as a whole by writing up the “invisible” work that you did - what did it take to get to a point where you could begin to engage with the project work flow? Are there aspects that were confusing or poorly explained to you? Were there obstacles that could be removed? I’ve probably spent too much time working with these systems to accurately remember what it’s really like to be faced with these challenges for the first time - your insights here can help design as smooth an onboarding experience as possible!
- See [here](https://www.catharsisinsight.com/reports) for more details.
