In this week we are taking a look at another HMM based tool, ChromHMM.

  * [Project website](http://compbio.mit.edu/ChromHMM)
  * [Manual](http://compbio.mit.edu/ChromHMM/ChromHMM_manual.pdf)

### What ChromHMM does

ChromHMM uses a multivariate HMM model to discover epigenomic features on a given chromosome.
Instead of sequence data, it uses experimental results mapping epigenomic (methylation, histone modification etc.) features to the chromosome.

## The difference from previous HMMs we have seen

  * The alphabet size is 2 (binary) : each feature either exists or not
  * There are multiple 'tracks' (sequences, variables ..) : these are multiple experiments done on the same chromosome

### How to get ChromHMM

ChromHMM is written in Java.
Java is preferred for some projects because just like Python, users do not have to compile it, but it runs much faster compared to Python.
*(It is however not quite as fast as native C/C++ and just almost as cumbersome to to code in.)*
If we have java already installed, we can [download](http://compbio.mit.edu/ChromHMM/ChromHMM.zip), unzip and be ready to run ChromHMM by doing :

```
wget http://compbio.mit.edu/ChromHMM/ChromHMM.zip
unzip ChromHMM.zip
cd ChromHMM
```

### How to run ChromHMM

As usual, the detailed specifications on how to run ChromHMM can be found in the [manual](http://compbio.mit.edu/ChromHMM/ChromHMM_manual.pdfhttp://compbio.mit.edu/ChromHMM/ChromHMM_manual.pdf).

Unfortunately, we need a specific type of data to run ChromHMM (experimental mapping of epigenomic features to chromosome) but fortunately, it comes with some sample data.

We can look at the sample data in the SAMPLEDATA_HG18 directory.
One of them looks like this :

```
GM12878	chr11
CTCF	H3K27ac	H3K27me3	H3K36me3	H3K4me1	H3K4me2	H3K4me3	H3K9ac	H4K20me1	WCE
0	0	0	0	0	0	0	0	0	0
0	0	0	0	0	0	0	0	0	0
0	0	0	0	0	0	0	0	0	0
0	0	0	0	0	0	0	0	0	0
0	0	0	0	0	0	0	0	0	0
0	0	0	0	0	0	0	0	0	0
0	0	0	0	0	0	0	0	0	0
0	0	0	0	0	0	0	0	0	0
```

Of course we see mostly zeroes because the beginning of the chromosome does not have many epigenomic markers, but we can see the structure.

  * The first line specifies **cell name** and **chromosome name**.
  * The second line specifies the **names of the markers**.
  * The remaining lines specify the presence of those markers in each 200 base segment of the chromosome. 1 means present and 0 means not present.

Once we have such a file, running ChromHMM is a single line operation such as :

```
java -jar ChromHMM.jar LearnModel SAMPLEDATA_HG18 test_output 4 hg18
```

Where