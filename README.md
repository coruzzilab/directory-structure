
Coruzzi lab suggested analysis directory structure
======

Update: 2020-04-15


Starting material
======
Guidelines:

1. [A Quick Guide to Organizing Computational Biology Projects](https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1000424)
2. [Good enough practices in scientific computing](https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1005510)
3. [How to share data with a statistician](https://github.com/jtleek/datasharing/blob/master/README.md).
4. [Data Organization in Spreadsheets](https://www.tandfonline.com/doi/full/10.1080/00031305.2017.1375989)


Directory structure
======

## A bare-bone structure 

```
.
├── data
├── doc
├── README.md
├── result
└── src
```

To create this bare-bone structures, you can put `mkproject` function in your `.bashrc`. Each time you make a new project directory, you can simply run `mkproject  projectname`.

```shell
mkproject() {
    mkdir -p $1/{data,src,result,doc}
    touch $1/README.md
}
```

## An example with some details

Directories/folders are in **bold**. 


Some suggestions:

1. Writing a description at the beginning of the script, and clear comments along with the script, so it is easier for someone else to find the relevant parts, and to understand the logic.
2. Providing an example for input and output files (small ones for testing), as well as an example for a command.
3. Providing a `README` file for each project, describing the purpose of this project, data origin and analysis methods.
4. When file numbers expanding, please use *sub-directories* to organize. 


+ **ProjectAwesome**
    + **data**
        + **raw_fastq**
        + **trim_fastq**
        + **aligned_bam**
        + ...
    + **src**
        + **functions**
        + **model_simplification**
        + 01_data_prep.sh
        + 02_adapter_trimming.slurm
        + 03_STAR_alignment.slurm
        + 04_DEG_analysis.R
        + 05_analysis.py
        + ...
    + **result**
        + **featureCount**
            + featureCount_output.tsv
            + featureCount.log
        + **DEG_limma**
        + **DEG_limma_20200408**
        + **DEG_DESeq2**
        + ...
    + **doc**
        + experimental_design.md
        + sample_description.md
        + DEG_summary.md
        + paper_in_progress.docx
    + `README.md`


Git and Github integration
======

**Git** version controls your code and **Github** host your code and version control history on cloud (for free!).

Tutorial: [Happy Git and GitHub for the useR](https://happygitwithr.com/)

For Git and Github, I usually don't syn `data` and `result` directory. You can add ignore those two directories in the `.gitignore` file.

```
# Ignore directories.
data/
result/
```

You can also create `.gitignore` files in sub-directories. For example, in the `src` directory, I ignore `.snakemake` and `log` files. Users should decide what files are essential for reproducibility and worth version control.

```
# Ignore snakemake log files
.snakmake/
log/
```

For **R** projects, the **[Project-oriented workflow](https://www.tidyverse.org/blog/2017/12/workflow-vs-script/)** (please read) is highly recommended. You can easily set up in RStudio. If you don't use RStudio, you can adopt the idea. Manny has a [video tutorial](https://www.youtube.com/watch?v=lQw6WHWAhQw). 

For **Python**, the [Python Best Practices – The only guide to become Python Expert](https://data-flair.training/blogs/python-best-practices/) is a good starting point. 
Also, [30 Python Best Practices, Tips, And Tricks](https://towardsdatascience.com/30-python-best-practices-tips-and-tricks-caefb9f8c5f5) for ideas, and for adding some fancy stuff very easily. 
Some tips for mantaining your code over time [Best Practices for Managing Your Code Library](https://pbpython.com/best-practices.html).

File Storage
=======

1. Do your analysis in your `$SCRATCH` directory (5TB/user). **All inactive files older than 60 days will be removed.** Remember to backup your files in `$ARCHIVE` and/or **Google Drive** (using [rclone](https://wikis.nyu.edu/display/NYUHPC/Transferring+files+between+the+HPC+Prince+Cluster+and+Google+Drive)). NYU has **unlimited** Google Drive storage space.
2. When working with large quantity of small files and intense I/O, `$BEEGFS` is recommended (2TB/user).
3. Large genome sequence, index, annotation files can be stored in `/scratch/cgsb/coruzzi` for easy access. 
We currently have a large collection of plant genomes (Gil collected for the BigPlant genomes analysis), and transcriptomes that we sequneced (from both the EvoNet and the Gymnosperms projects).
This is a huge resource for comparative genomics and evolutionary analyses. Gil has a record for each genome, which version was downloaded, from which database (with a link), and a PDF copy of the publication.

In addition, we currently have two grants for sequencing plant genomes:
1. The new Zegar grant - Sequencing 8 grass genomes (from the Aristida genus). Project that deals with the evolution of C3->C4 photosynthesis, annuality <-> perenniality transitions, and drought adaptation.
2. The Living Fossils project - Sequencing 5 huge gymnosperm genomes. Project that deals with genomic characterisitcs of diverging vs. not diverging gymnosperm lineages.

Extra Note
======

1. Always store you data in the **[tidy format](https://vita.had.co.nz/papers/tidy-data.pdf)**. The key ideas are:
    1. Each variable forms a column.
    2. Each observation forms a row.
    3. Each type of observational unit forms a table.


Contributors
=======

Ji Huang([@timedreamer](https://github.com/timedreamer)), Gil Eshel([@GilEshel](https://github.com/GilEshel))
