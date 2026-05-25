
# Awesome CSV - Tools, Libaries & Services



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

- CSV Standard Library - [(Doc)](http://docs.python.org/3/library/csv.html)

- csvkit - [(Source)](https://github.com/wireservice/csvkit), [(Doc)](http://csvkit.readthedocs.org)

- Panda read_csv - [(Doc)](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html)


### Perl

- Text::CSV - [(Doc)](https://metacpan.org/pod/Text::CSV)


### JavaScript

- csv-parse (for Node.js) - [(Doc)](https://csv.js.org), [(Source)](https://github.com/adaltas/node-csv)
- d3-dsv - [(Source)](https://github.com/d3/d3-dsv)
- papaparse - [(Doc)](https://www.papaparse.com/), [(Source)](https://github.com/mholt/PapaParse)

### Racket

- csv-reading - [(Doc)](https://docs.racket-lang.org/csv-reading)


### Rust

- csv - [(Doc)](https://docs.rs/csv)


### Services / Embed

- WeTransform - [(Doc)](https://www.wetransform.com), [(npm)](https://www.npmjs.com/package/@wetransform/core) - Embeddable AI file importer. Drop-in modal or iframe for B2B SaaS, customers upload CSV (or Excel, PDF, XML, JSON), the AI maps columns to your schema and validates, you receive clean data via API or webhook.



