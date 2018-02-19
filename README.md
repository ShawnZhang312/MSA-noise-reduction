# This is a final project of the Course DD2404, Applied Bioinfomatics at KTH.


MSA-noise-reduction


Multialignments are noisy. Homologous proteins can contain regions that are not inherited and should therefore not be aligned, and other regions may have evolved so fast that the correct multialignment is impossible to infer. In order to get rid of such problematic regions in subsequential analysis, in particular for phylogeny inference, "bad" columns are often removed using tools such as GBlocks or TrimAl.
In this project, you shall implement a simple noise-reduction method and evaluate its impact on phylogeny inference.

Removing noisy columns
In this project, a column is considered noisy if

there are more than 50% indels,
at least 50% of amino acids are unique,
no amino acid appears more than twice.
For example, a column containing "AFFFFFFFFF" has 10% unique amino acids (A) and is therefore not considered noisy, but "ARTLSFFFFF" has 50% unique amino acids (ARTLS) and should be classified as noisy. A column like "AARRTTLLSS" is also noisy, because of the third rule.

You will write a Python program that takes a multialignment as input and removes columns that fulfill at least one of the criteria above. If all columns are removed, your program should exit with an error.

Evaluation
Besides validating your program (making sure it computes what it was supposed to do), you must also evaluate its performance. The basic question is whether it is worthwhile to use multialignment noise reduction?

Test data
For testing, you will use data used by the authors of TrimAl in their evaluation. I have downloaded and reduced the dataset to make it easier to work with. The data is available in /info/appbio12/data/noise_project on the school computers, or downloadable from Canvas. If you download to a Linux or Mac computer, you unpack the data using this command:

prompt> tar -zxf testdata.tar.gz
and you probably want to delete the remanining file testdata.tar.gz.

The testdata contains six subdirectories:

$ ls
asymmetric_0.5  asymmetric_1.0  asymmetric_2.0  
symmetric_0.5  symmetric_1.0  symmetric_2.0
and each such directory contains one tree file, containing a reference tree, and 300 alignments that were created by evolving (using a computer program) sequences along the reference tree and then running muscle to align the resulting sequences. The trees are either symmetric ("easy") or assymetric ("less easy") and the number in the filename denotes the average amount of mutations per site in the sequences. Hence, the *_2.0 directories has alignments with on average two mutations per sequence position, from the root to the leaves and this is of course the hardest case.

What to test
You shall, for each gene alignment, infer a tree using the programs fastprot and fnj (see also the FastPhylo package (Länkar till en externa sida.)Länkar till en externa sida., or use the -h option to get hints) on both the given alignment and the noice-reduced alignment. How often is the reference tree recovered with the two methods?

To get access to the FastPhylo programs on the school computers, you should issue the commands

module use /misc/info/DD2404/appbio16/module/
module add appbio16
when you open a terminal. To get it every time you log in, you can add those lines to your .bashrc file.

BioPython contains a module called Bio.Phylo which unfortunately is somewhat limited. We recommend a Python package called DendroPy, which is installed on the CSC computers. And should be easy to download to your computer as well. If you use it, you can also try a metric called symmetric distance (Länkar till en externa sida.)Länkar till en externa sida. (often referred to as "Robinson-Foulds", but this is claimed to be wrong according to the DendroPy documentation) to quantify the difference between an inferred tree and the reference tree.

Your report
In your report, you are expected to present clear statistics regarding the value of noise reduction (compared to no reduction) for the six reference trees.
