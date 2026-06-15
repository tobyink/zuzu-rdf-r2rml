# rdf-r2rml

R2RML materialisation for the ZuzuScript `rdf` distribution.

This distribution provides `rdf/r2rml`, which can populate an `RDFStore`
from a `std/db` database handle using an R2RML mapping. Mapping input may be
pre-parsed RDF quads or serialized RDF parsed by a parser object from the
main `rdf` framework. Turtle is used by default.

Direct Mapping is intentionally not implemented here; Rowquill already
supports that shape.

## Example

```zzs
from rdf/r2rml import r2rml_materialize;
from rdf/store import RDFStore;
from std/db import DB;

let dbh := DB.temp();
dbh.prepare( "create table people (id integer, name text)" ).execute();
dbh.prepare( "insert into people (id, name) values (1, 'Ada')" ).execute();

let store := RDFStore.temp();
store.install_schema();

r2rml_materialize( dbh, """
@prefix rr: <http://www.w3.org/ns/r2rml#> .
@prefix ex: <http://example.com/> .

<#People>
	rr:logicalTable [ rr:tableName "people" ];
	rr:subjectMap [
		rr:template "http://example.com/person/{id}";
		rr:class ex:Person;
	];
	rr:predicateObjectMap [
		rr:predicate ex:name;
		rr:objectMap [ rr:column "name" ];
	].
""", into: store );
```

## Current Scope

The implementation is built against
[R2RML](https://www.w3.org/TR/r2rml/) and the W3C
[R2RML test cases](https://www.w3.org/TR/rdb2rdf-test-cases/). It currently
supports logical tables from `rr:tableName` and `rr:sqlQuery`, subject maps,
predicate-object maps, constant/column/template term maps, classes, named
graphs, datatypes, language tags, and basic referencing object maps.

The R2RML cases from the W3C RDB2RDF suite are vendored under
`tests/w3c/rdb2rdf` and run by `tests/w3c-r2rml.zzs`, covering 50 positive
cases and 13 invalid mappings. Direct Mapping is out of scope for this
distribution.
