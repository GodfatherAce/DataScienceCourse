An overview of JAQL - Transcript
Hi, my name is Scott Gray and welcome to very first in the series of educational
videos about Jaql - the scripting language for Big Data. In this video, my goal is
to cover what the language is all about and why it exists in the first place.
First and foremost, Jaql is a programming language for BigInsights, which is
IBM’s distribution and enhancement of the Apache Hadoop project and it’s
surrounding components. So I’ll talk briefly about how Jaql and BigInsights fit
together. Next I’ll talk about what the Jaql language is all about and why it
exists in the first place and finally, how Jaql and MapReduce fit together. And
don’t worry if you don’t know what Hadoop and MapReduce are all about; I’ll
take you through a very brief introduction of them.
When you look at the relationship between Jaql and BigInsights, calling it just a
query language is a bit of an understatement. As you begin to work more with
BigInsights, you’ll discover that Jaql is the language that glues it all together.
Beyond just being a general purpose programming language available within
BigInsights, it provides API’s (or modules) for reaching out to external IBM and
3rd party tools, such as relational databases, indexing services, text analytics,
machine learning etc, and it is also frequently sitting quietly behind the scenes,
being used by existing applications as the mechanism with which to reach into
BigInsights to manipulate Big Data.
So what is Jaql?
Jaql is a language build around a very simple and flexible data representation
model called JSON (pronounced Jay-Sahn). JSON is a standardized data
representation model, that is similar in goal to XML but dramatically easier to
work with—you’ll see when we get to it.
Jaql provides an elegant programming model for developing complex and
reusable queries and transformations against JSON data structures; even very
deeply nested data structures. And, as with SQL, the intent is that you should
focus on specifying the query you need to express to solve your business need,
leaving the language to deal with how the work is physically performed. Under
the hood, Jaql is automatically taking care managing the complexities of the
MapReduce world to optimally perform the work.
Finally, and one of the key points, is that Jaql is an extensible language. It
provides native Jaql functions and modules, that allow you to build up packages
of re-usable logic that can be shared throughout your environment. As I
mentioned on the previous slide, it is using this very functionality on which much
of BigInsights is built.
Many of you may not be that familiar with the Hadoop ecosystem, but I’m sure
that for those of you that are, you are asking yourself “why would I chose Jaql
over other existing languages, such as Hive and Pig?” Why yet another
programming language?
The answer, of course, is that all languages are built to solve specific problems,
and here are some of the problem areas in which Jaql differentiates itself.
In certain problem areas, such as text analytics, data can become deeply nested in
order to represent complex relationships, and this sort of deeply nested data is an
area in which Jaql excels. Syntactically and functionally, Jaql can work with
arbitrarily nested data and can even handle heterogeneous data – that is, data
that can vary in structure and content from record to record. Hive, being SQL
based, is of course restricted to very structured tabular data and, while Pig is
more adept at dealing with semi-structured data, it becomes increasingly more
difficult to work with as you go beyond two levels of nesting.
Jaql also differentiates itself in it’s ability to seamless combine programming
paradigms. Along with the core Jaql syntax that I’ll be covering today, it also
allows you to seamless utilize SQL as your query syntax – sort of like combining
Hive and Pig together into one language.
Perhaps the feature that differentiates Jaql the most is its modularity. Of the
popular Hadoop programming languages, it is the only one currently allows you
to write native functions (that is functions in written in the language itself) that
can parameterize and encapsulate any functionality of the language. You can
then package those functions up into re-usable modules or packages to be shared
across all of your applications.
Finally, although the “QL” in Jaql means Query Language, Jaql is full
programming language. With full flow-of-control features and the ability to
create native functions and modules, you can develop full programs from the
ground up, without requiring the use of another programming language to
orchestrate your logic.
The next aspect of Jaql I’d like to talk about is how Jaql and MapReduce
interact, but for those of you that may not be familiar with what MapReduce is
all about, I wanted to try to give you a very brief overview. I would like to note
that this leaves out a lot of details, but should hopefully be enough to convey the
flavor of what is going on.
The driving principal is MapReduce is a simple one: spread your data out across
a huge cluster of machines and then, rather than bringing the data to your
programs, as you do in a traditional programming, you write your program in a
specific way that allows the program to be moved to the data. Thus, the entire
cluster is brought to bear in both reading the data as well as processing the data.
The Distributed File System (DFS) is at the heart of MapReduce. It is
responsible for spreading data across the cluster, by making the entire cluster
look like one giant file system. When a file is written to the cluster, blocks of the
file are spread out and replicated across the whole cluster (in the diagram we can
see that every block of the file is replicated to three different machines).
Adding more nodes to the cluster instantly adds capacity to the file system and,
as we’ll see on the next slide, automatically increases the available processing
power and parallelism.
On the previous slide I said something to the effect that “if you write your
programs in a special way” the programs can be brought to the data. This special
way is called MapReduce, and involves breaking your program down into two
discrete parts: Map and Reduce.
A mapper is typically a relatively small program with a relatively simple task: it is
responsible for reading a portion of the input data, interpreting, filtering or
transforming the data as necessary and then finally producing a stream of
key, value pairs. What these keys and values are doesn’t really matter for this
discussion, but just keep in mind that these don’t have to be simple values. They
can be as big and complex as you need.
As shown in the diagram, the MapReduce environment will automatically take
care of taking your small “map” program (the blue boxes) and pushing that
program out to every machine that has a block of the file you are trying to
process. This means that the bigger the file, the bigger the cluster, the more
mappers get involved in processing the data! That’s a pretty powerful idea.
This next step is called “The Shuffle” and is orchestrated behind the scenes by
MapReduce.
The idea here is that all of the data that is being emitted from the mappers is first
locally grouped by the key that your program chose, and then for each unique
key, a node is chosen to process all of the values from all of the mappers for that
key.
For example, let say you used U.S. state (e.g. “MA”, “AK”, “NY”, “CA”, etc.) as
the key of your data, then one machine would be chosen to send all of the
California data to, one all of the New York data, and so on. Each machine would
be responsible for processing the data for its selected state. In the picture above,
the data clearly only had two keys (yellow and purple), but keep in mind that
there may be many many records with the same key coming from a given
mapper.
Reducers are the last part of the picture. Again, these are small programs (well,
typically small) that are responsible for sorting and/or aggregating all of the
values with the key that is was assigned to work on. Just like with mappers, the
more unique keys you have the more parallelism.
Once each reducer has completed whatever is assigned to do – maybe add up the
total sales for the state it was assigned – it, in turn, emits key/value pairs that get
written to storage that can, in turn, be used as the input to the next MapReduce
job.
In an extremely over-simplified nutshell, that is MapReduce. So, what does this
have to do with Jaql?
The power of Jaql comes in allowing you to focus strictly on the problem you are
trying to solve, and not how with how it is physically implemented in
MapReduce, or even whether or not MapReduce will be employed to solve it.
Just like with SQL, the queries you write describe the “what” and the underlying
engine figures out the “how” for you.
So, as a quick example: the statement on the left is our first peek at real Jaql
code. It probably doesn’t make much sense right now, but I think you can get the
gist that it reads an input file full of animal names, and then counts the total
number of occurrences of each animal name encountered, writing the results to
an output file. At no point do you see any reference to mappers or reducers, or
anything like that..
If you were to peek under the hood, however, you’d discover that a lot is going
on! Jaql takes your query and decomposes it into pieces – map pieces and reduce
pieces, taking care to try to optimally move logic to best location possible (for
example, to filter out as much data in the mapper before it has to be shipped to
the reducer), and then pushes those pieces out to MapReduce for execution and
stitches the results back together in the end (if necessary)
The piece on the right is our little peek under the hood at how Jaql is
decomposing the query. At this point I wouldn’t expect the logic shown to make
any sense to you, but the specifics aren’t important , the important part is that
Jaql is figuring all of this out for you.
Hopefully I’ve managed to describe what Jaql is all about and why it exists. It
really is a tremendously flexible and robust language for solving very large
problems very easily. And yes, it does have a learning curve… and what language
doesn’t? I promise you: it really isn’t that hard to pick up, and it’s well worth the
effort. And I highly encourage you to continue on with the rest of the Jaql
training materials.
