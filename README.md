# Star-Solo-workflow-for-the-10x-multiomics-analysis (Under Construction)
Using Star Solo to analyze 10X multiomic data

A following descibes a workflow for the 10xMultiomic data by using Star Solo.  One of the advanrage of using Star Solo (in my case at least) unlike CellRanger is that Solo can be complined in the arm-64 Mac and runs faster than CellRanger by PCs running Intel CPU (unofficial observation). Also, Solo has the edges over CellRanger on the custermization of aliment parameters that one can play with.  

A 10XMultiomics platform has two components, GEX and ATAC, which are combined to an one single GEX and ATAC count matrix with common barcodes, although GEX and ATAC sequecing are done in the different reactions.  

You can check my crude attempt at STAR discussion, https://github.com/alexdobin/STAR/discussions/1995
Steps to analyze 10xmultiome data by STARsolo will be described detail in the accompanying files.  As mentioned, 10Xmultiome has two components; 1) Gene Expression (GEX) and 2) ATAC analyses and data generated from a multiome kit are processed by ```CellRanger ARC``` which analyzes both GEX and ATAC.  An introduction of a 10x multiome assay is available  at https://www.10xgenomics.com/products/single-cell-multiome-atac-plus-gene-expression ,and a deescription of its analysis pipeline, ```CellRanger ARC``` is fountd at https://www.10xgenomics.com/support/software/cell-ranger-arc/latest/getting-started/what-is-cell-ranger-arc.  As ```CellRanger ARC```,  ```STARSolo``` can analyzed both GEX and ATAC data from the 10X multiome kit, and generate the results that are comparable to those generated by ```CellRanger ARC```.  

### Motivation ###
Why using ```STARsolo``` if ```CellRanger ARC``` is available ?  Interestingly, a core pipline of ```CellRanger ARC``` is STAR.  ```CellRanger``` is a sort of like wrapper for STAR with minor modifications for performaning read alignment.  There are a few reasons for favoing ```STARsolo``` 
1. It has been frequently updated owing to a leaderhip provided by a developer and maintainer of ``STARsolo```, Alex Dobin (this guys answers virtually all the questions posted on its github page,   which literally are ***thousands a week!!***)  as well as hundreds of contributors worldwide.   This ensures that new features and bug fixes are very quickly posted in the github page.
2. It can be compiled in any avaiable ***arm*** based device including new Mac with ***arm64 vased M series*** cpu.  In contrast, ```CellRanger``` is only available to ***X86_64*** based devices.
3. I have to say this but the ***arm64*** is the future (not comparing to GPU). In fact, based on my unscientific comparison, ```STARSolo``` running in the arm based machine (e.g. my M1 MacStudio) runs much faster and require less memory for some reasons than either ```STARsolo``` or ```CellRanger``` running in PCs (e.g. Dell workstation with wapping 50 cores of X86_64).  This is true when using arm Linux clusters inclduing AWS and added benefit is that the usage of the arm based AWS linux clusters are cheaper than the one with X86_64 based clusters.    

There are several other reasons related to STARsolo's unmatched capacity for customization and flexibility to analyze data from multiple sequencing platforms.  A pipeline described in this repository is one example of what ```STARSolo``` can achieve without a need for ```CellRagner```.  
