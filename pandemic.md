# Pandemic research

Bestilling: Pandemic Centre at UiB

Date: Spring 2025

Resulting report: https://hdl.handle.net/11250/3182716

## Scope

Everything that mentions covid-19, the covid-19 pandemic or pandemics in any context or discipline, from Norwegian institutions from 2020 onwards. Should find results both in English and Norwegian, and of diverse publication types (articles, books, chapters, reports, dissertations; but not media outputs or datasets).

Certain concepts connected to the pandemic were tested but taken out when they proved too noisy for this particular use case (unless combined with other pandemic terms). Note that research on these topics is not excluded, but will not be found unless also referencing some of the other search terms (e.g. covid-19 or the pandemic). These included:
- Epidemics
- Working from home
- Personal protective equipment

Timespan: Publication date = 2020-01-01 to 2024 as much as possible

## Other strings used/copied

The following strings were used for inspiration, to find terminology, and in some cases lines are copied from:

- PubMed covid-19 article filters: https://pubmed.ncbi.nlm.nih.gov/help/#covid19-article-filters
- Canada's Drug Agency covid-19 search strings: https://www.cda-amc.ca/literature-searching-tools/covid-19-search-strings
- Carrie Price MLS: https://carrieprice78.github.io/guides/search-filters/coronavirus/

## Search strings

As we are restricting the search to 2020 onwards, we can simplify the search for coronavirus terms (i.e. go broader by not specifying which coronavirus). 

### Search string, Web of Science

