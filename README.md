HiCdat: Hi-C data analysis tool
=========================

[About HiCdat](http://dx.doi.org/10.1186/s12859-015-0678-x)

User guide including a tutorial for data pre-processing:

[user guide](https://github.com/MWSchmid/HiCdat/blob/master/other/userGuide.pdf?raw=true)

Binaries (note that the MacOSX binary was built on 10.10.1 and in addition tested on 10.8.5):

[windows 7 64bit binary](https://github.com/MWSchmid/HiCdat/blob/master/other/windows_64bit.zip?raw=true)

[MacOSX 64bit binary](https://github.com/MWSchmid/HiCdat/blob/master/other/mac_64bit.zip?raw=true)

[linux 64bit binary](https://github.com/MWSchmid/HiCdat/blob/master/other/linux_64bit.zip?raw=true), IMPORTANT: install the Qt4 libraries: sudo apt-get install qt4-default

Data for pre-processing tutorial:

[pre-processing data (full data set, ~20 Gb)](http://www.botinst.uzh.ch/static/HiCat/At_pre-process_tutorial.zip)

[pre-processing data (reduced data set, ~5 Gb)](http://www.botinst.uzh.ch/static/HiCat/At_pre-process_tutorial_small.zip)

**IMPORTANT:** The function for the correlated HiC interaction matrix is slightly different to the one we used in the original article on the [_KNOT_ in _Arabidopsis_](http://www.cell.com/molecular-cell/abstract/S1097-2765(14)00602-9). The color gradient is less bright and it is reverted: **yellow/orange means low/negative correlation and red means high/positive correlation.** My thanks to Dr. Syed Islamuddin Shah for reporting this difference. You can check the "new" color gradient with:

```R
colorSet <- colorRampPalette(c("#ffeda0", "#feb24c", "#f03b20"), interpolate = "spline")(64)
plot(c(1:64),rep(1,64),col = colorSet, type = 'h', lwd = 10)
```

For the tutorial in R, download the package and the archives below, unpack the two archives, and open "HiCdat-tutorial-arabidopsis.R" in a text editor and follow the instructions. The HiCdat package HiCdatR can be installed with install.packages("/path/to/HiCdatR_0.99.0.tar.gz", repos=NULL, type = "source"). Note that HiCdatR requires the R libraries "gplots", "randomizeBE", "MASS", and "HiCseg". You can install them with: 

```R
install.packages(c("gplots", "randomizeBE", "MASS"))
source("http://bioconductor.org/biocLite.R")
biocLite("HiCseg")

install.packages("/path/to/HiCdatR_0.99.0.tar.gz", repos=NULL, type = "source")
```

[R-package](https://github.com/MWSchmid/HiCdat/blob/master/other/HiCdatR_0.99.0.tar.gz?raw=true)

[R-Scripts (including the R-tutorial script)](https://github.com/MWSchmid/HiCdat/blob/master/other/Rscripts.zip?raw=true)

[files required for the tutorial in R](https://github.com/MWSchmid/HiCdat/blob/master/other/At_tutorial_files.zip?raw=true)

If you encounter problems, please contact me.

NOTE: if you encounter problems installing one of the R packages (other than HiCdatR), try to install it via [Bioconductor](http://www.bioconductor.org/):

```R
source("http://bioconductor.org/biocLite.R")
biocLite("insertNameOfPackageHere")
```

NOTE: On linux, GLIBC needs to be at least version 2.14. Biolinux6 has a lower version.

NOTE: [Ay and Noble (2015)](http://dx.doi.org/10.1186/s13059-015-0745-7) list Subread as aligner for HiCdat in their table. While we do use Subread in the Tutorial, we also mention that any other aligner should in principle work with HiCdat. The only requirement is that the aligned reads are in BAM format. For Bowtie2, this can for example done directly with:

```bash
bowtie2 --no-unal -x myIndex -U sample.fastq.gz | samtools view -q 10 -h -b - > sample_minQ_10.bam
# -q 10 means that only alignments with a minimal quality of 10 are kept
# this should be sufficient to remove all "non-unique" alignments
```
