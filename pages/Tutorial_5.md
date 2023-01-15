Part 5 - R Markdown
================
Matthew Sasaki

- <a href="#markdown" id="toc-markdown">Markdown</a>
  - <a href="#setting-up-your-r-markdown"
    id="toc-setting-up-your-r-markdown">Setting up your R Markdown</a>
  - <a href="#yaml-yet-another-markup-language"
    id="toc-yaml-yet-another-markup-language">YAML (Yet Another Markup
    Language)</a>
  - <a href="#text-formatting" id="toc-text-formatting">Text Formatting</a>
  - <a href="#code-chunks" id="toc-code-chunks">Code Chunks</a>
  - <a href="#inline-r-code" id="toc-inline-r-code">Inline R Code</a>
- <a href="#output-formats" id="toc-output-formats">Output Formats</a>
  - <a href="#pdf-outputs" id="toc-pdf-outputs">PDF Outputs</a>
  - <a href="#html-outputs" id="toc-html-outputs">HTML Outputs</a>
    - <a href="#code-folding" id="toc-code-folding">Code Folding</a>
    - <a href="#table-of-contents" id="toc-table-of-contents">Table of
      Contents</a>
    - <a href="#interactive-tables--figures"
      id="toc-interactive-tables--figures">Interactive Tables &amp;
      Figures</a>
- <a href="#integrating-into-a-workflow"
  id="toc-integrating-into-a-workflow">Integrating Into a Workflow</a>

It is unavoidable that, at some point, you will need to communicate the
results of your analyses. It’s also likely that you will need to share
different components of your analyses (code, visualizations, written
reports, etc.) with different people. The traditional process may entail
performing your analyses in R, exporting your figures and tables, and
then manually inserting them into a word document with the written
summary of your results. Alongside this written summary, you will then
have to share the underlying code and raw data for those who are
interested. For collaborators that don’t use R, you will likely have to
provide additional information on what specifically you did to process
and analyze the data. We will talk more about streamlining and
organizing your workflow in the sixth and final tutorial in this series.
An essential component worthy of it’s own tutorial, however, is the R
Markdown (.Rmd) file.

# Markdown

After investing time and effort in learning the R coding language, you
probably don’t want to hear “time to learn another language”. Before you
close this file though, let me assure you that Markdown is not only
simple, but extremely powerful when used with R analyses. Markdown is a
simple “markup” language used to format documents. R Markdown integrates
R code within this formatting framework, allowing you to more
efficiently integrate code, visualizations, and written reports. You
might imagine that this would be useful for more than just written
reports, and indeed, R Markdown can be used to create a wide variety of
outputs, including presentation slides and web pages. These tutorials
were also generated using R Markdown files. We will focus on just two
outputs, PDF and HTML versions of a document.

## Setting up your R Markdown

In RStudio, a new R Markdown file can be created in the same way as a
new script, using the page icon in the top left corner of the window.
You’ll notice a number of options in the drop-down menu, which can be
explored at your leisure. When you create a new Markdown file you’ll be
presented with a series of fields and options. Title and Author can be
filled in as appropriate. You can input a static date, or choose to use
the current date each time you knit (i.e. - run the code for) the
document. There are three primary outputs for a markdown file: an HTML,
PDF, or Word document. Each come with their own advantages, some of
which will be explored in this tutorial. Also, don’t be overly concerned
about what you enter into these fields or which options you select - all
of these can be changed using the first key component of the markdown
file, the YAML.

## YAML (Yet Another Markup Language)

The YAML appears at the top of markdown files and will set key
parameters of the document. Some key components of the YAML are explored
below. After so much time working with R syntax, the YAML may appear
strange, and almost human-readable. This is by design. However, while
these sections are typically easier to read, they are just as sensitive
to formatting (if not more so) than R code.

## Text Formatting

One of the main reasons to use an R Markdown file is Markdown itself -
simple text formatting that looks great. The basic components of a
markdown doc are:

- Plain text. Entered just as you would with any word processor.

- Headings. These are indicated using “\#”. Different levels of headings
  are indicated by different numbers of “\#” (Heading level 1 - \#,
  heading level 2 - \##, heading level 3 - \###, etc.).

- Bolded, italicized, and underlined text. To **bold** text, put two
  asterisks on either end. To *italicize*, use just one asterisk.

## Code Chunks

The other reason R Markdown documents are so powerful is the direct
integration of R code.

## Inline R Code

# Output Formats

## PDF Outputs

## HTML Outputs

As you might have guessed from the format of these tutorial pages, I
prefer to knit markdown files to HTML. I find that the formatting is
cleaner, and the results are easier to share across systems. As we’ll
see, there’s also a set of features that are unique to HTML outputs that
help make these documents far easier to share with a broad audience
(coders and non-coders alike), and help them navigate the document.
Setting up these features is also incredibly easy, as you can see below
(this is the YAML used to produce this document).

![](Figures/markdown_YAML.png)

### Code Folding

The first of these features is Code Folding. You’ll find this specified
in the first line of the html_document parameters. Below this chunk of
text, you’ll notice a small button labelled “Code” and a simple plot.
When you click this button, the code used to generate the plot will be
revealed. Click it again, and the code folds back up into the
unobtrusive button form. This feature is really useful when sending a
report to collaborators with varying coding skill/interest levels: for
collaborators that don’t care to read through the code used to analyze
the data, big chunks of code are distracting and confusing; some
collaborators care more about the code used than the written
descriptions, however, and not providing any access to the code won’t
help them as much. Code folding allows you to satisfy both parties.

``` r
random_points = data.frame("id" = c(1:100), 
                           "value" = rnorm(n = 1000, mean = 50, sd = 10)) %>%  
  filter(value < 55)

ggplot(random_points, aes(x = value)) + 
  geom_histogram(binwidth = 1) + 
  theme_bw(base_size = 24) + 
  theme(panel.grid = element_blank())
```

<img src="/Users/matthewsasaki/Desktop/R_tutorial/Output/Tutorials/Tutorial_5_files/figure-gfm/unnamed-chunk-1-1.png" style="display: block; margin: auto;" />

### Table of Contents

Along the left side of this document, you’ll find a table of contents.
The second line of HTML parameters creates the table of contents (TOC),
while the third line specifies that the TOC should ‘float’ along the
left side of the document, no matter where you scroll in the document.
The different sections and sub-sections of the TOC are determined by the
heading levels used throughout the text (#, \##, \###, or \####). These
headings are nested based on the order they are provided (e.g. - \#
Section 1, \## Sub-section 1a, \## Sub-section 1b, \### Sub-sub-section
1b-1, \# Section 2, etc.)

### Interactive Tables & Figures

# Integrating Into a Workflow
