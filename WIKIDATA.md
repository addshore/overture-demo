# Wikidata

I'll start with a query that looks 2.5km around the EMpire State building.
I imagine geting this list of things from multiple sources should be easy enough..

```sparql
#Places within 2km of the Empire State Building
SELECT ?place ?placeLabel ?location ?instanceLabel
WHERE
{
  wd:Q9188 wdt:P625 ?loc .
  SERVICE wikibase:around {
      ?place wdt:P625 ?location .
      bd:serviceParam wikibase:center ?loc .
      bd:serviceParam wikibase:radius "2.3" .
  }
  OPTIONAL {    ?place wdt:P31 ?instance  }
  SERVICE wikibase:label { bd:serviceParam wikibase:language "en" }
  BIND(geof:distance(?loc, ?location) as ?dist)
} ORDER BY ?dist
```