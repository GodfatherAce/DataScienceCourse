Lesson 1: An Introduction to Apache Pig, Pig Basics
==================================

Learning objectives

- List the ways to invoke Pig
- Describe the data structures used in Pig
- Explain how to use the `LOAD` operator to read data
- Describe how to substitute parameters in a Pig script
- Explain how to use the `OUTPUT` operator to write data



### Overview
Pig or Pig Latin as the language is called, is a high-level language designed to
remove the complexities of coding MapReduce applications. Pig converts its operators into MapReduce code. So instead of needing Java programming skills and an understanding of the MapReduce coding infrastructure, people with little
programming skills, can simply invoke SORT or FILTER operators without having to
code a MapReduce application to accomplish those tasks.

One of the strong features of Pig is that the developer / analyst does not have to depend solely on the Pig-supplied operators. It is possible to extend the language by coding one’s own user-defined functions.

#### Executing Pig
Pig can run in interactive mode or in script mode. Both of these ways have two
options. 
* Local mode gives you access to data in your local file system. It runs in a single Java virtual machine. This mode is normally used for testing against a limited amount of data. 

* The second option, MapReduce mode, runs on a Hadoop cluster and converts the
Pig statements into MapReduce code.

----------------------------------------------------------------------------------------------
To invoke Pig in interactive mode, just execute pig and you are then placed into
the Grunt shell. By default you will be running in MapReduce mode. To execute
Pig interactively in local mode, execute `pig –x local`

To invoke a Pig script, just include the name of the script when you invoke pig. For
example to run a pig script called myscript.pig in local mode, execute ``pig –x local myscript.pig``. 
To run the same script in MapReduce mode, execute ``pig myscript.pig``.
It is also possible to invoke pig using a Java command as well.

#### First look at Pig data

As you might expect, the Pig language has a number of scalar data types used to define individual fields. Some examples are int for integers, chararray for string data, double and float for numbers with decimal points.

Fields are grouped together into tuples. You might think of a tuple as a row in a relational data table or a record in a file. Pig has greater flexibility over a relational table in that all tuples do not have to contain the same number of
fields.

Tuples are grouped into a bag. Now this is where it can get a little complex. I just said that a bag is a group of tuples, but a “field” in a tuple can actually be a bag that contains other tuples. In this case, the bag is an inner bag. The bag, that
contains the tuples that correlate to a row in a relational table, is known as an outer bag. It is also known as a relation.
Map data is also supported in Pig. A map is a set of key / value pairs. Accessing a map with a specify key will return the value associated with that key. 

####Pig Latin statement basics
Most Pig operators take a relation (an outer bag) as input and in turn emits a
relation. The exceptions are the LOAD operator which only emits a relation (after
reading data from some source). The STORE operator takes a relation as input but
writes the data in the relation to a file and the DUMP operator, which like the
STORE operator, takes a relation as input but writes the data values to the
console.

All Pig statements, both in a script and when running in a Grunt shell, are
terminated by a semicolon. In a script, it is possible to include comments. All
statements between a /* and an */ are commented. Double dashes – will
comment the rest of that line.
####Input
The LOAD operator is used to read data from a source and place that data into a
relation. Since there are a variety of ways that data can be stored, there are going
to be a variety of functions that can be used with this operator. Pig supplies four
such load functions and you can supply your own as well.
The default load function is PigStorage. This reads data that is in a delimited
format with the default delimiter being the tab character. If some other
delimiting character is to be used, then that character is supplied in single quotes.
The TextLoader reads in a line of text and this line of text is placed into a single
tuple. The BinStorage function is used to read data in a machine readable format.
This is used by Pig internally to store temporary data. There is also a JsonLoader.
This loads data that is in a standard JSON format.

Let’s look at an example. `A = load ‘/datadir/datafile’ using PigStorage(‘\t’); `will
read data from a file, datafile located in the /datadir. Since the ***PigStorage***
function is being used, the data is expected to be in a delimited format with the
tab character as being the delimiter. The results are placed into a relation call A.

