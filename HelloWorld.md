# datasciencecoursera

##First Mark down

How to share data with a statistician
This is a guide for anyone who needs to share data with a statistician or data scientist. The target audiences I have in mind are:

Collaborators who need statisticians or data scientists to analyze data for them
Students or postdocs in various disciplines looking for consulting advice
Junior statistics students whose job it is to collate/clean/wrangle data sets
The goals of this guide are to provide some instruction on the best way to share data to avoid the most common pitfalls and sources of delay in the transition from data collection to data analysis. The Leek group works with a large number of collaborators and the number one source of variation in the speed to results is the status of the data when they arrive at the Leek group. Based on my conversations with other statisticians this is true nearly universally.

My strong feeling is that statisticians should be able to handle the data in whatever state they arrive. It is important to see the raw data, understand the steps in the processing pipeline, and be able to incorporate hidden sources of variability in one's data analysis. On the other hand, for many data types, the processing steps are well documented and standardized. So the work of converting the data from raw form to directly analyzable form can be performed before calling on a statistician. This can dramatically speed the turnaround time, since the statistician doesn't have to work through all the pre-processing steps first.

What you should deliver to the statistician
To facilitate the most efficient and timely analysis this is the information you should pass to a statistician:

The raw data.
A tidy data set
A code book describing each variable and its values in the tidy data set.
An explicit and exact recipe you used to go from 1 -> 2,3
Let's look at each part of the data package you will transfer.

The raw data
It is critical that you include the rawest form of the data that you have access to. This ensures that data provenance can be maintained throughout the workflow. Here are some examples of the raw form of data:

The strange binary file your measurement machine spits out
The unformatted Excel file with 10 worksheets the company you contracted with sent you
The complicated JSON data you got from scraping the Twitter API
The hand-entered numbers you collected looking through a microscope
You know the raw data are in the right format if you:

Ran no software on the data
Did not modify any of the data values
You did not remove any data from the data set
You did not summarize the data in any way
If you made any modifications of the raw data it is not the raw form of the data. Reporting modified data as raw data is a very common way to slow down the analysis process, since the analyst will often have to do a forensic study of your data to figure out why the raw data looks weird. (Also imagine what would happen if new data arrived?)

The tidy data set
The general principles of tidy data are laid out by Hadley Wickham in this paper and this video. While both the paper and the video describe tidy data using R, the principles are more generally applicable:

Each variable you measure should be in one column
Each different observation of that variable should be in a different row
There should be one table for each "kind" of variable
If you have multiple tables, they should include a column in the table that allows them to be joined or merged
While these are the hard and fast rules, there are a number of other things that will make your data set much easier to handle. First is to include a row at the top of each data table/spreadsheet that contains full row names. So if you measured age at diagnosis for patients, you would head that column with the name AgeAtDiagnosis instead of something like ADx or another abbreviation that may be hard for another person to understand.

Here is an example of how this would work from genomics. Suppose that for 20 people you have collected gene expression measurements with RNA-sequencing. You have also collected demographic and clinical information about the patients including their age, treatment, and diagnosis. You would have one table/spreadsheet that contains the clinical/demographic information. It would have four columns (patient id, age, treatment, diagnosis) and 21 rows (a row with variable names, then one row for every patient). You would also have one spreadsheet for the summarized genomic data. Usually this type of data is summarized at the level of the number of counts per exon. Suppose you have 100,000 exons, then you would have a table/spreadsheet that had 21 rows (a row for gene names, and one row for each patient) and 100,001 columns (one row for patient ids and one row for each data type).

If you are sharing your data with the collaborator in Excel, the tidy data should be in one Excel file per table. They should not have multiple worksheets, no macros should be applied to the data, and no columns/cells should be highlighted. Alternatively share the data in a CSV or TAB-delimited text file. (Beware however that reading CSV files into Excel can sometimes lead to non-reproducible handling of date and time variables.)

The code book
For almost any data set, the measurements you calculate will need to be described in more detail than you can or should sneak into the spreadsheet. The code book contains this information. At minimum it should contain:

Information about the variables (including units!) in the data set not contained in the tidy data
Information about the summary choices you made
Information about the experimental study design you us