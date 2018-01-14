Part 2: Pig Relational Operators
=========================================
Learning objectives

- List the relational operators used in Pig
- Explain how to flatten your data
- Describe dereference operators

Pig relational operators
===============================

1. ``Filter`` and ``Order By``
2. ``Group`` and ``COGROUP``

#### ``FILTER`` and ``ORDER BY``

The ``FILTER`` operator selects tuples from a relation base upon a specified criteria.
For example if we had a relation called, data, which has a field called pubyear,
then ``b = filter data by pubyear == 2003;`` would return those tuples where the
value of pubyear is equal to 2003.

The ``ORDER BY`` operator sorts a relation on one or more fields. If the relation,
data, has a field called author, then ``b = order data by author ASC``; would sort the
tuples in relation, data, in ascending sequence by author. 

To sort in descending sequence, you would specify ``DESC``. Also multiple comma separated fields may be
specified, each specifying their own sort sequence.

####GROUP
* The group operator groups together tuples that have the same group key. 
* The group key can be based upon a single field in the tuple or multiple fields. 
* If the group key consists of multiple fields, then they are enclosed in parentheses. 
* The group operator emits a relation that contains one tuple per group. This tuple consists of two fields. The first field always has a name called, group. (Do not get this confused with the name of the operator.) 
* That field contains the value of the group key. The second field takes the name of the original relation that was
grouped.

####GROUP example
Here we have a relation called, data, that has four tuples. The schema for the relation indicates that there are three fields with names of f1, f2, and f3. Dumping data gives (1,2,3) (4,5,6) (7,8,9) (4,3,2).

If we create a new relation, grp, which is a grouping of data using the f1 field, we
would get (1,{1,2,3)}) (4,{(4,5,6),(4,3,2)}) (7,{(7,8,9)}).

####COGROUP
The GROUP and COGROUP operators are actually the same operator but, by convention, the COGROUP operator is used when grouping multiple relations at the same time. 127 relations can be grouped at the same time.

####COGROUP example
Assume a relation, emp, with three fields, id, dept, income. And a second relation,
dept, with two fields, did and name.
I am only going to refer to a subset of the data in the example on the visual.
emp has this data: (1,1,12000) (2,1,13000) (3,2,15000)
dept has (1, development) (2,marketing)
Executing x = cogroup emp by dept and dept by did; would produce
(1,{(1,1,12000),(2,1,13000),(1,development)}) and (2,{(3,2,15000),(2,marketing)})

----------------------------------------------------------
#### FOREACH
The `FOREACH` operator allows you to create a new relation through projection.
This new relation may have fewer fields or more fields than the original relation. 
There are two formats for this operator. One that works with a block and one that
works with a nested block.
#### FOREACH with an outer bag
Assume that we have a relation x that has three fields x1, x2, and x3. Also a dump
of x shows (1,2,3) (4,5,6) (7,8,9) (4,3,2). Executing
out = foreach x generate x1, x2, x2 + x3 as f1:int; results in a new relation, out,
that will have three fields x1, x2, and f1. Dumping out will show
(1,2,5) (4,5,10) (7,8,16) (4,3,5)

Understand that the FOREACH operator is just iterating over each field in the tuple. The current iterated field does not have to participate in the output. Assuming the same three fields for relation x, this statement is valid.
<pre><code>
Out = foreach x generate x2, x1, x2 + x1 as f1:int;
</code></pre>
X3 was never referenced and that is valid.

#### FOREACH with a grouped relation
Assume a relation, data, with three fields f1, f2, and f3. Dumping data shows
(1,2,3) (4,5,6) (7,8,9) (4,3,2)

Next we execute y = group data by f1; If we then dump y, we get
(1, {(1,2,3)}) (4,{(4,5,6),(4,3,2)}) (7,{(7,8,9)})

Remember that the schema for relation y contains two fields. The name of the
first field is group. The second field is the name of the relation that was grouped.
In this case it is data. Now you want to use the FOREACH operator to iterate
across the y relation. But how do you access the fields of the second field in
relation y? You use a dereference operator. If you executed this z = foreach y
generate group, data.f2, data.f3; you would get
(1, {(2)},{(3)}) (4,{(5),(3},{(6),(2)}) (7,{(8)},{(9)}) 
####  FOREACH with a nested block
The FOREACH operator can work with a nested block however you are limited to
these operators within the nested block, DISTINCT, FILTER, LIMIT, and ORDER BY.
#### FOREACH with a nested block – example
Assume that you have the same data for relation data that you had in the
previous example and that you have the same y relation created with y = group
data by f1; The resulting data would still be
(1, {(1,2,3)}) (4,{(4,5,6),(4,3,2)}) (7,{(7,8,9)})
Next you will create a new relation, z, by executing the following:
z = foreach y {fdata = filter data by f1 < 5; pdata = fdata.f1; generate group,
COUNT(pdata);};
The statements between the { and } is the nested block. In this nested block you
are able to further manipulate your data.
The result would be (1,1) (4,2) (7,0)
The tuple where group is equal to 7 is the only group where the value of f1 is not
less than 5. The tuple with a group equal to 1 only has one tuple where the value
of fi1 in that tuple is less than 5. The tuple with a group equal to 4 has two tuples that
meets the criterial.
#### Flatten
The FLATTEN operator, when working with tuples, substitutes the field of a tuple
for that tuple. If you have (1, (2,3)), then flattening it would result in (1,2,3).
#### Dereference
Sometimes it is necessary to reference a field in a tuple or bag that is outside the
scope of the current operator. This is especially true with the FOREACH operator.
<pre><code> 
data = load 'myfile' as (f1:int, f2:int, f3:int);
y = group data by f1;
z = foreach y generate group, data.f2, data.f3;
</code></pre>
Fields f2 and f3 are not defined in relation y. In order to reference them, they
have to be qualified with either a tuple or bag name where they were defined. It
is also possible to dereference by position as well, for instance, data.$1 or
data.$2.

#### DISTINCT and UNION
DISTINCT removes duplicate tuples found in a relation. UNION merges the
contents of two or more relations.

#### SPLIT and CROSS
SPLIT partitions a relation into two or more relations based upon some
conditional processing. For example split x into y if f1 < 3; z if f1 > 4;
CROSS computes the cross product of two or more relations.
#### JOIN – inner
This performs a join on two or more relations using one or more common fields.
The join will be an equijoin. So c = join a by a1, b by b1; will join the tuples in
relations a and b when the a1 field in relation a is equal to the b1 field in relation
b.
JOIN – outer
With this version of the join, keywords left, right and full are specified. It is only
valid for a two-way join.

#### JOIN ‘using’ clause
One of the join parameters is the using clause. This is designed to give you some
control on how the joins are to be processed. Replicated joins work well if one or
more of the relations are able to fit in memory. This allows the Hadoop work to
be done on the map side. 
Skewed joins should be used where the data is skewed. It computes a histogram
of the key space.
Merged joins where both inputs to the join are already sorted on the join key.
This allows for the data to be joined in the map phase of the MapReduce job.

#### Topic summary
Having completed this lesson, you should be able to:
- List the relational operators used in Pig
- Use the FILTER operator to remove unneeded data
- Use the ORDER BY operator to sort your data
- Group tuples that have the same group key
- Use the FOREACH operator to generate new tuples
- Explain how to flatten your data
- Describe dereferencing operators