####LOAD operator continued 
As I said, you can code your own load function if your data is in some proprietary
format not supported by the supplied load functions. There is a LOAD option that
we should discuss. This option provides a schema for you input data. To specify a schema you code as (your schema info) after the load function. So continuing with
a similar example, ``A = load ‘/datadir/datafile’ using PigStorage(‘,’) as (f1:int,
f2:chararray, f3:float);`` would read a comma delimited file and interpret the first
field as an integer and associate it with a name of f1. The second field would be a
chararray and the third a float.

If you do not supply a schema for the ***PigStorage*** function, then the fields are not
named and all fields default to bytearray for their data type. The JsonLoader
function requires a schema.

####Accessing data
You have seen examples where the LOAD operator was reading data from a
specific file. But it can go beyond that. If only a directory is specified, then the
LOAD operator will read all files within that directory.
Case sensitivity
The names of relations and fields are case sensitive. Function names are case
sensitive as well. But keywords and operator names are not case sensitive.

---------------------------------------------------------------------------

####Field references
* Fields are assigned names through the use of a schema and fields may be
referenced by their names. 
* But a field can also be referenced by position as well.
* This is accomplished by specifying a $ and a number. Field numbers start with
zero. So with a schema of (name: chararray, age:int, salary:float), the age field
could be reference by position as $1.
* If a schema is not specified when data is loaded, then the fields can only be
referenced by position.

####Pig data types 

Listed are the Pig data types and a description of each. I am not going to read
each type to you but you can use this page as a reference. The only two data
types that have not yet been mentioned is long, which is a 64 bit integer and
bytearray which is a blob type.

####Operators
Pig Latin allows for the normal arithmetic operators found in programming
languages - addition, subtraction, multiplication, and division. 

Also included in modulo. Binary condition is essentially a shorthand notation for an if then else.
<pre><code>
X == 5 ? 1 : 2; 
</code></pre>
If X equals 5, then 1 is returned, otherwise, 2 is returned.

Conditional processing is handled by Boolean operators, and, or, not. Field values
can be compared using the comparison operators. Equal to is written as == and
not equal is written as !=. is null will check if a field is NULL.

-------------------------------------------------------------------
####Parameter substitution
Parameters can be passed to a Pig script. This allows a single generic script to be
used for a specific situation. Values that are not common across all executions of the script can be changed for each invocation of the script. Within the script, parameters are referenced by preceding the parameter name
with a $.

There are two ways to pass parameter values to a script. Parameters can be set to
values on the command line when the script is invoked or the parameters, along
with their values, can be defined in a parameter file. 

Then that parameter file is referenced when the script is invoked.
Assume that within your Pig script, myscript.pig, you have the statement a = load
‘$dir/myfile.txt’; Your script is assuming that a parameter by the name of dir is
going to be passed. Now let’s look at the two ways that the value for dir can be
specified. 
``pig -param dir=’/labfiles’ myscript.pig``` passes dir to your script with a value of
/labfiles. So the load statement in your script expands to a = load
‘/labfiles/myfile.txt’;

A second technique is to have a file that has the parameter values. Assume that
the name of this file is myparams.txt. Within this file, you would code a statement
dir = ‘/labfiles’. Then when you invoke your script, you would execute pig -
param_file myparams.txt myscript.pig.

####Output
The STORE operator saves results to a file. It uses built-in functions, similar to the
LOAD operator, to determine how the output data is to be formatted. 
* PigStorage is once again the default and the tab character is the default delimiter.
* BinStorage is used by Pig for temporary files. 
* PigDump stores the data as tuples in a humanreadable UTF-8 format. 
* JsonStorage writes data in a JSON format. 

As with the LOAD operator, you can code and specify your own function.
The format of the STORE operator is STORE alias into ``‘<directory’ [using
function()];`` The specified directory will be created. 

If it already exits, then the operation will fail. Files written into the directory will be of the format partnnnnn.

As stated before, the DUMP operator writes the results to the console. Basically,
it is designed for debugging and testing.

####Topic summary

Having completed this lesson you should be able to:
* List the ways to invoke Pig
* Describe the data structures used in Pig
* Use the LOAD operator to read data into Pig
* Pass input parameters into a Pig script 
* Use the OUTPUT operator to write data from Pig
