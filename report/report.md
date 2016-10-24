<h1>Kiva in Kenya</h1>

<h2>An Analysis of Micro-loan Activity in an East African Country</h2>

<p>Non-technical summary
This analysis is directed at persons with interest in the <a href="http://kiva.org/">Kiva microloan development program</a>. Kiva is a development and philanthropy program that provides loans to people who would likely have no other access to credit.  According to its website, Kiva has headquarters in San Francisco and is active in over 80 countries. Kiva works with diverse field partners, including banks, schools and NGOs, to identify and vet potential borrowers.  Kiva donors provide funding either as individuals or groups.  Donors can choose which borrowers they want to support and the funds are then generally provided to partner organizations who disburse the funds, and manage and receive repayments.  In some cases, local trusties may endorse and back loans made to individuals in the local community. 
The analysis is based on publically available data that can be downloaded free of charge and without special permission from the Kiva website. The analysis uses data from Kenya which, being second in the number of Kiva loans globally, appeared in preliminary analysis to have an amount of data that would be manageable on a Macbook Pro computer with 8GB ram. The analysis provides graphical description of the distribution of Kiva activity in Kenya, and may serve to identify economic sectors that receive relatively little support from the program, for whatever reason. Further, this report describes attempts to model the rate of defaults and to explore gender-specfic information in the descriptions of borrower's situations, as provided to potential donors. 
The results indicate that historical default rates have varied among economic sectors, but are generally under 10% and in most cases under 5%. Prediction of default on a loan-by-loan basis were generally unsuccessful, perhaps owing to the low prevalence of defaulted loans in the data. This was likely compounded by the fact that nearly all descriptive and geographic information had been purged from records representing defaulted loans. The analysis indicates that there are strong gender differences in the number of awarded loans, depending upon economic sector. While the analysis does not attempt to identify the source of these differences (no data was available on the applicant pool), it does attempt to determine to what degree the text descriptions of borrower situation and activity are consistent between declared gender of borrower, using natural language processing. These attempts to identify the gender of the borrower were only successful when gender-specific nouns, pronouns and proper nouns were included in the analysis.  Once they were removed, the remaining information on the borrowers activities and situation were not sufficient to identify the gender of the borrower. Thus, the text descriptions provide little information, beyond gender-specific words, to use in determining whether the declared use of the loan might be inconsistent with broad patterns of lending indicated in the data.</p>

<p>Data Origin
The loan data were downloaded as a zipped archive of 2144 files in json format on 24 May 2016 (http://build.kiva.org/docs/data/snapshots).  Additional files with data on lenders and loan-lender indices were also available and inspected, but due to limited content were judged to hold data not central to the analysis.</p>

<p>Data Wrangling
The loan data were initially processed sequentially by file (https://github.com/pbpearman/capstone/blob/master/extract<em>Kenya</em>loans.ipynb). The following Python libraries were used for wrangling and creating a storable object: pandas, numpy os, json and cPickle. After loading each file (json.load()), as a three columns required normalization, after which they were merged to a single pandas dataframe on a shared column. </p>

<pre><code> Problems
</code></pre>

<p>Inspection of the imported and normalized json indicated that further flattening (normalization) could be attempted.  However, these features (e.g., 'terms', 'location', 'journal<em>totals') were of variable lengths.  When normalized using json</em>normalize(), flattened cells were inserted into the pandas dataframe as new row segments, corresponding to some number of new features.  However, the number of new features  varied in length from row to row.  Despite this, the apply function that implemented json<em>normalize() did not throw an error.  The result was corruption of the pandas dataframe: apparently the rows varied in length and consistent reference with df.iloc[] was impossible.  Due to time constraints, I chose not to pursue flattening these features.  However, I did extract information to create features quantifying the gender of the borrower or group of borrowers (https://github.com/pbpearman/capstone/blob/master/kenya</em>wo_problems.ipynb).
Additionally, I initially had hoped to include a geographic component into the analysis by using geographic coordinates and-or city and town names.  The great majority of loan records were represented by coordinates that simply indicated a point at 1 arc degree of resolution, sufficient to pinpoint the country of Kenya.  Nominal references to town sometimes indicated entire small cities, while the indicated economic sector suggested that the location must be suburban or rural.  These inconsistencies in data quality led me to abandon the idea of including an explicit geographical component in the analysis.
Finally, near the end of the analysis, I had a spontaneous impulse to examine the data for duplicate records.  This revealed over 6000 records in which the loan id, borrower's name, funded date, repayment status and discriptive text were duplicated in additional records.  While other aspects of the loan may have changed (re-classification to another economic sector), I chose to keep only the first occurrence of a record as identified by these variables jointly.</p>

<pre><code> Lessons learned
</code></pre>

<p>While the general patterns in the data were not affected by duplicate records, one should examine an unknown dataset for duplicate records at or near the beginning of an analysis.  Perhaps more importantly, the normalization of serial data, as in json-format files, can not simply be assumed successful when no error messages arise. Additional testing may reveal irregularities that have not be immediately apparent or, as happened here, anomalous and confusing results may require de-bugging and eventually lead to the problem. For example, I might have been able to detect problems had I examined the number of cells with NaN values, or exported the pandas dataframe to cvs, or run a function to actually test the number of cells in each row.</p>

<p>Data Patterns</p>

<p>The number of loans made in Kenya is again increasing after two years of relative stability.
<img src="./images/test.png" alt="loan increase" title=""></p>

<pre><code> Emergent questions
</code></pre>

<p>Feature Engineering</p>

<p>Modeling</p>

<pre><code>NLP

Machine Learning
</code></pre>

<p>Conclusions</p>
