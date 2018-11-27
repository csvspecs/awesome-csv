# TAB vs CSV



## Comparing TAB and CSV formats

The differences between TAB and CSV formats can be confusing. 
The obvious distinction is the default field separator: TAB uses tab (`→`), 
CSV uses comma (`,`). Both use newline as the record separator.


By itself, having different default field separators is not especially significant. 
Far more important is the approach to separators occurring in the data. 
CSV uses an escape syntax to represent comma and newlines in the data. 
TAB takes a different approach, disallowing tabs and newlines in the data.

The escape syntax enables CSV to fully represent common written text. 
This is a good fit for human edited documents, notably spreadsheets. 
This generality has a cost: reading it requires programs to parse the escape syntax. 
While not overly difficult, it is still easy to do incorrectly, especially when writing one-off programs. 
It is good practice to use a CSV parser when processing CSV files. 
Traditional Unix tools like `cut` and `awk` do not process CSV escapes, alternate tools are needed.

By contrast, parsing TAB data is simple. 
Records can be read using the typical `readline` routines. 
The fields in each record can be found using a `split` or `splitter` routine available in most programming languages. 
No special parser is needed. This is much more reliable. It is also faster, no CPU time is used parsing the escape syntax.

This makes TAB format well suited for the large tabular datasets common in data mining and machine learning environments. 
These datasets rarely need tab and newline characters in the fields.

The most common CSV escape format uses quotes (`"..."`) to enclose fields with / containing (comma) separators. 
Quotes must also be escaped, this is done by using a pair of quotes (`""`) to represent a "literal" quote (`"`) inside quotes. 
Consider the data in this table:

| Field 1 | Field 2              | Field 3 |
| ------- | -------------------- | ------- |
| abc     | hello, world!        | def     |
| ghi     | Say "hello, world!"  | jkl     |

In field 2, the first value contains a comma, the second value contain both quotes and a comma. 
Here is the CSV representation, using escapes to represent commas and quotes in the data.

```
Field 1,Field 2,Field 3
abc,"hello, world!",def
ghi,"Say ""hello, world!""",jkl
```

In the above example, only fields with / containing (comma) separators are quoted. 
It is also common to quote all fields whether or not they contain (comma) separators. 
The following CSV file is equivalent:

```
"Field 1","Field 2","Field 3"
"abc","hello, world!","def"
"ghi","Say ""hello, world!""","jkl"
```

Here's the same data in TAB. It is much simpler as no escapes are involved:

```
Field 1→Field 2→Field 3
abc→hello, world→def
ghi→Say "hello, world!"→jkl
```

The similarity between TAB and CSV can lead to confusion about which tools are appropriate. 
Furthering this confusion, it is somewhat common to have datafiles using comma as the field separator, 
but without comma, quote, or newlines in the data. 
No CSV escapes are needed in these files, with the implication that traditional Unix tools 
like `cut` and `awk` can be used to process these files. 
Such files are sometimes referred to as "simple CSV". 
They are equivalent to TAB files with comma as a field separator. 
Traditional Unix tools can process these files correctly by specifying the field separator. 
However, "simple CSV" is a very ad hoc and ill defined notion. 
A simple precaution when working with these files is to run a CSV-to-TAB converter like `csv2tab` 
prior to other processing steps.


(Source: Adapted from [Comparing TAB and CSV formats](https://github.com/eBay/tsv-utils/blob/master/docs/comparing-tsv-and-csv.md))


## The philosophy of TAB (command line utils)


There are many data processing and analysis situations where data consists of tables.
A "table" is a list of flat records each with the same set of named attributes, where it's easy to manipulate a particular attribute across all records -- a "column".  The main data structures in SQL, R, and Excel are tables.

TAB-with-headers sits in a sweet spot on the spectrum of data format complexity.

- A more complex alternative is to encode in arbitrarily nested structures (XML, JSON).  These have greater representational capacity, but are less convenient for data analysis.  Since they can have high structural complexity, it's often error-prone to use them -- ad-hoc querying is generally difficult.  Furthermore, it's wasteful of space to repeat key names over and over if all records are known to have the same set of keys.  Finally, when doing data analysis, especially statistical analysis, you want to turn columns into vectors, which presupposes a flatter, more table-like structure.
- A simpler alternative is a table with positional, un-named columns.  The main weakness is that for more than several columns, it's hard to remember which column is which.  Named columns improve maintainability.

But: SQL databases and Excel spreadsheets are often inconvenient data management environments compared to the filesystem on the unix commandline.  Unfortunately, the most common file format for tables is CSV, which is complex and has several incompatible versions.  It plays only moderately nicely with the unix commandline, which is the best ad-hoc processing tool for filesystem data.  Often the only correct way to handle CSV is to use a parsing library, but it's inconvenient to fire up a python/perl/ruby session just to do simple sanity checks and casually inspect data.

To balance these needs, so far I've found that TAB-with-headers is the most convenient canonical format for table data in the filesystem/commandline environment, or at least the lingua franca in shell pipelines.  These utilities are just a little bit of glue to make TAB play nicely with CSV, Excel, MySQL, and Unix tools.  Interfaces in and out of other table-centric environments could easily be added.

On the philosophy of having NO escaping or special data value conventions: If you want those things in your data, make up your own convention (like backslash escaping, URL escaping, or whatever) and have your application be aware of it.  Our philosophy is, a data processing utility should ignore that stuff in order to have safe and predictable behavior.  I've seen too many bugs because some intermediate program imposed a special meaning on "NA" or "\N" or "NULL", etc., when really a program further downstream should have had sole responsibility for this interpretation.


(Source: Adapted from [The philosophy of tab (command line utils) - Brendan O'Connor's discussion of the rationale for using TAB format in his open source toolkit](https://github.com/brendano/tsvutils#the-philosophy-of-tsvutils))

 
