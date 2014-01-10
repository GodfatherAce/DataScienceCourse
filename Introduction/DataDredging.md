Dredging 
Data dredging (data fishing, data snooping) is the inappropriate (sometimes deliberately so) use of data mining to uncover misleading relationships in data. Data-snooping bias is a form of statistical bias that arises from this misuse of statistics. Any relationships found might appear to be valid within the test set but they would have no statistical significance in the wider population.
Data dredging and data-snooping bias can occur when researchers either do not form a hypothesis in advance or narrow the data used to reduce the probability of the sample refuting a specific hypothesis. Although data-snooping bias can occur in any field that uses data mining, it is of particular concern in finance and medical research, both of which make heavy use of data mining techniques.
The process of data mining involves automatically testing huge numbers of hypotheses about a single data set by exhaustively searching for combinations of variables that might show a correlation. Conventional tests of statistical significance are based on the probability that an observation arose by chance, and necessarily accept some risk of mistaken test results, called the significance. When large numbers of tests are performed, it is always expected that some will produce 
false results, hence 5% of randomly chosen hypotheses will turn out to be significant at the 5% level, 1% will turn out to be significant at the 1% significance level, and so on, by chance alone.
If enough hypotheses are tested, it is virtually certain that some will falsely appear to be statistically significant, since every data set with any degree of randomness contains some bogus correlations. Researchers using data mining techniques can be easily misled by these apparently significant results, even though they are mere artifacts of random variation.
Circumventing the traditional scientific approach of conducting an experiment without a hypothesis can lead to premature conclusions. Data mining can be used negatively to seek more information from a data set than it actually contains. Failure to adjust existing statistical models when applying them to new datasets can also result in the occurrences of new patterns between different attributes that would otherwise have not shown up. Overfitting, oversearching, overestimation, and attribute selection errors are all actions that can lead to data dredging.