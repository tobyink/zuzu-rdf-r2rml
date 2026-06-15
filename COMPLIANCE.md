# Compliance Matrix

This matrix tracks R2RML conformance for this distribution.

| Area | Status | Test Coverage |
| --- | --- | --- |
| Mapping input | Implemented | Local tests cover Turtle mapping text and pre-parsed RDF quads. Other RDF serializations are supported by passing any parser object from the `rdf` framework. |
| Logical tables | Implemented | Local tests cover `rr:tableName` and `rr:sqlQuery`. |
| Term maps | Implemented | Local tests cover `rr:constant`, `rr:column`, `rr:template`, `rr:termType`, `rr:datatype`, and `rr:language`. |
| Triples maps | Implemented | Local tests cover subject maps, classes, predicate-object maps, and default/named graph generation. |
| Referencing object maps | Implemented | Local tests cover equality joins via `rr:parentTriplesMap` and `rr:joinCondition`; W3C R2RML cases cover the broader join set included in the R2RML suite. |
| W3C RDB2RDF R2RML test suite | Implemented | `tests/w3c-r2rml.zzs` runs 50 positive cases and 13 invalid mappings from the vendored W3C RDB2RDF R2RML suite. Direct Mapping tests are out of scope because Rowquill already supports Direct Mapping. |
