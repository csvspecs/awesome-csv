

# Awesome Comma-Separated Values (CSV) - What's Next? - Frequently Asked Questions (F.A.Q.s) - Libraries, Tools, Services, & More


A collection about the comma-separated values (CSV) world for rich structured data in (plain) text


#### _Contributions welcome. Anything missing? Send in a pull request. Thanks._


## CSV Family

_Formats, Formats, Formats_

[CSV RFC 4180 "Strict"](#csv-rfc-4180-strict) •
[CSV v1.0 "The Right Way"](#csv-v10-the-right-way) •
[CSV <3 Numerics](#csv-3-numerics) •
[CSV <3 JSON](#csv-3-json) •
[CSV <3 YAML](#csv-3-yaml) •
[CSV v1.1 "Modern"](#csv-v11-modern)


### Related

- [CSV (Inline) Meta Data Formats](https://github.com/csvspecs/csv-meta) - CSV in CSV, Attribute-Relation "Classic", Attribute-Relation "Inline", Front Matter in YAML and More
- [CSV with YAML Front Matter Meta Data Block (CSVY)](http://csvy.org)
- [CSV with Attribute-Relation File Format (ARFF)](https://waikato.github.io/weka-wiki/arff/) 




## CSV RFC 4180 "Strict" 

```
ID,Name,Code,Area,Pop
ca,Canada,CAN,9984670,34278406
us,United States,USA,9629091,314167157
mx,México [Mexico],MEX,1972550,112322757
...
```

- [IETF RFC #4180](http://tools.ietf.org/rfc/rfc4180.txt) - Common Format and MIME Type for Comma-Separated Values (CSV) Files - by Y. Shafranovich (SolidMatrix Technologies, Inc.), October 2005

### Why the CSV RFC 4180 "Strict" Memo Is Dangerous?

People and (simplistic) CSV parser writers (and fanatics) use it to claim that it is the ultimate (and only) CSV format
and use it to end all discussions if the code breaks when you add a space before a quote or mixed quotes and so on.
It's way too simplistic (no spaces, no comments, no blank lines, no semicolon for separator, no modern two-byte characters, and so on).

Next time someone bring ups:

> Have you read the [strict] RFC 4180 [CSV format memo]? The quoting rules are in there.

Why not ask back: Have you read it? :-) Let's start at the beginning (together):

**This memo provides information for the internet community. It does
not specify an internet standard of any kind. It does
not specify an internet standard of any kind. It does
not specify an internet standard of any kind.**




### Can I use \_\_? (RFC 4180 "Strict")


#### Q: Can I use blank lines?

**A**: No. No. No. 
In the "simplistic" CSV RFC 4180 "Strict" format you CANNOT use blank lines. Why? Blank lines are "ambiguous". Might be a blank record or a blank line.  

Yes. Yes. Yes. See CSV v1.0 or CSV v1.1 for "modern" practical common sense versions.


#### Q: Can I use comments?

**A**: No. No. No. 
In the "simplistic" CSV RFC 4180 "Strict" format you CANNOT use comments. Why? The original CSV format was intended just for machine reading and not for human mere mortals.

Yes. Yes. Yes. See CSV v1.0 or CSV v1.1 for "modern" human versions.


#### Q: Can I use "literal" geo coordinates e.g. `48°51'24"N`?

**A**: No. No. No. 
In the "simplistic" CSV RFC 4180 "Strict" format you CANNOT use "literal"
double quotes (`"`) e.g. `48°51'24"N` - you MUST double quote 
the geo coordinates and double up the double quote (`""`)
e.g. `"48°51'24""N"`. Example:

```
New York City,"40°42'46""N","74°00'21""W"
Paris,"48°51'24""N","2°21'03""E"
```

Yes. Yes. Yes. See CSV v1.0 or CSV v1.1 for "modern" human versions.
Example:

```
New York City, 40°42'46"N, 74°00'21"W
Paris,         48°51'24"N, 2°21'03"E
```


#### Q: Can I use "unix-style" escaping with backslashes (e.g. `\"` for `""`)? 

**A**: No. No. No. 
In the "simplistic" CSV RFC 4180 "Strict" format you MUST double up 
the double quote (`""`)  inside double quotes. Period. Example:

```
1,"Hamlet says, ""Seems,"" madam! Nay it is; I know not ""seems."""
```

Yes. Yes. Yes. See CSV v1.0 or CSV v1.1 for "modern" human versions.
Use as you like it. Example:

```
1, "Hamlet says, \"Seems,\" madam! Nay it is; I know not \"seems.\""
```


#### Q: Can I use mixed quotes (that is, single `'...'` or double quotes `"..."`)?

**A**: No. No. No. 
In the "simplistic" CSV RFC 4180 "Strict" format you MUST always use
double quotes (`""`) and double up the double quote inside double quotes. Period.

Yes. Yes. Yes. See CSV v1.0 or CSV v1.1 for "modern" human versions.
Use as you like it. Example:

```
1, "Hamlet says, 'Seems,' madam! Nay it is; I know not 'seems.'"
2, 'Hamlet says, "Seems," madam! Nay it is; I know not "seems."'
```





## CSV v1.0 "The Right Way"

Q: What's CSV the right way? What best practices can I use?  

Use best practices out-of-the-box with zero-configuration.
Do you know how to skip blank lines or how to add `#` single-line comments?
Or how to trim leading and trailing spaces?  No worries. It's turned on by default.

Yes, you can. Use

```
#######
# try with some comments
#   and blank lines even before header (first row)

Brewery,City,Name,Abv
Andechser Klosterbrauerei,Andechs,Doppelbock Dunkel,7%
Augustiner Bräu München,München,Edelstoff,5.6%

Bayerische Staatsbrauerei Weihenstephan,  Freising,  Hefe Weissbier,   5.4%
Brauerei Spezial,                         Bamberg,   Rauchbier Märzen, 5.1%
Hacker-Pschorr Bräu,                      München,   Münchner Dunkel,  5.0%
Staatliches Hofbräuhaus München,          München,   Hofbräu Oktoberfestbier, 6.3%
```

instead of strict "classic"
(no blank lines, no comments, no leading and trailing spaces, etc.):

```
Brewery,City,Name,Abv
Andechser Klosterbrauerei,Andechs,Doppelbock Dunkel,7%
Augustiner Bräu München,München,Edelstoff,5.6%
Bayerische Staatsbrauerei Weihenstephan,Freising,Hefe Weissbier,5.4%
Brauerei Spezial,Bamberg,Rauchbier Märzen,5.1%
Hacker-Pschorr Bräu,München,Münchner Dunkel,5.0%
Staatliches Hofbräuhaus München,München,Hofbräu Oktoberfestbier,6.3%
```


Or use the ARFF (attribute-relation file format)-like alternative style
with `%` for comments and `@`-directives
for "meta data" in the header (before any records):

```
%%%%%%%%%%%%%%%%%%
% try with some comments
%   and blank lines even before @-directives in header

@RELATION Beer

@ATTRIBUTE Brewery
@ATTRIBUTE City
@ATTRIBUTE Name
@ATTRIBUTE Abv

@DATA
Andechser Klosterbrauerei,Andechs,Doppelbock Dunkel,7%
Augustiner Bräu München,München,Edelstoff,5.6%

Bayerische Staatsbrauerei Weihenstephan,  Freising,  Hefe Weissbier,   5.4%
Brauerei Spezial,                         Bamberg,   Rauchbier Märzen, 5.1%
Hacker-Pschorr Bräu,                      München,   Münchner Dunkel,  5.0%
Staatliches Hofbräuhaus München,          München,   Hofbräu Oktoberfestbier, 6.3%
```

Or use the ARFF (attribute-relation file format)-like alternative style with  `@`-directives
inside comments (for easier backwards compatibility with old readers)
for "meta data" in the header (before any records):

```
##########################
# try with some comments
#   and blank lines even before @-directives in header
#
# @RELATION Beer
#
# @ATTRIBUTE Brewery
# @ATTRIBUTE City
# @ATTRIBUTE Name
# @ATTRIBUTE Abv

Andechser Klosterbrauerei,Andechs,Doppelbock Dunkel,7%
Augustiner Bräu München,München,Edelstoff,5.6%

Bayerische Staatsbrauerei Weihenstephan,  Freising,  Hefe Weissbier,   5.4%
Brauerei Spezial,                         Bamberg,   Rauchbier Märzen, 5.1%
Hacker-Pschorr Bräu,                      München,   Münchner Dunkel,  5.0%
Staatliches Hofbräuhaus München,          München,   Hofbräu Oktoberfestbier, 6.3%
```

Or use the CSV meta data in CSV style:

```
##########################
# try with some comments
#   and blank lines even header

Col, Name
1,   Brewery
2,   City
3,   Name
4,   Abv


Andechser Klosterbrauerei,Andechs,Doppelbock Dunkel,7%
Augustiner Bräu München,München,Edelstoff,5.6%

Bayerische Staatsbrauerei Weihenstephan,  Freising,  Hefe Weissbier,   5.4%
Brauerei Spezial,                         Bamberg,   Rauchbier Märzen, 5.1%
Hacker-Pschorr Bräu,                      München,   Münchner Dunkel,  5.0%
Staatliches Hofbräuhaus München,          München,   Hofbräu Oktoberfestbier, 6.3%
```




## CSV <3 Numerics

CSV ❤ Numerics Format - Comma-Separated Values (CSV) Line-by-Line Records with Auto-Converted Numerics (Float Numbers) Encoding Rules - A Modern (Simple) Tabular Data Format incl. Numbers, Comments and More

See [`csvspecs/csv-numerics` »](https://github.com/csvspecs/csv-numerics)



## CSV <3 JSON

CSV ❤ JSON Format - Comma-Separated Values (CSV) Line-by-Line Records with JSON Encoding Rules - A Modern (Simple) Tabular Data Format incl. Arrays, Numbers, Booleans, Nulls, Nested Structures, Comments and More

Examples:

```
# "Vanilla" CSV <3 JSON

1,"John","12 Totem Rd. Aspen",true
2,"Bob",null,false
3,"Sue","Bigsby, 345 Carnival, WA 23009",false
```

or

```
# "Vanilla" CSV <3 JSON (Pretty Printed)

1, "John", "12 Totem Rd. Aspen",            true
2, "Bob",  null,                            false
3, "Sue", "Bigsby, 345 Carnival, WA 23009", false
```

See [`csvspecs/csv-json` »](https://github.com/csvspecs/csv-json)


## CSV <3 YAML

CSV ❤ YAML Format - Comma-Separated Values (CSV) Line-by-Line Records with YAML Encoding Rules - A Modern (Simple) Tabular Data Format incl. Arrays, Numbers, Booleans, Nulls, Nested Structures, Comments and More

Examples:

```
# "Vanilla" CSV <3 YAML

1,John,12 Totem Rd. Aspen,true
2,Bob,null,false
3,Sue,"Bigsby, 345 Carnival, WA 23009",false
```

or

```
# "Vanilla" CSV <3 YAML (Pretty Printed)

1, John, 12 Totem Rd. Aspen,               true
2, Bob,  null,                             false
3, Sue,  "Bigsby, 345 Carnival, WA 23009", false
```

See [`csvspecs/csv-yaml` »](https://github.com/csvspecs/csv-yaml)


## CSV v1.1 "Modern"

```
#####################
# North America

# area (in sq km), pop(ulation)

ca, Canada,          CAN,   9 984 670 km²,  34 278 406
us, United States,   USA,   9 629 091 km², 314 167 157
mx, México [Mexico], MEX,   1 972 550 km², 112 322 757
...
```

- [CSV 1.1 - Comma Separated (Named) Values, Version: 1.1](https://github.com/csvspecs/csv-v11) - CSV evolved (for humans) - easy-to-write, easy-to-read



### Can I use \_\_ ? (v1.1)


#### Q: Can I use blank lines?

**A**: Yes, of course. A blank line is just a blank line. Use freely to format (beautify) your data.


#### Q: Can I use comments?

**A**: Yes, of course. Use `#` for comments. See the example above.



## Delimiter / Separator

_Why use commas, commas, commas?_

[Space](#space) •
[Tab](#tab) •
[Field Separator (FS)](#field-separator-fs) •
[Other](#other)


### Space

Did you know? In the English (or German) language the most popular word delimiter / separator is - surprise, surprise - space.
You're looking at spaces in action right now and right here ;-)

Why not use spaces?

- Spaces work great (and are the best) only if you do NOT use s p a c e s · i n · v a l u e s. 
For example, is `United States` one value or two? See?
- If it's only one value than you need to quote it e.g. `"United States"`. 

By using commas you do NOT need to quote spaces in values, that is, use 
`us, United States, USA` instead of `us "United States" USA`.


### Tab 

In theory the tab (`\t`) separator is perfect. Values never use tabs, don't they?  So why hasn't the tab separator taken off?

In practice tab separators are invisible or look like spaces and often you cannot tell if a space is a tab or not. 

Thus, tab works great only and only (like space) if your values do NOT use spaces and you treat a tab like a space.



### Field Separator (FS)

Again in theory the untypeable (unprintable) field separator (ASCII Code 31) is perfect. Values never use ASCII field separators.

In practice if the field separator is invisible and unprintable how do you type it on your keyboard? 

Remember: The point of comma-separated values (CSV) is an easy-to-write and easy-to-read format for humans first (not for machines).



### Other

- Pipe (`|`)
- Semicolon (`;`)
- Colon  (`:`)
- Interpunct  (`·`)
- Double Interpunct 
- And many others



## Articles

**Wikipedia**

- [Comma-separated values](http://en.wikipedia.org/wiki/Comma-separated_values)
- [Delimiter-separated values](https://en.wikipedia.org/wiki/Delimiter-separated_values)
- [Delimiter](https://en.wikipedia.org/wiki/Delimiter) - why not space, tab, pipe, ascii 31 - field separator (fs), etc.
- [String literal](https://en.wikipedia.org/wiki/String_literal) - (string) values with or without quotes; how to escape quotes, etc.
- [Word divider](https://en.wikipedia.org/wiki/Word_divider) - scriptio continua or space, interpunct, double interpunct, etc.


**More**

- [Textuality - Data File Metaformats @ The Art of Unix Programming](http://www.catb.org/esr/writings/taoup/html/ch05s02.html) by Eric S. Raymond



## Initiatives

[Frictionless Data](#frictionless-data) •
[CSV on the Web](#csv-on-the-web) •
[CSV 1.1 / CSV Next](#csv-11--csv-next)


### Frictionless Data 

_lightweight standards and tooling to make it effortless to get, share, and validate data_ 

by Open Knowledge Foundation (OKFN)

web: [frictionlessdata.io](http://frictionlessdata.io), github: [frictionlessdata](https://github.com/frictionlessdata) 

- [Comma-Separated Values Guide](http://frictionlessdata.io/guides/csv)



### CSV on the Web

by World Wide Web Consortium (W3C)

github: [w3c/csvw](https://github.com/w3c/csvw)


- [CSV on the Web: A Primer](https://www.w3.org/TR/2016/NOTE-tabular-data-primer-20160225/)



### CSV v1.1 / CSV Next

- [CSV Next Notes](https://github.com/csvspecs/csv-next) - Better Comma-Separated Values (CSV) Notes; Adding Comments, Named Values, Multi-Line Records, and More. 



## Libraries, Tools, Services, & More

see [SERVICES.md »](SERVICES.md)



## Conferences


### CSV,Conf

_A conference for data makers everywhere_

web: [csvconf.com](https://csvconf.com), 
github: [csvconf](https://github.com/csvconf),
twitter: [CSVConference](https://twitter.com/CSVConference)

- [csv,conf,v4](https://csvconf.com)       - 2019 - May 8+9 @ Portland, Oregon, United States
- [csv,conf,v3](https://csvconf.com/2017/) - 2017 - May 2+3 @ Portland, Oregon, United States
- [csv,conf,v2](https://csvconf.com/2016/) - 2016 - May 3+4 @ Berlin, Germany
- [csv,conf,v1](https://csvconf.com/2014/) - 2014 - July 15 @ Berlin, Germany



## Awesome Awesomeness

_A curated list of awesome lists._

- [Awesome CSV @ SecrectGeek](https://github.com/secretGeek/awesomecsv) - An awesome list of tools for dealing with CSV by Leon Bambrick




## Meta

**License**

The awesome list is dedicated to the public domain. Use it as you please with no restrictions whatsoever.

**Questions? Comments?**

Post them to the [wwwmake forum](http://groups.google.com/group/wwwmake). Thanks!
