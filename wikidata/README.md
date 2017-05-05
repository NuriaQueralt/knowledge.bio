# Wikidata items #
## SPARQL queries ##
### Get label, synonyms, description for for a selected list of diseases as DOID ###
~~~sparql
SELECT DISTINCT ?item ?doid ?itemLabel (group_concat(distinct ?itemaltLabel; separator="|") as ?altLabel) ?itemDesc
WHERE
{
  {?item wdt:P31 wd:Q12136 }
  UNION
  {?item wdt:P279 wd:Q12136 .}
  ?item wdt:P699 ?doid .
  values ?doid {"DOID:0050602" "DOID:0060308" "DOID:0060728" "DOID:10595" "DOID:11589" "DOID:2476" "DOID:5212"}
  OPTIONAL{
  ?item skos:altLabel ?itemaltLabel .
    FILTER(LANG(?itemaltLabel) = "en")
  ?item schema:description ?itemDesc .
    FILTER(LANG(?itemDesc) = "en")
  }
  SERVICE wikibase:label { bd:serviceParam wikibase:language "en" }
}
group by ?item ?doid ?itemLabel ?itemDesc
~~~
[Execute](http://tinyurl.com/ljlmqrn)
