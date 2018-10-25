

# Awesome Comma-Separated Values (CSV) - What's Next? - Frequently Asked Questions (F.A.Q.s) - Libraries & Tools


A collection about the comma-separated values (CSV) world for rich structured data in (plain) text


#### _Contributions welcome. Anything missing? Send in a pull request. Thanks._


## CSV Family

[CSV V1.0 "Classic"](#csv-v10-classic) •
[CSV V1.1 "Modern"](#csv-v11-modern)


## CSV V1.0 "Classic" 

```
ID,Name,Code,Area,Pop
ca,Canada,CAN,9984670,34278406
us,United States,USA,9629091,314167157
mx,México [Mexico],MEX,1972550,112322757
...
```

- [IETF RFC #4180](http://tools.ietf.org/rfc/rfc4180.txt) - Common Format and MIME Type for Comma-Separated Values (CSV) Files - by Y. Shafranovich (SolidMatrix Technologies, Inc.), October 2005


### Can I use \_\_? (V1.0)


#### Q: Can I use blank lines?

**A**: No. No. No. In "classic" CSV you CANNOT use blank lines. Why? Blank lines are "ambigious". Might be a blank record or a blank line.  

Yes. Yes. Yes. See CSV V1.1 for a "modern" practical common sense version.


#### Q: Can I use comments?

**A**: No. No. No. In "classic" CSV you CANNOT use comments. Why? The original CSV format was intended just for machine reading and not for human mere mortals.

Yes. Yes. Yes. See CSV V1.1 for a "modern" human version.




## CSV V1.1 "Modern"

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



### Can I use \_\_ ? (V1.1)


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



### CSV 1.1 / CSV Next

- [CSV Next Notes](https://github.com/csvspecs/csv-next) - Better Comma-Separated Values (CSV) Notes; Adding Comments, Named Values, Multi-Line Records, and More. 



## Libraries & Tools


### Ruby

- CSV Standard Library  - [(Source)](https://github.com/ruby/csv), [(Doc)](http://ruby-doc.org/stdlib/libdoc/csv/rdoc/CSV.html)
  - [**Why the Standard Library is Broken (and How to Fix it)**](https://github.com/csvreader/docs)  - use alternative more modern better libraries  

<!--
  - skip_blanks option allows skipping blank lines (w/ no content)
  - skip_lines option allows skipping comments (configured via a text pattern/regex)
-->

- CSV Reader Library -  [(Source)](https://github.com/csvreader/csvreader) - modern alternative to the broken ruby csv standard library

- Honey Format Library / Tool - [(Source)](https://github.com/buren/honey_format), [(Doc)](https://www.rubydoc.info/gems/honey_format/) by Jacob Burenstam  --
Makes working with CSVs as smooth as honey. Proper objects for CSV headers and rows, convert column values, filter columns and rows, small(-ish) perfomance overhead, no dependencies other than Ruby standard library.

``` ruby
csv_string = <<~CSV
  email,name,born,country
  john@example.com,John,2000-03-03,SE
  jane@example.com,Jane,1970-03-03,SE
  chris@example.com,Chris,1980-03-03,DK
CSV

# Print all rows where born is before 1990 and country code is 'SE'
csv = HoneyFormat::CSV.new(csv_string, type_map: { born: :date })
csv_string = csv.to_csv(columns: %i[born country]) do |row|
  row.country == 'SE' && row.born < Date.new(1990, 1, 1)
end
puts csv_string
```

- Ruby Toolbox CSV Category - [(Link)](https://www.ruby-toolbox.com/categories/CSV_Parsers)


### Python

- Python Standard Library CSV  - [(Doc)](http://docs.python.org/3/library/csv.html)

- csvkit - [(Source)](https://github.com/onyxfish/csvkit), [(Doc)](http://csvkit.readthedocs.org)




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

- [Awesome CSV @ SecrectGeek](https://github.com/secretGeek/awesomecsv) - A curated list of awesome tools for dealing with awesome CSV 




## Meta

**License**

![](https://publicdomainworks.github.io/buttons/zero88x31.png)

The awesome list is dedicated to the public domain. Use it as you please with no restrictions whatsoever.

**Questions? Comments?**

Post them to the [wwwmake forum](http://groups.google.com/group/wwwmake). Thanks!
