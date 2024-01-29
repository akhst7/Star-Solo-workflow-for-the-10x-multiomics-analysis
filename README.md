# Star-Solo-workflow-for-the-10x-multiomics-analysis (Under Construction)
Using Star Solo to analyze 10X multiomic data

A following descrives a workflow for the 10xMultiomic data by using Star Solo.  One of the advanrage of using Star Solo (in my case at least) unlike CellRanger is that Solo can be complined in the arm-64 Mac and runs faster than CellRanger by PCs running Intel CPU (unofficial observation). Also, Solo has the edges over CellRanger on the custermization of aliment parameters that one can play with.  

A 10XMultiomics platform has two components, GEX and ATAC, which are combined to an one single GEX and ATAC count matrix with common barcodes, although GEX and ATAC sequecing are done in the different reactions.  