Web of Science (Clarivate) (English only; Topic (title, abstract, keywords, keywordsplus) 

Databases
- WOS.SCI: 1945 to 2024
- WOS.AHCI: 1975 to 2024
- WOS.ESCI: 2019 to 2024
- WOS.SSCI: 1956 to 2024

#### 1

```py
TS=(
"coronavirus*" OR "corona virus*" OR "covid"
OR "corona infection" OR "corona vaccin*" 
OR "COVID19*" OR "COVID2019" OR "COVID-19*" OR "COVID-2019*" 
OR "SARS-CoV-2019" OR "SARS-CoV-19"
OR "SARS-CoV-2" OR "SARS-COV2" OR "SARSCOV-2" OR "SARSCOV2" OR "SARSCoV"
OR "NCOV" OR "2019-nCoV" OR "2019nCoV" OR "SARS-nCoV" OR "SARSnCoV"
OR "pandemic*"
)
```

- I tested using variations of e.g. "omicron", "delta variant" etc. but this lead to irrelevant results. Two relevant results used "omicron" but many more were irrelevant (and these two are added by the Web of Science Citation cateogy in search #4). "omicron" is thus only included in the Cristin title search. 

#### 2

```py
TS=(
"facemask*" OR "face mask*" OR "surgical mask*" OR "face shield*" OR "FFP1" OR "FFP2"
OR (("N99" OR "N95" OR "N 99" OR "N 95" OR "FFP" OR "P100") NEAR/3 "respirator*")
OR 	(("respiratory" OR "facial" OR "N99" OR "N95" OR "N 99" OR "N 95")
	NEAR/3 ("mask" OR "masks")
	)
)
NOT TS=("neonatal" OR "newborn" OR "resuscitation")
```

- Originally this search contained a line for PPE - but many other fields use these terms (e.g. firefighters, construction workers), and the abbreviation is used for many other things. In practice, this part of the search only adds two additional results for Norway in the target years, and these are not specifically about the pandemic, therefore it is dropped. Original search tested: `(("personal protective equipment") NOT ("construction" OR "firefight*" OR "kiln" OR "cement" OR "police" OR "recycl*" OR "radiation" OR "ship*" OR "oil" OR "H2S" OR "mining" OR "miner*" OR "mercury" OR "heavy metal*" OR "soot" OR "agricult*" OR "farm*" OR "pesticide*" OR "cold"))`
- Face mask results are not always about the pandemic but do mostly seem to be about medical face masks. I have tried to exclude results about neonatal ventilation/resuscitation, which also use face masks.

#### 3

```py
TS=("lockdown*" OR "social distancing" OR "physical distancing")
```

- Here I tried with "social distanc*" but "social distance" seems to be mostly about non-pandemic topics, while "distancing" is much more focused.
- I also tried with `TS=("work from home" OR "working from home" OR "home office" OR "school closure$")`, but in Norway and the year restrictions it gave no extra results to phrase #1 anyway. In general testing it can add some results about the pandemic, but many more generally about working from home, and we decided that this was too far outside the scope for this use-case.

#### 4

```py
TMIC=("1.104.1353 Coronavirus")
```

- TMIC = Micro Level Citation Topic. https://incites.help.clarivate.com/Content/Research-Areas/citation-topics.htm
  
#### 5

```py
(#1 OR #2 OR #3 OR #4)
AND CU="Norway"
AND PY=2020-2024
```

https://www.webofscience.com/wos/woscc/summary/c36fc976-aa14-4e0f-8e9a-3e399997473a-011199caf1/relevance/1

Note, year published ("PY") includes both the "Published early access year" and the "Final publication year". From Clarivate's Web of Science help:
> "For example, searching Year Published = 2022, will return items with Final Publication Year of 2022 and any items with Published Early Access Year of 2022. This will also impact the years displayed for Refine an Analyze Results. In the case where an item's Published Early Access Year is different from the Final Publication Year, the Published Early Access year will be used for both Refine and Analyze. Thus, a search of Year Published=2021 may show a Refine Results for Publication year with items listed for 2019, 2020 and 2021."

### Search PubMed

MeSH and all fields term search (English only). Here we do a search using the general covid-19 filter as pre-defined by PubMed (all covid terms in the search below are automatically added through this, https://pubmed.ncbi.nlm.nih.gov/help/#covid19-article-filters). Note that the Affiliation field in PubMed does not always work well, depending on what metadata the journal supplies. In previous work I have seen that country affiliation is missing for Tidsskrift for den norske legeforening - therefore this journal is included as a search term, as it is central in Norway.

```py
(
	("Norway"[Affiliation] OR "tidsskrift for den norske laegeforening tidsskrift for praktisk medicin ny raekke"[Journal])
	AND ("covid 19"[All Fields] OR "covid19"[All Fields] OR "covid 19"[MeSH Terms] OR "covid 19 vaccines"[All Fields] OR "covid 19 vaccines"[MeSH Terms] OR "covid 19 serotherapy"[All Fields] OR "covid 19 serotherapy"[MeSH Terms] OR "covid 19 nucleic acid testing"[All Fields] OR "covid 19 nucleic acid testing"[MeSH Terms] OR "covid 19 serological testing"[All Fields] OR "covid 19 serological testing"[MeSH Terms] OR "covid 19 testing"[All Fields] OR "covid 19 testing"[MeSH Terms] OR "sars cov 2"[All Fields] OR "sarscov2"[All Fields] OR "sarscov 2"[All Fields] OR "sars cov2"[All Fields] OR "sars cov 2"[MeSH Terms] OR "severe acute respiratory syndrome coronavirus 2"[All Fields] OR "2019 ncov"[All Fields] OR (("coronavirus"[MeSH Terms] OR "coronavirus"[All Fields] OR "cov"[All Fields] OR "ncov"[All Fields]) AND 2019/11/01:3000/12/31[Date - Publication]))
)
AND (2020:2024[pdat]) 
```

### Search string, Cristin

Norway's national CRIS system (Cristin) via Tableau DUCT (from Sikt) (English and Norwegian; title search only)

- Truncation of "corona" is limited to avoid "coronary". The same issue occurs in Norwegian with "korona", but is a rare issue in publication titles, and we miss many more relevant results by limiting it (e.g. koronatiltak, koronatid, koronakrise...).
- "face mask" was tested, but only added irrelevant results about face masks for neonatal resuscitation for theses, and added only 3 relevant results for articles (and more irrelevant). Therefore it was removed. 
- "PPE"/"personal protective equipment" do not add any additional relevant results when searching Cristin and are therefore dropped (`OR CONTAINS(LOWER([result_title]),"personal protective equipment") OR REGEXP_MATCH(([result_title]), "\bPPE\b")`. The same applies to mask types (e.g. N95) which only added irrelevant works.
- "omicron" is added as a variant, but not others (e.g. alpha, delta). This is because alpha, beta, delta are common terms in other non-covid related fields, plus they do not give any additional results in this particular case.
- Originally terms about home office in general were included, but now has been removed as too far outside the scope (`"home office", "working from home", "work from home", "hjemmekontor"`).

```py
IF 
CONTAINS(LOWER([result_title]),	"pandemi"	)
OR CONTAINS(LOWER([result_title]),	"covid"	)
OR CONTAINS(LOWER([result_title]),	"coronavirus"	)
OR REGEXP_MATCH(LOWER([result_title]), "\bcorona\b")
OR CONTAINS(LOWER([result_title]),	"korona"	)
OR REGEXP_MATCH(([result_title]), "\bSARS")
OR REGEXP_MATCH(LOWER([result_title]), "\bncov")
OR REGEXP_MATCH(LOWER([result_title]), "\bsars-cov")
OR REGEXP_MATCH(LOWER([result_title]), "\bsarscov")
OR REGEXP_MATCH(([result_title]), "\bCoV\b")
OR REGEXP_MATCH(([result_title]), "\bCoV2\b")
OR REGEXP_MATCH(([result_title]), "\bCOV\b")
OR REGEXP_MATCH(([result_title]), "\bCOV2\b")
OR CONTAINS(LOWER([result_title]), "omicron"	)
OR CONTAINS(LOWER([result_title]), "omikron"	)

OR CONTAINS(LOWER([result_title]),	"face mask"	)
OR CONTAINS(LOWER([result_title]),	"facemask"	)
OR CONTAINS(LOWER([result_title]),	"ansiktsmask"	)

OR CONTAINS(LOWER([result_title]),	"quarantine"	)
OR CONTAINS(LOWER([result_title]),	"karantene"	)
OR CONTAINS(LOWER([result_title]),	"lock-down"	)
OR CONTAINS(LOWER([result_title]),	"lockdown"	)
OR CONTAINS(LOWER([result_title]),	"nedstenging"	)
OR CONTAINS(LOWER([result_title]),	"en-metersregel"	)
OR CONTAINS(LOWER([result_title]),	"en metersregel"	)
OR CONTAINS(LOWER([result_title]),	"hjemmeskole"	)
OR CONTAINS(LOWER([result_title]),	"skolestenging"	)
THEN "pandemic"

ELSEIF 
CONTAINS(LOWER([result_title_anthology]),	"pandemi"	)
OR CONTAINS(LOWER([result_title_anthology]),	"covid"	)
OR CONTAINS(LOWER([result_title_anthology]),	"coronavirus"	)
OR REGEXP_MATCH(LOWER([result_title_anthology]), "\bcorona\b")
OR CONTAINS(LOWER([result_title_anthology]),	"korona"	)
OR REGEXP_MATCH(([result_title_anthology]), "\bSARS")
OR REGEXP_MATCH(LOWER([result_title_anthology]), "\bsars-cov")
OR REGEXP_MATCH(LOWER([result_title_anthology]), "\bsarscov")
OR REGEXP_MATCH(LOWER([result_title_anthology]), "\bncov")
OR REGEXP_MATCH(([result_title_anthology]), "\bCoV\b")
OR REGEXP_MATCH(([result_title_anthology]), "\bCoV2\b")
OR REGEXP_MATCH(([result_title_anthology]), "\bCOV\b")
OR REGEXP_MATCH(([result_title_anthology]), "\bCOV2\b")

OR CONTAINS(LOWER([result_title_anthology]),	"face mask"	)
OR CONTAINS(LOWER([result_title_anthology]),	"facemask"	)
OR CONTAINS(LOWER([result_title_anthology]),	"ansiktsmask"	)

OR CONTAINS(LOWER([result_title_anthology]),	"quarantine"	)
OR CONTAINS(LOWER([result_title_anthology]),	"karantene"	)
OR CONTAINS(LOWER([result_title_anthology]),	"lock-down"	)
OR CONTAINS(LOWER([result_title_anthology]),	"lockdown"	)
OR CONTAINS(LOWER([result_title_anthology]),	"nedstenging"	)
OR CONTAINS(LOWER([result_title_anthology]),	"en-metersregel"	)
OR CONTAINS(LOWER([result_title_anthology]),	"en metersregel"	)
OR CONTAINS(LOWER([result_title_anthology]),	"hjemmeskole"	)
OR CONTAINS(LOWER([result_title_anthology]),	"skolestenging"	)
THEN "pandemic"

END
```

### Search string, BORA (Bergen Open Research Archive)

This search is for looking within the archive for master theses and PhD dissertations. It is based on the Cristin search over. (English and Norwegian; title, abstract and keyword search)

- While in the Cristin search "korona" was not limited in any way, here it mainly adds extra results about coronary issues (likely because so many works in BORA have a Norwegian abstract). Therefore, "korona" is limited in this search. A few more Norwegian "korona" terms are added to catch the two relevant works that were found by unlimited "korona".  

```
IF 
CONTAINS(LOWER([name]),	"pandemi"	)
OR CONTAINS(LOWER([name]),	"covid"	)
OR CONTAINS(LOWER([name]),	"coronavirus"	)
OR REGEXP_MATCH(LOWER([name]), "\bcorona\b")
OR REGEXP_MATCH(LOWER([name]), "korona\b")
OR CONTAINS(LOWER([name]),	"koronavirus"	)
OR CONTAINS(LOWER([name]),	"koronatiltak"	)
OR CONTAINS(LOWER([name]),	"koronakris"	)
OR CONTAINS(LOWER([name]),	"koronasituas"	)
OR CONTAINS(LOWER([name]),	"koronavaksin"	)
OR REGEXP_MATCH(([name]), "\bSARS")
OR REGEXP_MATCH(LOWER([name]), "\bncov")
OR REGEXP_MATCH(LOWER([name]), "\bsars-cov")
OR REGEXP_MATCH(LOWER([name]), "\bsarscov")
OR REGEXP_MATCH(([name]), "\bCoV\b")
OR REGEXP_MATCH(([name]), "\bCoV2\b")
OR REGEXP_MATCH(([name]), "\bCOV\b")
OR REGEXP_MATCH(([name]), "\bCOV2\b")
OR CONTAINS(LOWER([name]), "omicron"	)
OR CONTAINS(LOWER([name]), "omikron"	)

OR CONTAINS(LOWER([name]),	"ansiktsmask"	)

OR CONTAINS(LOWER([name]),	"quarantine"	)
OR CONTAINS(LOWER([name]),	"karantene"	)
OR CONTAINS(LOWER([name]),	"lock-down"	)
OR CONTAINS(LOWER([name]),	"lockdown"	)
OR CONTAINS(LOWER([name]),	"nedstenging"	)
OR CONTAINS(LOWER([name]),	"en-metersregel"	)
OR CONTAINS(LOWER([name]),	"en metersregel"	)
OR CONTAINS(LOWER([name]),	"hjemmeskole"	)
OR CONTAINS(LOWER([name]),	"skolestenging"	)
THEN "pandemic"

ELSEIF
CONTAINS(LOWER([dc.description.abstract]),	"pandemi"	)
OR CONTAINS(LOWER([dc.description.abstract]),	"covid"	)
OR CONTAINS(LOWER([dc.description.abstract]),	"coronavirus"	)
OR REGEXP_MATCH(LOWER([dc.description.abstract]), "\bcorona\b")
OR REGEXP_MATCH(LOWER([dc.description.abstract]), "korona\b")
OR CONTAINS(LOWER([dc.description.abstract]),	"koronavirus"	)
OR CONTAINS(LOWER([dc.description.abstract]),	"koronatiltak"	)
OR CONTAINS(LOWER([dc.description.abstract]),	"koronakris"	)
OR CONTAINS(LOWER([dc.description.abstract]),	"koronasituas"	)
OR CONTAINS(LOWER([dc.description.abstract]),	"koronavaksin"	)
OR REGEXP_MATCH(([dc.description.abstract]), "\bSARS")
OR REGEXP_MATCH(LOWER([dc.description.abstract]), "\bncov")
OR REGEXP_MATCH(LOWER([dc.description.abstract]), "\bsars-cov")
OR REGEXP_MATCH(LOWER([dc.description.abstract]), "\bsarscov")
OR REGEXP_MATCH(([dc.description.abstract]), "\bCoV\b")
OR REGEXP_MATCH(([dc.description.abstract]), "\bCoV2\b")
OR REGEXP_MATCH(([dc.description.abstract]), "\bCOV\b")
OR REGEXP_MATCH(([dc.description.abstract]), "\bCOV2\b")
OR CONTAINS(LOWER([dc.description.abstract]), "omicron"	)
OR CONTAINS(LOWER([dc.description.abstract]), "omikron"	)

OR CONTAINS(LOWER([dc.description.abstract]),	"ansiktsmask"	)

OR CONTAINS(LOWER([dc.description.abstract]),	"quarantine"	)
OR CONTAINS(LOWER([dc.description.abstract]),	"karantene"	)
OR CONTAINS(LOWER([dc.description.abstract]),	"lock-down"	)
OR CONTAINS(LOWER([dc.description.abstract]),	"lockdown"	)
OR CONTAINS(LOWER([dc.description.abstract]),	"nedstenging"	)
OR CONTAINS(LOWER([dc.description.abstract]),	"en-metersregel"	)
OR CONTAINS(LOWER([dc.description.abstract]),	"en metersregel"	)
OR CONTAINS(LOWER([dc.description.abstract]),	"hjemmeskole"	)
OR CONTAINS(LOWER([dc.description.abstract]),	"skolestenging"	)
THEN "pandemic"

ELSEIF
CONTAINS(LOWER([dc.subject]),	"pandemi"	)
OR CONTAINS(LOWER([dc.subject]),	"covid"	)
OR CONTAINS(LOWER([dc.subject]),	"coronavirus"	)
OR REGEXP_MATCH(LOWER([dc.subject]), "\bcorona\b")
OR REGEXP_MATCH(LOWER([dc.subject]), "korona\b")
OR CONTAINS(LOWER([dc.subject]),	"koronavirus"	)
OR CONTAINS(LOWER([dc.subject]),	"koronatiltak"	)
OR CONTAINS(LOWER([dc.subject]),	"koronakris"	)
OR CONTAINS(LOWER([dc.subject]),	"koronasituas"	)
OR CONTAINS(LOWER([dc.subject]),	"koronavaksin"	)
OR REGEXP_MATCH(([dc.subject]), "\bSARS")
OR REGEXP_MATCH(LOWER([dc.subject]), "\bncov")
OR REGEXP_MATCH(LOWER([dc.subject]), "\bsars-cov")
OR REGEXP_MATCH(LOWER([dc.subject]), "\bsarscov")
OR REGEXP_MATCH(([dc.subject]), "\bCoV\b")
OR REGEXP_MATCH(([dc.subject]), "\bCoV2\b")
OR REGEXP_MATCH(([dc.subject]), "\bCOV\b")
OR REGEXP_MATCH(([dc.subject]), "\bCOV2\b")
OR CONTAINS(LOWER([dc.subject]), "omicron"	)
OR CONTAINS(LOWER([dc.subject]), "omikron"	)

OR CONTAINS(LOWER([dc.subject]),	"ansiktsmask"	)

OR CONTAINS(LOWER([dc.subject]),	"quarantine"	)
OR CONTAINS(LOWER([dc.subject]),	"karantene"	)
OR CONTAINS(LOWER([dc.subject]),	"lock-down"	)
OR CONTAINS(LOWER([dc.subject]),	"lockdown"	)
OR CONTAINS(LOWER([dc.subject]),	"nedstenging"	)
OR CONTAINS(LOWER([dc.subject]),	"en-metersregel"	)
OR CONTAINS(LOWER([dc.subject]),	"en metersregel"	)
OR CONTAINS(LOWER([dc.subject]),	"hjemmeskole"	)
OR CONTAINS(LOWER([dc.subject]),	"skolestenging"	)
THEN "pandemic"

END
``
