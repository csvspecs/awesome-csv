# Notes


Q: Run SQL Directly on CSV Files?
@ Hacker News <https://news.ycombinator.com/item?id=18453133>

TextQL: Execute SQL Against CSV or TSV 
@ Hacker News <https://news.ycombinator.com/item?id=16781294>




## CSV Format

<https://github.com/eBay/tsv-utils/blob/master/docs/comparing-tsv-and-csv.md> - 
Comparing TSV and CSV formats


<https://github.com/brendano/tsvutils#the-philosophy-of-tsvutils> - 
The philosophy of tsvutils.
Brendan O'Connor's discussion of the rationale for using TSV format in his open source toolkit.



## CSV Tools

<https://github.com/BurntSushi/xsv> - 
xsv is a command line program for indexing, slicing, analyzing, splitting and joining CSV files. 
Commands should be simple, fast and composable.


<https://github.com/eBay/tsv-utils> - 
eBay's TSV Utilities: 
Command line tools for large, tabular data files. 
Filtering, statistics, sampling, joins and more.

<https://github.com/eBay/tsv-utils/blob/master/docs/OtherToolkits.md> - 
Other open-source tools

<https://github.com/dbohdan/structured-text-tools> - 
Structured text tools.
The following is a list of text-based file formats and command line tools for manipulating each.


<https://github.com/shenwei356/csvtk> -
A cross-platform, efficient and practical CSV/TSV toolkit in Golang


<https://github.com/dbohdan/sqawk> -
Like Awk, but with SQL and table joins




## CSV & Programming Languages

### F#

<http://fsharp.github.io/FSharp.Data/library/CsvProvider.html> - 
F# Data: CSV Type Provider

<http://fsharp.github.io/FSharp.Data/library/CsvFile.html> -
F# Data: CSV Parser




## CSV & Databases

### PostgreSQL

<https://wiki.postgresql.org/wiki/Foreign_data_wrappers> - 
PostgreSQL Foreign Data Wrappers

### SQLite

<https://sqlite.org/csv.html> -
The CSV Virtual Table

<https://sqlite.org/vtab.html> -
The Virtual Table Mechanism Of SQLite

```
$ sqlite3
sqlite3> .mode csv
sqlite3> .import foo.csv foo
sqlite3> SELECT * FROM foo WHERE bar = 'baz';
(a bunch of rows)
```



