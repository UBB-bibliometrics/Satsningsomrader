# GSU

Identifies scientific articles/books/chapters connected to the global challenges priority area. String to use in Tableau against "FOR_data_sted_total"-extract from DUCT or live.

*A number of terms are included twice in different parts of the string - once for article title, and another time for book title - remember to edit both if making changes*

As we are searching in the titles only, the terms used are broad. Search terms will always be searched for in truncated form, unless a space is included at the beginning/end (e.g. "migrant" finds "migrants"), this works also for journal/anthology/book titles ("global health" finds "global health action").

## Description provided in reports

Tematiske områder som er inkludert i den bibliometriske kartleggingen 2020 (Bibliometrigruppen, Universitetsbiblioteket i samråd med forskningsdekan Marit Bakke, og direktøren Bente Moen)

#### Global helse

Helse-relatert forskning med fokus på global helse: 
* helse (ink. psykisk helse og helsefremmende arbeid), sykdommer og helsetjenester i «low and middle income countries» (LMCs). Medisinsk eller helseforskning utenfor disse land (e.g. generell kreftforskning, kreft i Norge) er ikke inkludert, med mindre den faller inn under et annet aspekt for satsningsområdet
* sykdommer og folkehelseproblemer som er mest vanlig i LMCs (e.g. malaria, neglected tropical diseases, maternal mortality)
* global health, internasjonal helse
* klimaendringer eller naturkatastrofe og helse

Helse og Migrasjon:
* All forskning som gjelder migranter/flyktninger og helse (ink. psykisk helse), sykdommer eller helsetjenester, eller helse og flerkulturelt samfunn. Eksempler kan inkludere tilgang til helsetjenester for flyktninger, eller arbeidsforhold for migrant helsearbeidere. 

Helse og Ulikhet:
* lik representasjon/prioritering innen helseforskning (etikk, kjønn, etnisitet og juridiske utfordringer) 
* forskjellsbehandling og helse; helse/helsetjenester sett i lyset av kjønn, etnisitet, funksjonsevne osv. 
* tilgang til helsetjenester (ink. seksuelle eller psykiske helsetjenester)
* helse av/vold mot sårbare grupper eller grupper som kan oppleve diskriminering; barnevern
* helse og fattigdom eller økonomisk ulikhet
* helse og utviklingsmidler, globalisation
* body politics

#### Migrasjon 
All forskning som omhandler migrasjon, flykninger, asyl, eller immigrasjon (ikke avgrenset ytterligere), for eksempel (men ikke begrenset til):
* Media and samfunnsdebatt om migrasjons/immigranter 
* Flerkulturelt samfunn og integrering
* Migration in historic times
* Migration and resilient cities
* Migrasjon og klimaendringer 

Helse og Migrasjon (beskrevet over)

Migrasjon og Ulikhet:
* migranter/flyktninger/asylsøkere og 
  *	forskjellsbehandling, equity, representasjon og eksklusjon
  * folkerett, menneskerettighet, juridiske problemstillinger, frihet og sikkerhet
  *	fattigdom og økonomisk ulikhet
  *	alder, kjønn, seksualitet, funksjonsevner, sårbare grupper
  *	matsikkerhet
  *	kolonialisme
*	forskjellsbehandling knyttet til religion av migranter (e.g. islamophobia)
*	smugling og traffiking av personer 

#### Ulikhet
*	equality og equity
*	menneskerettigheter, sivilrettigheter, land rights 
*	fattigdom og økonomisk ulikhet, microfinance, ressursfordeling (i samfunn, på verdensbasis, blant generasjoner), velferdspolitikk
*	utviklingsmidler, kolonialisme, globalisation, and development
*	politiske konflikter, genocide
*	sosial bærekraft
*	climate justice
*	likestilling, inkludering, utenforskap
*	gender perspectives and studies
*	lokal og tradisjonell kunnskap
*	minoriteter, kvinner, eldre, personer med nedsatt funksjonsevne, religiøse grupper, urfolk, sårbare grupper, barn, osv. og område som:
 	*	Forskjellsbehandling og diskriminering (økonomisk, sosialt, juridisk), fordømming og utenforskap
 	*	Makt og empowerment
 	*	Representasjon, demokrati og rettigheter
 	*	Språkpolitikk
 	*	Miljø- og klimaendringer

Migrasjon og Ulikhet (beskrevet over), Helse og Ulikhet (beskrevet over)

#### Øvrige tema
*	Klimaendringer, ekstremvær, naturkatastrofe og landbruk/akvakultur i low- and middle income countries. Den WoS søkestrengen er satt opp for å unngå rene klimavitenskap resultater (e.g. Cenozoic climate changes in landx). Cristin versjonen har ingen avgrensning, siden det er vanskeligere i tittelen. 
*	Matsikkerhet, access to food and water


## Combinations

The three main focus areas under GSU have their own strings, as do their overlap areas (e.g. "health and migration" has it's own string where health terms are combined with migration terms). The publications found by the overlap strings contribute to both main focus areas, when publications are counted in the focus areas.

#### TOTAL GSU

```Ceylon =
STR([HEALTH total] + "," + [MIGRATION total] + "," + [INEQUALITY total] + "," + [CC in LMCs])
```
#### TOTAL GSU (nocat)

```Ceylon =
IF CONTAINS([Health - general], "health")
OR CONTAINS([Health & Inequality], "health")
OR CONTAINS([Health & Migration], "health")
OR CONTAINS([Migration], "migration")
OR CONTAINS([Inequality & Migration], "migration")
OR CONTAINS([Health & Migration], "migration")
OR CONTAINS([Inequality], "inequality")
OR CONTAINS([Inequality & Migration], "inequality")
OR CONTAINS([Health & Inequality], "inequality")
OR CONTAINS([CC in LMCs], "climate")
THEN "GSU"
ELSE "non"
END
```

#### HEALTH total

```Ceylon =
IF CONTAINS([Health - general], "health")
OR CONTAINS([Health & Inequality], "health")
OR CONTAINS([Health & Migration], "health")
THEN "health"
ELSE "non"
END
```

#### INEQUALITY total

```Ceylon =
IF CONTAINS([Inequality], "inequality")
OR CONTAINS([Inequality & Migration], "inequality")
OR CONTAINS([Health & Inequality], "inequality")
THEN "inequality"
ELSE "non"
END
```

#### MIGRATION total

```Ceylon =
IF CONTAINS([Migration], "migration")
OR CONTAINS([Inequality & Migration], "migration")
OR CONTAINS([Health & Migration], "migration")
THEN "migration"
ELSE "non"
END
```

## Global health

Should health & ethics be included here (regardless of country?) - if so, in what form (e.g. medical ethics?) - We did not get a clear answer on this. Some medical ethics (related to global health, climate change or in LMCs) will be covered anyway as we combine with NPI field "medisin" and terms like "medical".

Journal "global health" covers global health action etc.

For the climate phrase, the Norwegian terms were tested but there were no results. Nothing for flood or drought either. Could be expanded in a later version. Note that combining climate change with "health" does pick up the occasional biology paper (e.g. health of polar bears, ocean health). 

Use of the general terms "health", "medical", "disease" etc. can introduce noise, but add many more relevant results by picking up all sorts of topics (e.g. medical ethics, communicable diseases, health workers, universal health coverage, mental health, respiratory health, health care etc.)

Specific diseases/health issues added with LMCs (low and middle income countries) in focus: i.e. Added if diseases and major issues primarily in LMCs (e.g. malaria, TB, maternal mortality). Neglected tropical diseases added from the SDG3 search string, based on WHOs list. 

The combination of countries with NPI field "medisin" should compensate for missing specific terms. 

Countries are added from a list over LMCs, SIDS and African countries, but reduced due to capacity problems in Tableau. Countries were removed based on size, expected research focus, and if they were high income. Only 151 publications from the whole of Norway over 2011-2020 mention the missing countries, meaning that not including them in this list should have a small effect. ALL LMCs, SIDS and African countries (minus high income) were included in the WoS search. "Peru" changed to prevent picking up gill amoeba species name containing peru*. "Chad" changed to prevent picking up medical acronym SCHAD.

```Ceylon =
IF		
CONTAINS(LOWER([journal]),	"malaria"	)
OR CONTAINS(LOWER([journal]),	"neglected tropical disease"	)
OR CONTAINS(LOWER([journal]),	"global health"	)
OR CONTAINS(LOWER([journal]),	"global public health"	)
OR CONTAINS(LOWER([journal]),	"african journal of disability"	)
OR CONTAINS(LOWER([journal]),	"disability and the global south"	)
OR CONTAINS(LOWER([journal]),	"tanzania journal of health"	)
OR CONTAINS(LOWER([journal]),	"developing world bioethic"	)

OR CONTAINS(LOWER([result_title]),	"global health"	)
OR CONTAINS(LOWER([result_title]),	"international health"	)
OR CONTAINS(LOWER([result_title]),	"global mental health"	)
OR CONTAINS(LOWER([result_title]),	"global helse"	)
OR CONTAINS(LOWER([result_title]),	"internasjonal helse"	)
THEN 'health'		

ELSEIF((		
CONTAINS(LOWER([result_title]),	"climate change"	)
OR CONTAINS(LOWER([result_title]),	"sustainable development"	)
OR CONTAINS(LOWER([result_title]),	"disaster"	)
OR CONTAINS(LOWER([result_title]),	"tsunami"	)
)		
AND (		
CONTAINS(LOWER([result_title]),	"health"	)
OR CONTAINS(LOWER([result_title]),	"wellbeing"	)
OR CONTAINS(LOWER([result_title]),	"well-being"	)
OR CONTAINS(LOWER([result_title]),	"medical"	)
OR CONTAINS(LOWER([scientific_area_npi]),	"medisin"	)
))		
THEN 'health'		

ELSEIF		
CONTAINS(LOWER([result_title]),	"neglected tropical disease"	)
OR CONTAINS(LOWER([result_title]),	"Buruli ulcer" 	)
OR CONTAINS(LOWER([result_title]),	"leishmaniasis" 	)
OR CONTAINS(LOWER([result_title]),	"foodborne termatod" 	)
OR CONTAINS(LOWER([result_title]),	" yaws" 	)
OR CONTAINS(LOWER([result_title]),	"chagas" 	)
OR CONTAINS(LOWER([result_title]),	"leprosy" 	)
OR CONTAINS(LOWER([result_title]),	"rabies" 	)
OR CONTAINS(LOWER([result_title]),	"human african trypanosomiasis" 	)
OR CONTAINS(LOWER([result_title]),	"dengue" 	)
OR CONTAINS(LOWER([result_title]),	"lymphatic filariasis" 	)
OR CONTAINS(LOWER([result_title]),	"scabies" 	)
OR CONTAINS(LOWER([result_title]),	"sleeping sickness"	)
OR CONTAINS(LOWER([result_title]),	"chikungunya" 	)
OR CONTAINS(LOWER([result_title]),	"mycetoma" 	)
OR CONTAINS(LOWER([result_title]),	"schistosomiasis" 	)
OR CONTAINS(LOWER([result_title]),	"dracunculiasis" 	)
OR CONTAINS(LOWER([result_title]),	"chromoblastomycosis" 	)
OR CONTAINS(LOWER([result_title]),	"soil-transmitted helminthiases" 	)
OR CONTAINS(LOWER([result_title]),	"guinea-worm" 	)
OR CONTAINS(LOWER([result_title]),	"onchocerciasis" 	)
OR CONTAINS(LOWER([result_title]),	"snakebite envenoming" 	)
OR CONTAINS(LOWER([result_title]),	"echinococcosis" 	)
OR CONTAINS(LOWER([result_title]),	"river blindness"	)
OR CONTAINS(LOWER([result_title]),	"taeniasis" 	)
OR CONTAINS(LOWER([result_title]),	"cysticercosis" 	)
OR CONTAINS(LOWER([result_title]),	"trachoma"	)
OR CONTAINS(LOWER([result_title]),	"malaria"	)
OR CONTAINS(LOWER([result_title]),	"cholera"	)
OR CONTAINS(([result_title]),	"HIV"	)
OR CONTAINS(LOWER([result_title]),	"polio"	)
OR CONTAINS(LOWER([result_title]),	"tuberculosis"	)
OR CONTAINS(LOWER([result_title]),	"water-bourne"	)
OR CONTAINS(LOWER([result_title]),	"waterbourne"	)
OR CONTAINS(LOWER([result_title]),	"maternal mortality"	)
OR CONTAINS(LOWER([result_title]),	"child mortality"	)
OR CONTAINS(LOWER([result_title]),	"infant mortality"	)
THEN "health"		

ELSEIF ((		
CONTAINS(LOWER([scientific_area_npi]),	"medisin"	)
OR CONTAINS(LOWER([result_title]),	"health"	)
OR CONTAINS(LOWER([result_title]),	"mortality"	)
OR CONTAINS(LOWER([result_title]),	"medicin"	)
OR CONTAINS(LOWER([result_title]),	"medical"	)
OR CONTAINS(LOWER([result_title]),	"clinic"	)
OR CONTAINS(LOWER([result_title]),	"disease"	)
OR CONTAINS(LOWER([result_title]),	"infection"	)
OR CONTAINS(LOWER([result_title]),	"illness"	)
OR CONTAINS(LOWER([result_title]),	"vaccin"	)
OR CONTAINS(LOWER([result_title]),	"antibiotic"	)
OR CONTAINS(LOWER([result_title]),	"nurses"	)
OR CONTAINS(LOWER([result_title]),	"doctors"	)
OR CONTAINS(LOWER([result_title]),	"physician"	)
OR CONTAINS(LOWER([result_title]),	"dentist"	)
OR CONTAINS(LOWER([result_title]),	"dental"	)
OR CONTAINS(LOWER([result_title]),	"surgery"	)
OR CONTAINS(LOWER([result_title]),	"surgeon"	)
OR CONTAINS(LOWER([result_title]),	"trauma"	)
OR CONTAINS(LOWER([result_title]),	"matern"	)
OR CONTAINS(LOWER([result_title]),	"midwif"	)
OR CONTAINS(LOWER([result_title]),	"childbirth"	)
OR CONTAINS(LOWER([result_title]),	"childbear"	)
OR CONTAINS(LOWER([result_title]),	"breastfeed"	)
OR CONTAINS(LOWER([result_title]),	"birthweight"	)
OR CONTAINS(LOWER([result_title]),	"perinatal"	)
OR CONTAINS(LOWER([result_title]),	"postnatal"	)
OR CONTAINS(LOWER([result_title]),	"enatal "	)
OR CONTAINS(LOWER([result_title]),	"abortion"	)
OR CONTAINS(LOWER([result_title]),	"pregnan"	)
OR CONTAINS(LOWER([result_title]),	"obstetric"	)
OR CONTAINS(LOWER([result_title]),	"sex education"	)
OR CONTAINS(LOWER([result_title]),	"residential care"	)
OR CONTAINS(LOWER([result_title]),	"disab"	)
OR CONTAINS(LOWER([result_title]),	"impairment"	)
OR CONTAINS(LOWER([result_title]),	"child development"	)
OR CONTAINS(LOWER([result_title]),	"cognative"	)
OR CONTAINS(LOWER([result_title]),	"nutrition"	)
OR CONTAINS(LOWER([result_title]),	"konzo"	)
OR CONTAINS(LOWER([result_title]),	"marasmus"	)
OR CONTAINS(LOWER([result_title]),	"kwashiorkor"	)
OR CONTAINS(LOWER([result_title]),	"vitamin"	)
OR CONTAINS(LOWER([result_title]),	"micronutrient"	)
OR CONTAINS(LOWER([result_title]),	"diet"	)
OR CONTAINS(LOWER([result_title]),	"risk behavi"	)
OR CONTAINS(LOWER([result_title]),	"therap"	)
OR CONTAINS(LOWER([result_title]),	"counselling"	)
OR CONTAINS(LOWER([result_title]),	"psycholog"	)
OR CONTAINS(LOWER([result_title]),	"psychiat"	)
OR CONTAINS(LOWER([result_title]),	"wellbeing"	)
OR CONTAINS(LOWER([result_title]),	"well-being"	)
OR CONTAINS(LOWER([result_title]),	"suicide"	)
OR CONTAINS(LOWER([result_title]),	"self-harm"	)
OR CONTAINS(LOWER([result_title]),	"orthopedic"	)
OR CONTAINS(LOWER([result_title]),	"cancer"	)
OR CONTAINS(LOWER([result_title]),	"asthma"	)
OR CONTAINS(LOWER([result_title]),	"diabetes"	)
OR CONTAINS(LOWER([result_title]),	"dust exposure"	)
OR CONTAINS(LOWER([result_title]),	"pneumonia"	)
OR CONTAINS(LOWER([result_title]),	"diarrhea"	)
OR CONTAINS(LOWER([result_title]),	"coronavirus"	)
OR CONTAINS(LOWER([result_title]),	"covid"	)
OR CONTAINS(LOWER([result_title]),	"tobacco"	)
OR CONTAINS(LOWER([result_title]),	"tombak"	)
OR CONTAINS(LOWER([result_title]),	"injuries"	)
OR CONTAINS(LOWER([result_title]),	"accident"	)
OR CONTAINS(LOWER([result_title]),	"mercury"	)
OR CONTAINS(LOWER([result_title]),	"toxi"	)
OR CONTAINS(LOWER([result_title]),	"alcoholism"	)
OR CONTAINS(LOWER([result_title]),	"binge drink"	)
OR CONTAINS(LOWER([result_title]),	"addict"	)
OR CONTAINS(LOWER([journal]),	"parasites and vectors"	)
)		
AND (		
CONTAINS(LOWER([result_title]),	"least developed count" 	)
OR CONTAINS(LOWER([result_title]),	"developing count" 	)
OR CONTAINS(LOWER([result_title]),	"developing state" 	)
OR CONTAINS(LOWER([result_title]),	"low income countr" 	)
OR CONTAINS(LOWER([result_title]),	"middle income countr" 	)
OR CONTAINS(LOWER([result_title]),	"low-income countr" 	)
OR CONTAINS(LOWER([result_title]),	"middle-income countr" 	)
OR CONTAINS(LOWER([result_title]),	"afghanistan"	)
OR CONTAINS(LOWER([result_title]),	"angola" 	)
OR CONTAINS(LOWER([result_title]),	"bangladesh" 	)
OR CONTAINS(LOWER([result_title]),	"bhutan" 	)
OR CONTAINS(LOWER([result_title]),	"burkina faso" 	)
OR CONTAINS(LOWER([result_title]),	"burundi" 	)
OR CONTAINS(LOWER([result_title]),	"cambodia" 	)
OR CONTAINS(LOWER([result_title]),	"congo" 	)
OR CONTAINS(LOWER([result_title]),	"cuba" 	)
OR CONTAINS(LOWER([result_title]),	"eritrea" 	)
OR CONTAINS(LOWER([result_title]),	"ethiopia" 	)
OR CONTAINS(LOWER([result_title]),	"gambia" 	)
OR CONTAINS(LOWER([result_title]),	"haiti" 	)
OR CONTAINS(LOWER([result_title]),	"jamaica" 	)
OR CONTAINS(LOWER([result_title]),	"liberia" 	)
OR CONTAINS(LOWER([result_title]),	"madagascar" 	)
OR CONTAINS(LOWER([result_title]),	"malawi" 	)
OR CONTAINS(LOWER([result_title]),	"maldives" 	)
OR CONTAINS(LOWER([result_title]),	" mali " 	)
OR CONTAINS(LOWER([result_title]),	"mauritius" 	)
OR CONTAINS(LOWER([result_title]),	"mozambique" 	)
OR CONTAINS(LOWER([result_title]),	"myanmar" 	)
OR CONTAINS(LOWER([result_title]),	"nepal" 	)
OR CONTAINS(LOWER([result_title]),	"papua new guinea" 	)
OR CONTAINS(LOWER([result_title]),	"rwanda" 	)
OR CONTAINS(LOWER([result_title]),	"la reunion" 	)
OR CONTAINS(LOWER([result_title]),	"samoa" 	)
OR CONTAINS(LOWER([result_title]),	"sierra leone" 	)
OR CONTAINS(LOWER([result_title]),	"somalia" 	)
OR CONTAINS(LOWER([result_title]),	"sudan" 	)
OR CONTAINS(LOWER([result_title]),	"tanzania" 	)
OR CONTAINS(LOWER([result_title]),	"timor leste" 	)
OR CONTAINS(LOWER([result_title]),	"timor-leste" 	)
OR CONTAINS(LOWER([result_title]),	"tuvalu" 	)
OR CONTAINS(LOWER([result_title]),	"uganda" 	)
OR CONTAINS(LOWER([result_title]),	"yemen" 	)
OR CONTAINS(LOWER([result_title]),	"zambia" 	)
OR CONTAINS(LOWER([result_title]),	"africa" 	)
OR CONTAINS(LOWER([result_title]),	"nigeria"	)
OR CONTAINS(LOWER([result_title]),	"egypt"	)
OR CONTAINS(LOWER([result_title]),	"kenya"	)
OR CONTAINS(LOWER([result_title]),	"algeria"	)
OR CONTAINS(LOWER([result_title]),	"morocco"	)
OR CONTAINS(LOWER([result_title]),	"ghana"	)
OR CONTAINS(LOWER([result_title]),	"cameroon"	)
OR CONTAINS(LOWER([result_title]),	"zimbabwe"	)
OR CONTAINS(LOWER([result_title]),	"tunisia"	)
OR CONTAINS(LOWER([result_title]),	"libya"	)
OR CONTAINS(LOWER([result_title]),	"botswana"	)
OR CONTAINS(LOWER([result_title]),	"equatorial guinea"	)
OR CONTAINS(LOWER([result_title]),	"albania"	)
OR CONTAINS(LOWER([result_title]),	"argentina"	)
OR CONTAINS(LOWER([result_title]),	"armenia"	)
OR CONTAINS(LOWER([result_title]),	"azerbaijan"	)
OR CONTAINS(LOWER([result_title]),	"belarus"	)
OR CONTAINS(LOWER([result_title]),	"bolivia"	)
OR CONTAINS(LOWER([result_title]),	"bosnia"	)
OR CONTAINS(LOWER([result_title]),	"brazil"	)
OR CONTAINS(LOWER([result_title]),	"bulgaria"	)
OR CONTAINS(LOWER([result_title]),	"china"	)
OR CONTAINS(LOWER([result_title]),	"colombia"	)
OR CONTAINS(LOWER([result_title]),	"costa rica"	)
OR CONTAINS(LOWER([result_title]),	"ecuador"	)
OR CONTAINS(LOWER([result_title]),	"el salvador"	)
OR CONTAINS(LOWER([result_title]),	"guatemala"	)
OR CONTAINS(LOWER([result_title]),	"honduras"	)
OR CONTAINS(LOWER([result_title]),	"india"	)
OR CONTAINS(LOWER([result_title]),	"indonesia"	)
OR CONTAINS(LOWER([result_title]),	"iran"	)
OR CONTAINS(LOWER([result_title]),	"iraq"	)
OR CONTAINS(LOWER([result_title]),	"jordan"	)
OR CONTAINS(LOWER([result_title]),	"kazakhstan"	)
OR CONTAINS(LOWER([result_title]),	"kosovo"	)
OR CONTAINS(LOWER([result_title]),	"kyrgyz"	)
OR CONTAINS(LOWER([result_title]),	"lebanon"	)
OR CONTAINS(LOWER([result_title]),	"malaysia"	)
OR CONTAINS(LOWER([result_title]),	"mexico"	)
OR CONTAINS(LOWER([result_title]),	"micronesia"	)
OR CONTAINS(LOWER([result_title]),	"moldova"	)
OR CONTAINS(LOWER([result_title]),	"mongolia"	)
OR CONTAINS(LOWER([result_title]),	"montenegro"	)
OR CONTAINS(LOWER([result_title]),	"nicaragua"	)
OR CONTAINS(LOWER([result_title]),	"macedonia"	)
OR CONTAINS(LOWER([result_title]),	"pakistan"	)
OR CONTAINS(LOWER([result_title]),	"paraguay"	)
OR CONTAINS(LOWER([result_title]),	"phillipines"	)
OR CONTAINS(([result_title]),	"Peru"	)
OR CONTAINS(LOWER([result_title]),	"peruvian"	)
OR CONTAINS(LOWER([result_title]),	"romania"	)
OR CONTAINS(LOWER([result_title]),	"russia"	)
OR CONTAINS(LOWER([result_title]),	"serbia"	)
OR CONTAINS(LOWER([result_title]),	"sri lanka"	)
OR CONTAINS(LOWER([result_title]),	"syria"	)
OR CONTAINS(LOWER([result_title]),	"tajikistan"	)
OR CONTAINS(LOWER([result_title]),	"thailand"	)
OR CONTAINS(LOWER([result_title]),	"turkey"	)
OR CONTAINS(LOWER([result_title]),	"turkmenistan"	)
OR CONTAINS(LOWER([result_title]),	"ukraine"	)
OR CONTAINS(LOWER([result_title]),	"venezuela"	)
OR CONTAINS(LOWER([result_title]),	"vietnam"	)
OR CONTAINS(LOWER([result_title]),	"west bank"	)
OR CONTAINS(LOWER([result_title]),	" gaza"	)
))		
THEN "health"

ELSEIF(		
CONTAINS(LOWER([scientific_area_npi]),	"medisin"	)
AND (		
CONTAINS(LOWER([result_title]),	"antigua" 	)
OR CONTAINS(LOWER([result_title]),	"bahrain" 	)
OR CONTAINS(LOWER([result_title]),	"barbados" 	)
OR CONTAINS(LOWER([result_title]),	"belize" 	)
OR CONTAINS(LOWER([result_title]),	"benin" 	)
OR CONTAINS(LOWER([result_title]),	"bermuda" 	)
OR CONTAINS(LOWER([result_title]),	"cabo verde" 	)
OR CONTAINS(([result_title]),	"Chad" 	)
OR CONTAINS(LOWER([result_title]),	"marianas" 	)
OR CONTAINS(LOWER([result_title]),	"comoros" 	)
OR CONTAINS(LOWER([result_title]),	"djibouti" 	)
OR CONTAINS(LOWER([result_title]),	"dominica" 	)
OR CONTAINS(LOWER([result_title]),	"micronesia" 	)
OR CONTAINS(LOWER([result_title]),	"fiji" 	)
OR CONTAINS(LOWER([result_title]),	"french polynesia" 	)
OR CONTAINS(LOWER([result_title]),	"grenada" 	)
OR CONTAINS(LOWER([result_title]),	"guadeloupe" 	)
OR CONTAINS(LOWER([result_title]),	"guyana" 	)
OR CONTAINS(LOWER([result_title]),	"kiribati" 	)
OR CONTAINS(LOWER([result_title]),	" laos " 	)
OR CONTAINS(LOWER([result_title]),	"lesotho" 	)
OR CONTAINS(LOWER([result_title]),	"marshall islands" 	)
OR CONTAINS(LOWER([result_title]),	"martinique" 	)
OR CONTAINS(LOWER([result_title]),	"mauritania" 	)
OR CONTAINS(LOWER([result_title]),	"montserrat" 	)
OR CONTAINS(LOWER([result_title]),	"nauru" 	)
OR CONTAINS(LOWER([result_title]),	"new caledonia" 	)
OR CONTAINS(LOWER([result_title]),	" niger " 	)
OR CONTAINS(LOWER([result_title]),	" niue " 	)
OR CONTAINS(LOWER([result_title]),	"saint lucia" 	)
OR CONTAINS(LOWER([result_title]),	"grenadines" 	)
OR CONTAINS(LOWER([result_title]),	"sao tome" 	)
OR CONTAINS(LOWER([result_title]),	"senegal" 	)
OR CONTAINS(LOWER([result_title]),	"solomon islands" 	)
OR CONTAINS(LOWER([result_title]),	"suriname" 	)
OR CONTAINS(LOWER([result_title]),	" togo " 	)
OR CONTAINS(LOWER([result_title]),	"tonga" 	)
OR CONTAINS(LOWER([result_title]),	"vanuatu" 	)
OR CONTAINS(LOWER([result_title]),	"ivory coast"	)
OR CONTAINS(LOWER([result_title]),	"gabon"	)
OR CONTAINS(LOWER([result_title]),	"eswatini"	)
OR CONTAINS(LOWER([result_title]),	"cape verde"	)
OR CONTAINS(LOWER([result_title]),	"western sahara"	)
OR CONTAINS(LOWER([result_title]),	"mayotte"	)
))		
THEN "health"

ELSE "non"
END
```

## Inequality

It was unclear from consultations if "democracy" itself should be included - in the end I included it as it was related to some terms given in consultations (e.g. voting rights). Traditional knowledge included after consultation. NPI field "utviklingsstudier" is included in its entirity after consultation. 

Note terms such as "equality" will also cover "inequality" due to truncation. "minoritet" dekker minoriteter, minoritetsbarn/befolkning/språk/kvinner/politikk osv. In English, "minority" is used in other contexts in a much more general way, and is combined with other terms (vs. included alone in Norwegian). The same is true for "inclusion" and "exclusion" vs. "inkludering" and "utenforskap". 

Several NOT terms had to be included due to widespread use of "inequalities" in mathematics, including exclusion of all publications in NPI fields mathematics and physics.

Climate and environmental justice is included, as is climate change with specific groups of people/religions/class/globalisation. 

```Ceylon =
IF		
CONTAINS(LOWER([journal]),	"equality, diversity and inclusion"	)
OR CONTAINS(LOWER([journal]),	"journal of human rights"	)
OR CONTAINS(LOWER([journal]),	"human rights law review"	)
OR CONTAINS(LOWER([journal]),	"human rights quarterly"	)
OR CONTAINS(LOWER([journal]),	"human rights review"	)
OR CONTAINS(LOWER([journal]),	"children's rights"	)
OR CONTAINS(LOWER([journal]),	"economic inequality"	)
OR CONTAINS(LOWER([journal]),	"journal of peasant studies"	)
OR CONTAINS(LOWER([journal]),	"review of development economics"	)
OR CONTAINS(LOWER([journal]),	"world bank research observer"	)
OR CONTAINS(LOWER([journal]),	"journal of global south studies"	)
OR CONTAINS(LOWER([journal]),	"journal of homelessness"	)
OR CONTAINS(LOWER([journal]),	"children and poverty"	)
OR CONTAINS(LOWER([journal]),	"journal of poverty"	)
OR CONTAINS(LOWER([journal]),	"povery & public policy"	)
OR CONTAINS(LOWER([journal]),	"global slavery"	)
OR CONTAINS(LOWER([journal]),	"women's studies"	)
OR CONTAINS(LOWER([journal]),	"masculinity studies"	)
OR CONTAINS(LOWER([journal]),	"kjønnsforskning"	)
OR CONTAINS(LOWER([journal]),	"gender"	)

OR CONTAINS(LOWER([scientific_field_npi]),	"utviklings"	)
THEN 'inequality'		

ELSEIF((		
CONTAINS(LOWER([result_title]),	"equalit"	)
OR CONTAINS(LOWER([result_title]),	"equity"	)
OR CONTAINS(LOWER([result_title]),	"marginali"	)
OR CONTAINS(LOWER([result_title]),	"disparities"	)
OR CONTAINS(LOWER([result_title_anthology]),	"equalit"	)
OR CONTAINS(LOWER([result_title_anthology]),	"equity"	)
OR CONTAINS(LOWER([result_title_anthology]),	"marginali"	)
)		
AND NOT (		
CONTAINS(([scientific_field_npi]),	"Matematikk"	)
OR CONTAINS(([scientific_field_npi]),	"Fysikk"	)
OR CONTAINS(LOWER([result_title]),	"hull inequalities"	)
OR CONTAINS(LOWER([result_title]),	"gaussian"	)
OR CONTAINS(LOWER([result_title]),	"distributional"	)
OR CONTAINS(LOWER([result_title]),	"triangle inequalit"	)
))		
THEN 'inequality'		


ELSEIF		
CONTAINS(LOWER([result_title]),	"egalitar"	)
OR CONTAINS(LOWER([result_title]),	"poverty"	)
OR CONTAINS(LOWER([result_title]),	"microfinance"	)
OR CONTAINS(LOWER([result_title]),	"microcredit"	)
OR CONTAINS(LOWER([result_title]),	"financial inclusion"	)
OR CONTAINS(LOWER([result_title]),	"welfare system"	)
OR CONTAINS(LOWER([result_title]),	"social policy"	)
OR CONTAINS(LOWER([result_title]),	"beggar"	)
OR CONTAINS(LOWER([result_title]),	"begging"	)
OR CONTAINS(LOWER([result_title]),	"homeless"	)
OR CONTAINS(LOWER([result_title]),	"slaver"	)
OR CONTAINS(LOWER([result_title]),	"slaves"	)
OR CONTAINS(LOWER([result_title]),	"disadvantaged"	)
OR CONTAINS(LOWER([result_title]),	"the vulnerable"	)
OR CONTAINS(LOWER([result_title]),	"social sustainab"	)
OR CONTAINS(LOWER([result_title]),	"global south"	)
OR CONTAINS(LOWER([result_title]),	"post-coloni"	)
OR CONTAINS(LOWER([result_title]),	"postcoloni"	)
OR CONTAINS(LOWER([result_title]),	"decoloni"	)
OR CONTAINS(LOWER([result_title]),	"genocide"	)
OR CONTAINS(LOWER([result_title]),	"epistemicide"	)
OR CONTAINS(LOWER([result_title]),	" riot"	)
OR CONTAINS(LOWER([result_title]),	"uprising"	)
OR CONTAINS(LOWER([result_title]),	"insurrection"	)
OR CONTAINS(LOWER([result_title]),	"political protest"	)
OR CONTAINS(LOWER([result_title]),	"political conflict"	)
OR CONTAINS(LOWER([result_title]),	"social justice"	)
OR CONTAINS(LOWER([result_title]),	"development assistance"	)
OR CONTAINS(LOWER([result_title]),	"development aid"	)
OR CONTAINS(LOWER([result_title]),	"racism"	)
OR CONTAINS(LOWER([result_title]),	"racial"	)
OR CONTAINS(LOWER([result_title]),	"ageism"	)
OR CONTAINS(LOWER([result_title]),	"sexism"	)
OR CONTAINS(LOWER([result_title]),	"gendered"	)
OR CONTAINS(LOWER([result_title]),	"homophob"	)
OR CONTAINS(LOWER([result_title]),	"queer"	)
OR CONTAINS(LOWER([result_title]),	"gender perspective"	)
OR CONTAINS(LOWER([result_title]),	"minorities"	)
OR CONTAINS(LOWER([result_title]),	"minority group"	)
OR CONTAINS(LOWER([result_title]),	"minority language"	)
OR CONTAINS(LOWER([result_title]),	"minority stress"	)
OR CONTAINS(LOWER([result_title]),	"otherness"	)
OR CONTAINS(LOWER([result_title]),	" othering"	)
OR CONTAINS(LOWER([result_title]),	"intersectional"	)
OR CONTAINS(LOWER([result_title]),	"discrimination"	)
OR CONTAINS(LOWER([result_title]),	"stereotyp"	)
OR CONTAINS(LOWER([result_title]),	"apartheid"	)
OR (CONTAINS(LOWER([result_title])," caste ") AND NOT CONTAINS(LOWER([result_title]),"bee"))		


OR CONTAINS(LOWER([result_title]),	"fattigdom"	)
OR CONTAINS(LOWER([result_title]),	"slavehandel"	)
OR CONTAINS(LOWER([result_title]),	"sosialt bærekraft"	)
OR CONTAINS(LOWER([result_title]),	"sosial bærekraft"	)
OR CONTAINS(LOWER([result_title]),	"rasisme"	)
OR CONTAINS(LOWER([result_title]),	"homofil"	)
OR CONTAINS(LOWER([result_title]),	"skeive"	)
OR CONTAINS(LOWER([result_title]),	"minoritet"	)
OR CONTAINS(LOWER([result_title]),	"forskjellsbehan"	)
OR CONTAINS(LOWER([result_title]),	"likestilling"	)
OR CONTAINS(LOWER([result_title]),	"inkludering"	)
OR CONTAINS(LOWER([result_title]),	"utenforskap"	)

THEN "inequality"		

ELSEIF (( 		
CONTAINS(LOWER([result_title]),	"minority"	)
OR CONTAINS(LOWER([result_title]),	"democracy"	)
OR CONTAINS(LOWER([result_title]),	"governance"	)
OR CONTAINS(LOWER([result_title]),	"representation "	)
OR CONTAINS(LOWER([result_title]),	"hierarch "	)
OR CONTAINS(LOWER([result_title]),	"empowerment"	)
OR CONTAINS(LOWER([result_title]),	"inclusion"	)
OR CONTAINS(LOWER([result_title]),	"exclusion"	)
OR CONTAINS(LOWER([result_title]),	"inclusive"	)
OR CONTAINS(LOWER([result_title]),	"exclusive "	)
OR CONTAINS(LOWER([result_title]),	"excluding"	)
OR CONTAINS(LOWER([result_title]),	"belonging"	)
OR CONTAINS(LOWER([result_title]),	"livelihood"	)
OR CONTAINS(LOWER([result_title]),	"language polic"	)
OR CONTAINS(LOWER([result_title]),	"bilingual"	)
OR CONTAINS(LOWER([result_title]),	"sustainab"	)
OR CONTAINS(LOWER([result_title]),	"climate chang"	)
OR CONTAINS(LOWER([result_title]),	"climatic chang"	)
OR CONTAINS(LOWER([result_title]),	"environmental chang"	)
)		
AND (		
CONTAINS(LOWER([result_title]),	"ethnic"	)
OR CONTAINS(LOWER([result_title]),	"indigenous"	)
OR CONTAINS(LOWER([result_title]),	"autochthonous"	)
OR CONTAINS(LOWER([result_title]),	"sami"	)
OR CONTAINS(LOWER([result_title]),	"sámi "	)
OR CONTAINS(LOWER([result_title]),	"sápmi"	)
OR CONTAINS(LOWER([result_title]),	"tribal"	)
OR CONTAINS(LOWER([result_title]),	"women"	)
OR CONTAINS(LOWER([result_title]),	"girls"	)
OR CONTAINS(LOWER([result_title]),	"gender"	)
OR CONTAINS(LOWER([result_title]),	"disab"	)
OR CONTAINS(LOWER([result_title]),	"multicultur"	)
OR CONTAINS(LOWER([result_title]),	"welfare"	)
OR CONTAINS(LOWER([result_title]),	"social class"	)
OR CONTAINS(LOWER([result_title]),	"globalization"	)
OR CONTAINS(LOWER([result_title]),	"globalisation"	)
OR CONTAINS(LOWER([result_title]),	"neoliberal"	)
OR CONTAINS(LOWER([result_title]),	"capitalism"	)
OR CONTAINS(LOWER([result_title]),	"religio"	)
OR CONTAINS(LOWER([result_title]),	"islam"	)
OR CONTAINS(LOWER([result_title]),	"muslim"	)
OR CONTAINS(LOWER([result_title]),	"christian"	)
OR CONTAINS(LOWER([result_title]),	"jewish"	)
OR CONTAINS(LOWER([result_title]),	"hindu"	)
OR CONTAINS(LOWER([result_title]),	"sikh"	)
OR CONTAINS(LOWER([result_title]),	"buddhis"	)
))		
THEN 'inequality'		

ELSEIF (( 		
CONTAINS(LOWER([result_title]),	"intergeneration"	)
)		
AND (		
CONTAINS(LOWER([result_title]),	"resouces"	)
OR CONTAINS(LOWER([result_title]),	"wealth"	)
OR CONTAINS(LOWER([result_title]),	"econom"	)
OR CONTAINS(LOWER([result_title]),	"sustainab"	)
OR CONTAINS(LOWER([result_title]),	"mobility"	)
OR CONTAINS(LOWER([result_title]),	"education"	)
OR CONTAINS(LOWER([result_title]),	"welfare"	)
OR CONTAINS(LOWER([result_title]),	"gender"	)
))		
THEN 'inequality'		

ELSEIF (( 		
CONTAINS(LOWER([result_title]),	"globalization"	)
OR CONTAINS(LOWER([result_title]),	"globalisation"	)
OR CONTAINS(LOWER([result_title]),	"neoliberal"	)
OR CONTAINS(([result_title]),	"BRICS"	)
OR CONTAINS(LOWER([result_title]),	"neoliberal"	)
OR CONTAINS(LOWER([result_title]),	"least-developed countr"	)
OR CONTAINS(LOWER([result_title]),	"developing countr"	)
OR CONTAINS(LOWER([result_title]),	"low income countr"	)
OR CONTAINS(LOWER([result_title]),	"low-income countr"	)
OR CONTAINS(LOWER([result_title]),	"poor countr"	)
)		
AND (		
CONTAINS(LOWER([result_title]),	"development"	)
))		
THEN 'inequality'

ELSEIF ((
CONTAINS(LOWER([result_title]),	"local"	)
OR CONTAINS(LOWER([result_title]),	"traditional"	)
OR CONTAINS(LOWER([result_title]),	"community-based"	)
OR CONTAINS(LOWER([result_title]),	"indigenous"	)
)
AND (		
CONTAINS(LOWER([result_title]),	"knowledge"	)
))		
THEN 'inequality'			

ELSEIF 		
CONTAINS(LOWER([result_title]),	"human right"	)
OR CONTAINS(LOWER([result_title_anthology]),	"human right"	)
OR CONTAINS(LOWER([result_title]),	"political rights"	)
OR CONTAINS(LOWER([result_title]),	"civil right"	)
OR CONTAINS(LOWER([result_title]),	"voting rights"	)
OR CONTAINS(LOWER([result_title]),	"sexual rights"	)
OR CONTAINS(LOWER([result_title]),	"land rights"	)
OR CONTAINS(LOWER([result_title]),	"land tenure"	)
OR CONTAINS(LOWER([result_title]),	"constitutional rights"	)
OR CONTAINS(LOWER([result_title]),	"social rights"	)
THEN 'inequality'		

ELSEIF ((		
CONTAINS(LOWER([result_title]),	"women"	)
OR CONTAINS(LOWER([result_title]),	"girls"	)
OR CONTAINS(LOWER([result_title]),	"child"	)
OR CONTAINS(LOWER([result_title]),	"gender"	)
OR CONTAINS(LOWER([result_title]),	"elderly" 	)
OR CONTAINS(LOWER([result_title]),	"disab" 	)
OR CONTAINS(LOWER([result_title]),	"religio"	)
OR CONTAINS(LOWER([result_title]),	"indigenous"	)
OR CONTAINS(LOWER([result_title]),	"autochthonous"	)
OR CONTAINS(LOWER([result_title]),	"sami "	)
OR CONTAINS(LOWER([result_title]),	"sámi "	)
OR CONTAINS(LOWER([result_title]),	"sápmi"	)
OR CONTAINS(LOWER([result_title]),	"tribal"	)
OR CONTAINS(LOWER([result_title]),	"ethnic"	)
OR CONTAINS(LOWER([result_title]),	"minorit"	)
OR CONTAINS(LOWER([result_title]),	"multicultur"	)
OR CONTAINS(LOWER([result_title]),	"workers" 	)
OR CONTAINS(LOWER([result_title]),	"elector" 	)
OR CONTAINS(LOWER([result_title]),	"gay"	)
OR CONTAINS(LOWER([result_title]),	"lesbian"	)
OR CONTAINS(LOWER([result_title]),	"bisexual"	)
OR CONTAINS(LOWER([result_title]),	"transgender"	)
OR CONTAINS(LOWER([result_title]),	"LGBT"	)
)		
AND (		
CONTAINS(LOWER([result_title]),	"right"	)
OR CONTAINS(LOWER([result_title]),	"justice"	)
OR CONTAINS(LOWER([result_title]),	"legislat"	)
OR CONTAINS(LOWER([result_title]),	"legal"	)
OR CONTAINS(LOWER([result_title]),	"freedom"	)
OR CONTAINS(LOWER([result_title]),	"security"	)
OR CONTAINS(LOWER([result_title]),	"power balance"	)
OR CONTAINS(LOWER([result_title]),	"empower"	)
OR CONTAINS(LOWER([result_title]),	"political power"	)
OR CONTAINS(LOWER([result_title]),	"quota"	)
OR CONTAINS(LOWER([result_title]),	"sharia"	)
OR CONTAINS(LOWER([result_title]),	"traditional law"	)
))		
THEN 'inequality'		


ELSEIF 		
CONTAINS(LOWER([result_title]),	"menneskerett"	)
OR CONTAINS(LOWER([result_title]),	"rettferdig"	)
OR CONTAINS(LOWER([result_title]),	"stemmerett"	)
OR CONTAINS(LOWER([result_title]),	"sexuelle rettigheter"	)
OR CONTAINS(LOWER([result_title]),	"politiske rettigheter"	)
OR CONTAINS(LOWER([result_title]),	"konstitusjonelle rettigheter"	)
THEN 'inequality'		

ELSEIF ((		
CONTAINS(LOWER([result_title]),	"kvinne"	)
OR CONTAINS(LOWER([result_title]),	"barn"	)
OR CONTAINS(LOWER([result_title]),	"kjønn"	)
OR CONTAINS(LOWER([result_title]),	"funksjonshemm" 	)
OR CONTAINS(LOWER([result_title]),	" eldre"	)
OR CONTAINS(LOWER([result_title]),	"religio"	)
OR CONTAINS(LOWER([result_title]),	"urfolk"	)
OR CONTAINS(LOWER([result_title]),	"sami "	)
OR CONTAINS(LOWER([result_title]),	"sámi "	)
OR CONTAINS(LOWER([result_title]),	"sápmi"	)
OR CONTAINS(LOWER([result_title]),	"etnisk"	)
)		
AND (		
CONTAINS(LOWER([result_title]),	"rettigheter"	)
OR CONTAINS(LOWER([result_title]),	"politikk"	)
OR CONTAINS(LOWER([result_title]),	"represent"	)
OR CONTAINS(LOWER([result_title]),	"kvote"	)
OR CONTAINS(LOWER([result_title]),	"frihet"	)
OR CONTAINS(LOWER([result_title]),	"sikkerhet"	)
OR CONTAINS(LOWER([result_title]),	"makt"	)
))		
THEN 'inequality'		

ELSEIF		
CONTAINS(LOWER([result_title_anthology]),	"egalitar"	)
OR CONTAINS(LOWER([result_title_anthology]),	"poverty"	)
OR CONTAINS(LOWER([result_title_anthology]),	"microfinance"	)
OR CONTAINS(LOWER([result_title_anthology]),	"microcredit"	)
OR CONTAINS(LOWER([result_title_anthology]),	"welfare system"	)
OR CONTAINS(LOWER([result_title_anthology]),	"social policy"	)
OR CONTAINS(LOWER([result_title_anthology]),	"financial inclusion"	)
OR CONTAINS(LOWER([result_title_anthology]),	"beggar"	)
OR CONTAINS(LOWER([result_title_anthology]),	"begging"	)
OR CONTAINS(LOWER([result_title_anthology]),	"homeless"	)
OR CONTAINS(LOWER([result_title_anthology]),	"slaver"	)
OR CONTAINS(LOWER([result_title_anthology]),	"slaves"	)
OR CONTAINS(LOWER([result_title_anthology]),	"disadvantaged"	)
OR CONTAINS(LOWER([result_title_anthology]),	"the vulnerable"	)
OR CONTAINS(LOWER([result_title_anthology]),	"social sustainab"	)
OR CONTAINS(LOWER([result_title_anthology]),	"global south"	)
OR CONTAINS(LOWER([result_title_anthology]),	"post-coloni"	)
OR CONTAINS(LOWER([result_title_anthology]),	"postcoloni"	)
OR CONTAINS(LOWER([result_title_anthology]),	"decoloni"	)
OR CONTAINS(LOWER([result_title_anthology]),	"genocide"	)
OR CONTAINS(LOWER([result_title_anthology]),	"epistemicide"	)
OR CONTAINS(LOWER([result_title_anthology]),	" riot"	)
OR CONTAINS(LOWER([result_title_anthology]),	"uprising"	)
OR CONTAINS(LOWER([result_title_anthology]),	"insurrection"	)
OR CONTAINS(LOWER([result_title_anthology]),	"political protest"	)
OR CONTAINS(LOWER([result_title_anthology]),	"political conflict"	)
OR CONTAINS(LOWER([result_title_anthology]),	"social justice"	)
OR CONTAINS(LOWER([result_title_anthology]),	"development assistance"	)
OR CONTAINS(LOWER([result_title_anthology]),	"development aid"	)
OR CONTAINS(LOWER([result_title_anthology]),	"racism"	)
OR CONTAINS(LOWER([result_title_anthology]),	"racial"	)
OR CONTAINS(LOWER([result_title_anthology]),	"ageism"	)
OR CONTAINS(LOWER([result_title_anthology]),	"sexism"	)
OR CONTAINS(LOWER([result_title_anthology]),	"gendered"	)
OR CONTAINS(LOWER([result_title_anthology]),	"homophob"	)
OR CONTAINS(LOWER([result_title_anthology]),	"queer"	)
OR CONTAINS(LOWER([result_title_anthology]),	"gender perspective"	)
OR CONTAINS(LOWER([result_title_anthology]),	"minorities"	)
OR CONTAINS(LOWER([result_title_anthology]),	"minority group"	)
OR CONTAINS(LOWER([result_title_anthology]),	"minority language"	)
OR CONTAINS(LOWER([result_title_anthology]),	"minority stress"	)
OR CONTAINS(LOWER([result_title_anthology]),	"otherness"	)
OR CONTAINS(LOWER([result_title_anthology]),	" othering"	)
OR CONTAINS(LOWER([result_title_anthology]),	"intersectional"	)
OR CONTAINS(LOWER([result_title_anthology]),	"discrimination"	)
OR CONTAINS(LOWER([result_title_anthology]),	"stereotyp"	)
OR CONTAINS(LOWER([result_title_anthology]),	"apartheid"	)


OR CONTAINS(LOWER([result_title_anthology]),	"fattigdom"	)
OR CONTAINS(LOWER([result_title_anthology]),	"slavehandel"	)
OR CONTAINS(LOWER([result_title_anthology]),	"sosialt bærekraft"	)
OR CONTAINS(LOWER([result_title_anthology]),	"sosial bærekraft"	)
OR CONTAINS(LOWER([result_title_anthology]),	"rasisme"	)
OR CONTAINS(LOWER([result_title_anthology]),	"homofil"	)
OR CONTAINS(LOWER([result_title_anthology]),	"skeive"	)
OR CONTAINS(LOWER([result_title_anthology]),	"minoritet"	)
OR CONTAINS(LOWER([result_title_anthology]),	"forskjellsbehan"	)
OR CONTAINS(LOWER([result_title_anthology]),	"likestilling"	)
OR CONTAINS(LOWER([result_title_anthology]),	"inkludering"	)
OR CONTAINS(LOWER([result_title_anthology]),	"utenforskap"	)

THEN "inequality"		

ELSEIF (( 		
CONTAINS(LOWER([result_title_anthology]),	"minority"	)
OR CONTAINS(LOWER([result_title_anthology]),	"democracy"	)
OR CONTAINS(LOWER([result_title_anthology]),	"governance"	)
OR CONTAINS(LOWER([result_title_anthology]),	"representation "	)
OR CONTAINS(LOWER([result_title_anthology]),	"hierarch "	)
OR CONTAINS(LOWER([result_title_anthology]),	"empowerment"	)
OR CONTAINS(LOWER([result_title_anthology]),	"inclusion"	)
OR CONTAINS(LOWER([result_title_anthology]),	"exclusion"	)
OR CONTAINS(LOWER([result_title_anthology]),	"inclusive"	)
OR CONTAINS(LOWER([result_title_anthology]),	"exclusive "	)
OR CONTAINS(LOWER([result_title_anthology]),	"excluding"	)
OR CONTAINS(LOWER([result_title_anthology]),	"belonging"	)
OR CONTAINS(LOWER([result_title_anthology]),	"livelihood"	)
OR CONTAINS(LOWER([result_title_anthology]),	"language polic"	)
OR CONTAINS(LOWER([result_title_anthology]),	"bilingual"	)
OR CONTAINS(LOWER([result_title_anthology]),	"sustainab"	)
OR CONTAINS(LOWER([result_title_anthology]),	"climate chang"	)
OR CONTAINS(LOWER([result_title_anthology]),	"climatic chang"	)
OR CONTAINS(LOWER([result_title_anthology]),	"environmental chang"	)
)		
AND (		
CONTAINS(LOWER([result_title_anthology]),	"ethnic"	)
OR CONTAINS(LOWER([result_title_anthology]),	"indigenous"	)
OR CONTAINS(LOWER([result_title_anthology]),	"autochthonous"	)
OR CONTAINS(LOWER([result_title_anthology]),	"sami"	)
OR CONTAINS(LOWER([result_title_anthology]),	"sámi "	)
OR CONTAINS(LOWER([result_title_anthology]),	"sápmi"	)
OR CONTAINS(LOWER([result_title_anthology]),	"tribal"	)
OR CONTAINS(LOWER([result_title_anthology]),	"women"	)
OR CONTAINS(LOWER([result_title_anthology]),	"girls"	)
OR CONTAINS(LOWER([result_title_anthology]),	"gender"	)
OR CONTAINS(LOWER([result_title_anthology]),	"disab"	)
OR CONTAINS(LOWER([result_title_anthology]),	"multicultur"	)
OR CONTAINS(LOWER([result_title_anthology]),	"welfare"	)
OR CONTAINS(LOWER([result_title_anthology]),	"social class"	)
OR CONTAINS(LOWER([result_title_anthology]),	"globalization"	)
OR CONTAINS(LOWER([result_title_anthology]),	"globalisation"	)
OR CONTAINS(LOWER([result_title_anthology]),	"neoliberal"	)
OR CONTAINS(LOWER([result_title_anthology]),	"capitalism"	)
OR CONTAINS(LOWER([result_title_anthology]),	"religio"	)
OR CONTAINS(LOWER([result_title_anthology]),	"islam"	)
OR CONTAINS(LOWER([result_title_anthology]),	"muslim"	)
OR CONTAINS(LOWER([result_title_anthology]),	"christian"	)
OR CONTAINS(LOWER([result_title_anthology]),	"jewish"	)
OR CONTAINS(LOWER([result_title_anthology]),	"hindu"	)
OR CONTAINS(LOWER([result_title_anthology]),	"sikh"	)
OR CONTAINS(LOWER([result_title_anthology]),	"buddhis"	)
))		
THEN 'inequality'		

ELSEIF (( 		
CONTAINS(LOWER([result_title_anthology]),	"globalization"	)
OR CONTAINS(LOWER([result_title_anthology]),	"globalisation"	)
OR CONTAINS(LOWER([result_title_anthology]),	"neoliberal"	)
OR CONTAINS(([result_title_anthology]),	"BRICS"	)
OR CONTAINS(LOWER([result_title_anthology]),	"neoliberal"	)
OR CONTAINS(LOWER([result_title_anthology]),	"least-developed countr"	)
OR CONTAINS(LOWER([result_title_anthology]),	"developing countr"	)
OR CONTAINS(LOWER([result_title_anthology]),	"low income countr"	)
OR CONTAINS(LOWER([result_title_anthology]),	"low-income countr"	)
OR CONTAINS(LOWER([result_title_anthology]),	"poor countr"	)
)		
AND (		
CONTAINS(LOWER([result_title_anthology]),	"development"	)
))		
THEN 'inequality'		

ELSEIF (((		
CONTAINS(LOWER([result_title_anthology]),	"local"	)
OR CONTAINS(LOWER([result_title_anthology]),	"traditional"	)
OR CONTAINS(LOWER([result_title_anthology]),	"community-based"	)
OR CONTAINS(LOWER([result_title_anthology]),	"indigenous"	))
AND (		
CONTAINS(LOWER([result_title_anthology]),	"knowledge"	))
)		
AND (		
NOT CONTAINS(LOWER([scientific_area_npi]),	"realfag"	))
)		
THEN 'inequality'		

ELSEIF 		
CONTAINS(LOWER([result_title_anthology]),	"human right"	)
OR CONTAINS(LOWER([result_title_anthology]),	"political rights"	)
OR CONTAINS(LOWER([result_title_anthology]),	"civil right"	)
OR CONTAINS(LOWER([result_title_anthology]),	"voting rights"	)
OR CONTAINS(LOWER([result_title_anthology]),	"sexual rights"	)
OR CONTAINS(LOWER([result_title_anthology]),	"land rights"	)
OR CONTAINS(LOWER([result_title_anthology]),	"constitutional rights"	)
OR CONTAINS(LOWER([result_title_anthology]),	"social rights"	)
THEN 'inequality'		

ELSEIF ((		
CONTAINS(LOWER([result_title_anthology]),	"women"	)		
OR CONTAINS(LOWER([result_title_anthology]),	"child"	)
OR CONTAINS(LOWER([result_title_anthology]),	"gender"	)
OR CONTAINS(LOWER([result_title_anthology]),	"indigenous"	)
)		
AND (		
CONTAINS(LOWER([result_title_anthology]),	"right"	)
OR CONTAINS(LOWER([result_title_anthology]),	"justice"	)
OR CONTAINS(LOWER([result_title_anthology]),	"security"	)
OR CONTAINS(LOWER([result_title_anthology]),	"quota"	)
))		
THEN 'inequality'		

ELSEIF (
CONTAINS(LOWER([result_title_anthology]),	"menneskerett"	)
OR CONTAINS(LOWER([result_title_anthology]),	"rettferdig"	)
OR CONTAINS(LOWER([result_title_anthology]),	"stemmerett"	)
OR CONTAINS(LOWER([result_title_anthology]),	"sexuelle rettigheter"	)
OR CONTAINS(LOWER([result_title_anthology]),	"politiske rettigheter"	)
OR CONTAINS(LOWER([result_title_anthology]),	"konstitusjonelle rettigheter"	)
)
THEN 'inequality'		

ELSEIF ((		
CONTAINS(LOWER([result_title_anthology]),	"kvinne"	)
OR CONTAINS(LOWER([result_title_anthology]),	"barn"	)
OR CONTAINS(LOWER([result_title_anthology]),	"kjønn"	)
OR CONTAINS(LOWER([result_title_anthology]),	"funksjonshemm" 	)
OR CONTAINS(LOWER([result_title_anthology]),	"urfolk"	)
)		
AND (		
CONTAINS(LOWER([result_title_anthology]),	"rettigheter"	)
OR CONTAINS(LOWER([result_title_anthology]),	"politikk"	)
OR CONTAINS(LOWER([result_title_anthology]),	"represent"	)
OR CONTAINS(LOWER([result_title_anthology]),	"kvote"	)
OR CONTAINS(LOWER([result_title_anthology]),	"makt"	)
))		
THEN 'inequality'

ELSE "non"
END
```

## Migration

"migration" is a difficult term as it is used so widely in biology (migrations of other species) and medicine (migration of cells, implants etc.). Thus, when used as a stand alone term, it is limited to NPI fields social sciences, humanities, psychology. 

Multiculturalism and integration is included. 

Mostly we use generic terms, but there were a number of publications specifically about islam/muslims in Europe/Norway, hence the specific search terms for this. For the same reason, a focus area in Norway, we include "Sami" as a specific search term. 

```Ceylon =
IF (		
CONTAINS(LOWER([journal]),	"asian and pacific migration journal"	)
OR CONTAINS(LOWER([journal]),	"central and eastern european migration review"	)
OR CONTAINS(LOWER([journal]),	"comparative migration studies"	)
OR CONTAINS(LOWER([journal]),	"crossings: journal of migration & culture"	)
OR CONTAINS(LOWER([journal]),	"european journal of migration and law"	)
OR CONTAINS(LOWER([journal]),	"immigration and asylum law and policy in europe"	)
OR CONTAINS(LOWER([journal]),	"international journal of migration, health and social care"	)
OR CONTAINS(LOWER([journal]),	"international migration (geneva. print)"	)
OR CONTAINS(LOWER([journal]),	"international migration review"	)
OR CONTAINS(LOWER([journal]),	"journal of ethnic and migration studies"	)
OR CONTAINS(LOWER([journal]),	"journal of identity and migration studies"	)
OR CONTAINS(LOWER([journal]),	"journal of international migration and integration"	)
OR CONTAINS(LOWER([journal]),	"journal of migration history"	)
OR CONTAINS(LOWER([journal]),	"migration and development"	)
OR CONTAINS(LOWER([journal]),	"migration letters"	)
OR CONTAINS(LOWER([journal]),	"migration studies"	)
OR CONTAINS(LOWER([journal]),	"nordic journal of migration research"	)
OR CONTAINS(LOWER([journal]),	"studies in global migration history"	)
OR CONTAINS(LOWER([journal]),	"international journal of refugee law"	)
OR CONTAINS(LOWER([journal]),	"journal of immigrant & refugee studies"	)
OR CONTAINS(LOWER([journal]),	"journal of refugee studies"	)
OR CONTAINS(LOWER([journal]),	"refugee survey quarterly"	)
OR CONTAINS(LOWER([journal]),	"multicultural education review"	)
)		
THEN 'migration'		

ELSEIF (		
CONTAINS(LOWER([result_title]),	"migrant"	)
OR CONTAINS(LOWER([result_title]),	"refugee"	)
OR CONTAINS(LOWER([result_title]),	"displaced person"	)
OR CONTAINS(LOWER([result_title]),	"displaced people"	)
OR CONTAINS(LOWER([result_title]),	"asyl"	)
OR CONTAINS(LOWER([result_title]),	"diaspora"	)
OR CONTAINS(LOWER([result_title]),	"stateless person"	)
OR CONTAINS(LOWER([result_title]),	"returnee"	)
OR CONTAINS(LOWER([result_title]),	"border regime"	)

OR CONTAINS(LOWER([result_title]),	"utvandring"	)
OR CONTAINS(LOWER([result_title]),	"innvandr"	)
OR CONTAINS(LOWER([result_title]),	"folkevandring"	)
OR CONTAINS(LOWER([result_title]),	"trelldom"	)
OR CONTAINS(LOWER([result_title]),	"flyktning"	)

OR CONTAINS(LOWER([result_title_anthology]),	"migrant"	)
OR CONTAINS(LOWER([result_title_anthology]),	"refugee"	)
OR CONTAINS(LOWER([result_title_anthology]),	"displaced person"	)
OR CONTAINS(LOWER([result_title_anthology]),	"displaced people"	)
OR CONTAINS(LOWER([result_title_anthology]),	"asyl"	)
OR CONTAINS(LOWER([result_title_anthology]),	"diaspora"	)
OR CONTAINS(LOWER([result_title_anthology]),	"stateless person"	)
OR CONTAINS(LOWER([result_title_anthology]),	"returnee"	)
OR CONTAINS(LOWER([result_title_anthology]),	"border regime"	)

OR CONTAINS(LOWER([result_title_anthology]),	"utvandring"	)
OR CONTAINS(LOWER([result_title_anthology]),	"innvandr"	)
OR CONTAINS(LOWER([result_title_anthology]),	"folkevandring"	)
OR CONTAINS(LOWER([result_title_anthology]),	"trelldom"	)
OR CONTAINS(LOWER([result_title_anthology]),	"flyktning"	)
)		
THEN 'migration'		

ELSEIF (		
( CONTAINS(LOWER([result_title]),	"migrasjon"	)
OR CONTAINS(LOWER([result_title]),	"migration"	)
OR CONTAINS(LOWER([result_title_anthology]),	"migration"	)
OR CONTAINS(LOWER([result_title_anthology]),	"migrasjon"	)
)		
AND (		
CONTAINS(LOWER([scientific_area_npi]),	"samfunn"	)
 OR CONTAINS(LOWER([scientific_area_npi]),	"humaniora"	)
 OR CONTAINS(LOWER([scientific_field_npi]),	"psykolog"	)
 OR CONTAINS(LOWER([scientific_field_npi]),	"psykiatri"	)
 OR CONTAINS(LOWER([scientific_field_npi]),	"samfunn"	)
))		
THEN 'migration'		

ELSEIF ((		
CONTAINS(LOWER([result_title]),	"islam"	)
OR CONTAINS(LOWER([result_title]),	"muslim"	)
OR CONTAINS(LOWER([result_title_anthology]),	"islam"	)
OR CONTAINS(LOWER([result_title_anthology]),	"muslim"	)
)		
AND (		
CONTAINS(LOWER([result_title]),	"europe"	)
OR CONTAINS(LOWER([result_title]),	"norway"	)
OR CONTAINS(LOWER([result_title_anthology]),	"europe"	)
OR CONTAINS(LOWER([result_title_anthology]),	"norway"	)
))		
THEN 'migration'		

ELSEIF 		
CONTAINS(LOWER([result_title]),	"cultural integra"	)
OR CONTAINS(LOWER([result_title]),	"acculturat"	)
OR CONTAINS(LOWER([result_title]),	"intercultur"	)
OR CONTAINS(LOWER([result_title]),	"multicultural"	)
OR CONTAINS(LOWER([result_title]),	"multikulturel"	)
OR CONTAINS(LOWER([result_title]),	"flerkultu"	)
OR CONTAINS(LOWER([result_title]),	"kulturelt mangfold"	)
OR CONTAINS(LOWER([result_title_anthology]),	"cultural integra"	)
OR CONTAINS(LOWER([result_title_anthology]),	"acculturat"	)
OR CONTAINS(LOWER([result_title_anthology]),	"intercultur"	)
OR CONTAINS(LOWER([result_title_anthology]),	"multicultural"	)
OR CONTAINS(LOWER([result_title_anthology]),	"multikulturel"	)
OR CONTAINS(LOWER([result_title_anthology]),	"flerkultu"	)
OR CONTAINS(LOWER([result_title_anthology]),	"kulturelt mangfold"	)
THEN 'migration'		

ELSE "non"
END
```

## Health & Inequality

Made of terms from the two main searches in these areas, with some changes (e.g. NPI field "medisin" did not work as effectively here, thus was removed). Plus additional terms:

* Journals relevant to this intersection
* Terms for partner violence
* Terms for violence, addictions and disability and certain groups
* Inequality terms combined with disability
* "body politics" 

```Ceylon =
IF		
CONTAINS(LOWER([journal]),	"equity in health"	)
OR CONTAINS(LOWER([journal]),	"globalization and health"	)
OR CONTAINS(LOWER([journal]),	"health and human rights"	)
OR CONTAINS(LOWER([journal]),	"gender medicine"	)
OR CONTAINS(LOWER([journal]),	"disability & society"	)
OR CONTAINS(LOWER([journal]),	"immigrant and minority health"	)
OR CONTAINS(LOWER([journal]),	"ethnicity and health"	)
OR CONTAINS(LOWER([journal]),	"disability, development and education"	)
OR CONTAINS(LOWER([journal]),	"diseases of poverty"	)
OR CONTAINS(LOWER([journal]),	"body & society"	)
OR CONTAINS(LOWER([result_title]),	"body politics"	)
THEN 'health and inequality'		

ELSEIF ((		
CONTAINS(LOWER([result_title]),	"global south"	)
OR CONTAINS(LOWER([result_title]),	"development assistance"	)
OR CONTAINS(LOWER([result_title]),	"development aid"	)
OR CONTAINS(LOWER([result_title]),	"least-developed countr"	)
OR CONTAINS(LOWER([result_title]),	"developing countr"	)
OR CONTAINS(LOWER([result_title]),	"low income countr"	)
OR CONTAINS(LOWER([result_title]),	"low-income countr"	)
OR CONTAINS(LOWER([result_title]),	"poor countr"	)
OR CONTAINS(LOWER([result_title]),	"globalization"	)
OR CONTAINS(LOWER([result_title]),	"globalisation"	)
)		
AND (		
CONTAINS(LOWER([result_title]),	"health"	)
OR CONTAINS(LOWER([scientific_area_npi]),	"medisin"	)
))		
THEN 'health and inequality'		

ELSEIF((		
CONTAINS(LOWER([result_title]),	"equalit"	)
OR CONTAINS(LOWER([result_title]),	"equity"	)
OR CONTAINS(LOWER([result_title]),	"egalitar"	)
OR CONTAINS(LOWER([result_title]),	"disparit"	)
OR CONTAINS(LOWER([result_title]),	"representation"	)
OR CONTAINS(LOWER([result_title]),	"discrimination"	)
OR CONTAINS(LOWER([result_title]),	"criminali"	)
OR CONTAINS(LOWER([result_title]),	"marginali"	)
OR CONTAINS(LOWER([result_title]),	"otherness"	)
OR CONTAINS(LOWER([result_title]),	"stereotyp"	)
OR CONTAINS(LOWER([result_title]),	"rights"	)
OR CONTAINS(LOWER([result_title]),	"justice"	)
OR CONTAINS(LOWER([result_title]),	"access "	)
OR CONTAINS(LOWER([result_title]),	"poverty"	)
OR CONTAINS(LOWER([result_title]),	"economic burden"	)
OR CONTAINS(LOWER([result_title]),	"debt"	)
OR CONTAINS(LOWER([result_title]),	"microfinance"	)
OR CONTAINS(LOWER([result_title]),	"homeless"	)
OR CONTAINS(LOWER([result_title]),	"social welfare"	)
OR CONTAINS(LOWER([result_title]),	"social security"	)
OR CONTAINS(LOWER([result_title]),	"social sustainab"	)
OR CONTAINS(LOWER([result_title]),	"social policy"	)
OR CONTAINS(LOWER([result_title]),	"disadvantaged"	)
OR CONTAINS(LOWER([result_title]),	"the vulnerable"	)
OR CONTAINS(LOWER([result_title]),	"vulnerable group"	)
OR CONTAINS(LOWER([result_title]),	"indigenous"	)
OR CONTAINS(LOWER([result_title]),	"autochthonous"	)
OR CONTAINS(LOWER([result_title]),	"sami "	)
OR CONTAINS(LOWER([result_title]),	"sámi "	)
OR CONTAINS(LOWER([result_title]),	"sápmi"	)
OR CONTAINS(LOWER([result_title]),	"minorit"	)
OR CONTAINS(LOWER([result_title]),	"ethnicity"	)
OR CONTAINS(LOWER([result_title]),	"racism"	)
OR CONTAINS(LOWER([result_title]),	"racial"	)
OR CONTAINS(LOWER([result_title]),	"apartheid"	)
OR CONTAINS(LOWER([result_title]),	"colonial"	)
OR CONTAINS(LOWER([result_title]),	"colonialism"	)
OR CONTAINS(LOWER([result_title]),	"gender perspective"	)
OR CONTAINS(LOWER([result_title]),	"gendered"	)
OR CONTAINS(LOWER([result_title]),	"sexism"	)
OR CONTAINS(LOWER([result_title]),	"intersectional"	)
OR CONTAINS(LOWER([result_title]),	"ageism"	)
OR CONTAINS(LOWER([result_title]),	"homophob"	)
OR CONTAINS(LOWER([result_title]),	"gay"	)
OR CONTAINS(LOWER([result_title]),	"lesbian"	)
OR CONTAINS(LOWER([result_title]),	"bisexual"	)
OR CONTAINS(LOWER([result_title]),	"transgender"	)
OR CONTAINS(LOWER([result_title]),	"queer"	)
OR CONTAINS(LOWER([result_title]),	"LGBT"	)
OR CONTAINS(LOWER([result_title]),	"food insecurity"	)
OR CONTAINS(LOWER([result_title]),	"food security"	)
OR CONTAINS(LOWER([result_title]),	"right to food"	)
OR CONTAINS(LOWER([result_title]),	"development assistance"	)
OR CONTAINS(LOWER([result_title]),	"development aid"	)
)		
AND (		
CONTAINS(LOWER([result_title]),	"health"	)
OR CONTAINS(LOWER([result_title]),	"mortality"	)
OR CONTAINS(LOWER([result_title]),	"medicin"	)
OR CONTAINS(LOWER([result_title]),	"medical"	)
OR CONTAINS(LOWER([result_title]),	"clinic"	)
OR CONTAINS(LOWER([result_title]),	"disease"	)
OR CONTAINS(LOWER([result_title]),	"illness"	)
OR CONTAINS(LOWER([result_title]),	"infection"	)
OR CONTAINS(LOWER([result_title]),	"vaccin"	)
OR CONTAINS(LOWER([result_title]),	"antibiotic"	)
OR CONTAINS(LOWER([result_title]),	"nurses"	)
OR CONTAINS(LOWER([result_title]),	"doctors"	)
OR CONTAINS(LOWER([result_title]),	"physician"	)
OR CONTAINS(LOWER([result_title]),	"dentist"	)
OR CONTAINS(LOWER([result_title]),	"dental"	)
OR CONTAINS(LOWER([result_title]),	"surgery"	)
OR CONTAINS(LOWER([result_title]),	"surgeon"	)
OR CONTAINS(LOWER([result_title]),	"trauma"	)
OR CONTAINS(LOWER([result_title]),	"matern"	)
OR CONTAINS(LOWER([result_title]),	"midwif"	)
OR CONTAINS(LOWER([result_title]),	"childbirth"	)
OR CONTAINS(LOWER([result_title]),	"childbear"	)
OR CONTAINS(LOWER([result_title]),	"breastfeed"	)
OR CONTAINS(LOWER([result_title]),	"birthweight"	)
OR CONTAINS(LOWER([result_title]),	"perinatal"	)
OR CONTAINS(LOWER([result_title]),	"postnatal"	)
OR CONTAINS(LOWER([result_title]),	"enatal "	)
OR CONTAINS(LOWER([result_title]),	"abortion"	)
OR CONTAINS(LOWER([result_title]),	"pregnan"	)
OR CONTAINS(LOWER([result_title]),	"obstetric"	)
OR CONTAINS(LOWER([result_title]),	"sex education"	)
OR CONTAINS(LOWER([result_title]),	"residential care"	)
OR CONTAINS(LOWER([result_title]),	"disab"	)
OR CONTAINS(LOWER([result_title]),	"impairment"	)
OR CONTAINS(LOWER([result_title]),	"child development"	)
OR CONTAINS(LOWER([result_title]),	"cognative"	)
OR CONTAINS(LOWER([result_title]),	"nutrition"	)
OR CONTAINS(LOWER([result_title]),	"konzo"	)
OR CONTAINS(LOWER([result_title]),	"marasmus"	)
OR CONTAINS(LOWER([result_title]),	"kwashiorkor"	)
OR CONTAINS(LOWER([result_title]),	"vitamin"	)
OR CONTAINS(LOWER([result_title]),	"micronutrient"	)
OR CONTAINS(LOWER([result_title]),	"diet"	)
OR CONTAINS(LOWER([result_title]),	"risk behavi"	)
OR CONTAINS(LOWER([result_title]),	"therap"	)
OR CONTAINS(LOWER([result_title]),	"counselling"	)
OR CONTAINS(LOWER([result_title]),	"psycholog"	)
OR CONTAINS(LOWER([result_title]),	"psychiat"	)
OR CONTAINS(LOWER([result_title]),	"wellbeing"	)
OR CONTAINS(LOWER([result_title]),	"well-being"	)
OR CONTAINS(LOWER([result_title]),	"suicide"	)
OR CONTAINS(LOWER([result_title]),	"self-harm"	)
OR CONTAINS(LOWER([result_title]),	"depression"	)
OR CONTAINS(LOWER([result_title]),	"orthopedic"	)
OR CONTAINS(LOWER([result_title]),	"cancer"	)
OR CONTAINS(LOWER([result_title]),	"asthma"	)
OR CONTAINS(LOWER([result_title]),	"diabetes"	)
OR CONTAINS(LOWER([result_title]),	"dust exposure"	)
OR CONTAINS(LOWER([result_title]),	"pneumonia"	)
OR CONTAINS(LOWER([result_title]),	"diarrhea"	)
OR CONTAINS(LOWER([result_title]),	"coronavirus"	)
OR CONTAINS(LOWER([result_title]),	"covid"	)
OR CONTAINS(LOWER([result_title]),	"tobacco"	)
OR CONTAINS(LOWER([result_title]),	"tombak"	)
OR CONTAINS(LOWER([result_title]),	"injuries"	)
OR CONTAINS(LOWER([result_title]),	"accident"	)
OR CONTAINS(LOWER([result_title]),	"malaria"	)
OR CONTAINS(LOWER([result_title]),	"cholera"	)
OR CONTAINS(([result_title]),	"HIV"	)
OR CONTAINS(LOWER([result_title]),	"polio"	)
OR CONTAINS(LOWER([result_title]),	"tuberculosis"	)
)		
AND (		
NOT CONTAINS(LOWER([result_title]),	"access control"	)
))		
THEN 'health and inequality'		

ELSEIF ((		
CONTAINS(LOWER([result_title]),	"kvinne"	)
OR CONTAINS(LOWER([result_title]),	"kjønn"	)
OR CONTAINS(LOWER([result_title]),	"homofil"	)
OR CONTAINS(LOWER([result_title]),	"LGBT"	)
OR CONTAINS(LOWER([result_title]),	"urfolk"	)
OR CONTAINS(LOWER([result_title]),	"sami "	)
OR CONTAINS(LOWER([result_title]),	"sámi "	)
OR CONTAINS(LOWER([result_title]),	"sápmi"	)
OR CONTAINS(LOWER([result_title]),	"minorit"	)
OR CONTAINS(LOWER([result_title]),	"etnisk"	)
OR CONTAINS(LOWER([result_title]),	"forskjellsbehan"	)
OR CONTAINS(LOWER([result_title]),	"likestilling"	)
OR CONTAINS(LOWER([result_title]),	"inkludering"	)
OR CONTAINS(LOWER([result_title]),	"utenforskap"	)
)		
AND (		
CONTAINS(LOWER([result_title]),	"funksjonshem"	)
OR CONTAINS(LOWER([result_title]),	"ufør"	)
))		
THEN 'health and inequality'		

ELSEIF		
CONTAINS(LOWER([result_title]),	"domestic violence"	)
OR CONTAINS(LOWER([result_title]),	"partner violence"	)
OR CONTAINS(LOWER([result_title]),	"vold i parforhold"	)
OR CONTAINS(LOWER([result_title]),	"femicide"	)
THEN 'health and inequality'		

ELSEIF ((		
CONTAINS(LOWER([result_title]),	"women"	)
OR CONTAINS(LOWER([result_title]),	"gender"	)
OR CONTAINS(LOWER([result_title]),	"gay"	)
OR CONTAINS(LOWER([result_title]),	"lesbian"	)
OR CONTAINS(LOWER([result_title]),	"bisexual"	)
OR CONTAINS(LOWER([result_title]),	"care" 	)
OR CONTAINS(LOWER([result_title]),	"elderly" 	)
OR CONTAINS(LOWER([result_title]),	"disab" 	)
OR CONTAINS(LOWER([result_title]),	"elector" 	)
OR CONTAINS(LOWER([result_title]),	"indigenous"	)
OR CONTAINS(LOWER([result_title]),	"autochthonous"	)
OR CONTAINS(LOWER([result_title]),	"sami "	)
OR CONTAINS(LOWER([result_title]),	"sámi "	)
OR CONTAINS(LOWER([result_title]),	"sápmi"	)
OR CONTAINS(LOWER([result_title]),	"minorit"	)
OR CONTAINS(LOWER([result_title]),	"ethnic"	)
)		
AND (		
CONTAINS(LOWER([result_title]),	"violence"	)
OR CONTAINS(LOWER([result_title]),	"abuse"	)
OR CONTAINS(LOWER([result_title]),	"alcoholism"	)
OR CONTAINS(LOWER([result_title]),	"binge drink"	)
OR CONTAINS(LOWER([result_title]),	"addict"	)
))		
THEN 'health and inequality'		

ELSEIF ((		
CONTAINS(LOWER([result_title]),	"kvinne"	)
OR CONTAINS(LOWER([result_title]),	"kjønn"	)
OR CONTAINS(LOWER([result_title]),	"homofil"	)
OR CONTAINS(LOWER([result_title]),	"LGBT"	)
OR CONTAINS(LOWER([result_title]),	" eldre"	)
OR CONTAINS(LOWER([result_title]),	"funksjonshem" 	)
OR CONTAINS(LOWER([result_title]),	"politisk" 	)
OR CONTAINS(LOWER([result_title]),	"urfolk"	)
OR CONTAINS(LOWER([result_title]),	"sami "	)
OR CONTAINS(LOWER([result_title]),	"sámi "	)
OR CONTAINS(LOWER([result_title]),	"sápmi"	)
OR CONTAINS(LOWER([result_title]),	"minorit"	)
OR CONTAINS(LOWER([result_title]),	"etnisk"	)
)		
AND (		
CONTAINS(LOWER([result_title]),	"vold"	)
OR CONTAINS(LOWER([result_title]),	"rusavhengi"	)
))		
THEN 'health and inequality'		

ELSE "non"
END
```

## Health & Migration

Terms taken from the main focus areas. 

"Whales", "cancer cells", NPI field biology excluded from health and migration

```Ceylon =
IF		
CONTAINS(LOWER([journal]),	"immigrant and minority health"	)
OR CONTAINS(LOWER([journal]),	"ethnicity and health"	)
THEN "health and migration"		

ELSEIF (((		
CONTAINS(LOWER([result_title]),	"migrant"	)
OR CONTAINS(LOWER([result_title]),	"migration"	)
OR CONTAINS(LOWER([result_title]),	"refugee"	)
OR CONTAINS(LOWER([result_title]),	"displaced person"	)
OR CONTAINS(LOWER([result_title]),	"displaced people"	)
OR CONTAINS(LOWER([result_title]),	"stateless person"	)
OR CONTAINS(LOWER([result_title]),	"returnee"	)
OR CONTAINS(LOWER([result_title]),	"asylum seeker"	)
OR CONTAINS(LOWER([result_title]),	"cultural integ"	)
OR CONTAINS(LOWER([result_title]),	"language barrier"	)
)		
AND (		
CONTAINS(LOWER([result_title]),	"health"	)
OR CONTAINS(LOWER([result_title]),	"mortality"	)
OR CONTAINS(LOWER([result_title]),	"medicin"	)
OR CONTAINS(LOWER([result_title]),	"medical"	)
OR CONTAINS(LOWER([result_title]),	"clinic"	)
OR CONTAINS(LOWER([result_title]),	"disease"	)
OR CONTAINS(LOWER([result_title]),	"infection"	)
OR CONTAINS(LOWER([result_title]),	"illness"	)
OR CONTAINS(LOWER([result_title]),	"vaccin"	)
OR CONTAINS(LOWER([result_title]),	"antibiotic"	)
OR CONTAINS(LOWER([result_title]),	"nurses"	)
OR CONTAINS(LOWER([result_title]),	"doctors"	)
OR CONTAINS(LOWER([result_title]),	"physician"	)
OR CONTAINS(LOWER([result_title]),	"dentist"	)
OR CONTAINS(LOWER([result_title]),	"dental"	)
OR CONTAINS(LOWER([result_title]),	"surgery"	)
OR CONTAINS(LOWER([result_title]),	"surgeon"	)
OR CONTAINS(LOWER([result_title]),	"trauma"	)
OR CONTAINS(LOWER([result_title]),	"matern"	)
OR CONTAINS(LOWER([result_title]),	"midwif"	)
OR CONTAINS(LOWER([result_title]),	"childbirth"	)
OR CONTAINS(LOWER([result_title]),	"childbear"	)
OR CONTAINS(LOWER([result_title]),	"breastfeed"	)
OR CONTAINS(LOWER([result_title]),	"birthweight"	)
OR CONTAINS(LOWER([result_title]),	"perinatal"	)
OR CONTAINS(LOWER([result_title]),	"postnatal"	)
OR CONTAINS(LOWER([result_title]),	"enatal "	)
OR CONTAINS(LOWER([result_title]),	"abortion"	)
OR CONTAINS(LOWER([result_title]),	"pregnan"	)
OR CONTAINS(LOWER([result_title]),	"obstetric"	)
OR CONTAINS(LOWER([result_title]),	"sex education"	)
OR CONTAINS(LOWER([result_title]),	"residential care"	)
OR CONTAINS(LOWER([result_title]),	"disab"	)
OR CONTAINS(LOWER([result_title]),	"impairment"	)
OR CONTAINS(LOWER([result_title]),	"child development"	)
OR CONTAINS(LOWER([result_title]),	"cognative"	)
OR CONTAINS(LOWER([result_title]),	"nutrition"	)
OR CONTAINS(LOWER([result_title]),	"konzo"	)
OR CONTAINS(LOWER([result_title]),	"marasmus"	)
OR CONTAINS(LOWER([result_title]),	"kwashiorkor"	)
OR CONTAINS(LOWER([result_title]),	"vitamin"	)
OR CONTAINS(LOWER([result_title]),	"micronutrient"	)
OR CONTAINS(LOWER([result_title]),	"diet"	)
OR CONTAINS(LOWER([result_title]),	"risk behavi"	)
OR CONTAINS(LOWER([result_title]),	"therap"	)
OR CONTAINS(LOWER([result_title]),	"counselling"	)
OR CONTAINS(LOWER([result_title]),	"psycholog"	)
OR CONTAINS(LOWER([result_title]),	"psychiat"	)
OR CONTAINS(LOWER([result_title]),	"wellbeing"	)
OR CONTAINS(LOWER([result_title]),	"well-being"	)
OR CONTAINS(LOWER([result_title]),	"suicide"	)
OR CONTAINS(LOWER([result_title]),	"self-harm"	)
OR CONTAINS(LOWER([result_title]),	"orthopedic"	)
OR CONTAINS(LOWER([result_title]),	"cancer"	)
OR CONTAINS(LOWER([result_title]),	"asthma"	)
OR CONTAINS(LOWER([result_title]),	"diabetes"	)
OR CONTAINS(LOWER([result_title]),	"dust exposure"	)
OR CONTAINS(LOWER([result_title]),	"pneumonia"	)
OR CONTAINS(LOWER([result_title]),	"diarrhea"	)
OR CONTAINS(LOWER([result_title]),	"coronavirus"	)
OR CONTAINS(LOWER([result_title]),	"covid"	)
OR CONTAINS(LOWER([result_title]),	"tobacco"	)
OR CONTAINS(LOWER([result_title]),	"tombak"	)
OR CONTAINS(LOWER([result_title]),	"injuries"	)
OR CONTAINS(LOWER([result_title]),	"accident"	)
OR CONTAINS(LOWER([result_title]),	"alcoholism"	)
OR CONTAINS(LOWER([result_title]),	"binge drink"	)
OR CONTAINS(LOWER([result_title]),	"addict"	)
OR CONTAINS(LOWER([journal]),	"parasites and vectors"	)
OR CONTAINS(LOWER([result_title]),	"malaria"	)
OR CONTAINS(LOWER([result_title]),	"cholera"	)
OR CONTAINS(([result_title]),	"HIV"	)
OR CONTAINS(LOWER([result_title]),	"polio"	)
OR CONTAINS(LOWER([result_title]),	"tuberculosis"	)
OR CONTAINS(LOWER([result_title]),	"water-bourne"	)
OR CONTAINS(LOWER([result_title]),	"waterbourne"	)
OR CONTAINS(LOWER([result_title]),	"maternal mortality"	)
OR CONTAINS(LOWER([result_title]),	"child mortality"	)
OR CONTAINS(LOWER([result_title]),	"infant mortality"	)

OR CONTAINS(LOWER([scientific_area_npi]),	"medisin"	)
))		

AND NOT (		
CONTAINS(([scientific_field_npi]),	"Biologi"	)
 OR CONTAINS(LOWER([result_title]),	"cancer cell"	)
 OR CONTAINS(LOWER([result_title]),	"cell migration"	)
 OR CONTAINS(LOWER([result_title]),	"whale"	)

))		

THEN "health and migration"		

ELSEIF((		
CONTAINS(LOWER([result_title]),	"innvandr"	)
OR CONTAINS(LOWER([result_title]),	"migrasjon"	)
OR CONTAINS(LOWER([result_title]),	"flyktning"	)
OR CONTAINS(LOWER([result_title]),	"asyl"	)
OR CONTAINS(LOWER([result_title]),	"minoritet"	)
OR CONTAINS(LOWER([result_title]),	"multikulturel"	)
OR CONTAINS(LOWER([result_title]),	"flerkultu"	)
OR CONTAINS(LOWER([result_title_anthology]),	"innvandr"	)
OR CONTAINS(LOWER([result_title_anthology]),	"migrasjon"	)
OR CONTAINS(LOWER([result_title_anthology]),	"multikulturel"	)
OR CONTAINS(LOWER([result_title_anthology]),	"flerkultu"	)
)		
AND (		
CONTAINS(LOWER([result_title]),	"helse"	)
OR CONTAINS(LOWER([result_title]),	"funksjonshem"	)
OR CONTAINS(LOWER([result_title]),	"syke"	)
OR CONTAINS(LOWER([result_title]),	"omsorg"	)
OR CONTAINS(LOWER([result_title_anthology]),	"helse"	)
OR CONTAINS(LOWER([result_title_anthology]),	"funksjonshem"	)
OR CONTAINS(LOWER([result_title_anthology]),	"syke"	)
OR CONTAINS(LOWER([result_title_anthology]),	"omsorg"	)
OR CONTAINS(LOWER([scientific_area_npi]),	"medisin"	)
))		

THEN "health and migration"		

ELSE "non"
END
```

## Inequality & Migration

Combined migration terms with inequality words. In addition, terms for research about people traffiking and islamophobia are included. 

```Ceylon =
IF		
CONTAINS(LOWER([journal]),	"ethnicities"	)
OR CONTAINS(LOWER([journal]),	"muslims in europe"	)
THEN 'migration and inequality'		

ELSEIF((		
CONTAINS(LOWER([result_title]),	"migrant"	)
OR CONTAINS(LOWER([result_title]),	"migration"	)
OR CONTAINS(LOWER([result_title]),	"refugee"	)
OR CONTAINS(LOWER([result_title]),	"displaced person"	)
OR CONTAINS(LOWER([result_title]),	"displaced people"	)
OR CONTAINS(LOWER([result_title]),	"stateless person"	)
OR CONTAINS(LOWER([result_title]),	"returnee"	)
OR CONTAINS(LOWER([result_title]),	"asylum seeker"	)
OR CONTAINS(LOWER([result_title_anthology]),	"migrant"	)
OR CONTAINS(LOWER([result_title_anthology]),	"migration"	)
OR CONTAINS(LOWER([result_title_anthology]),	"refugee"	)
OR CONTAINS(LOWER([result_title_anthology]),	"asylum"	)
)		
AND (		
CONTAINS(LOWER([result_title]),	"equal"	)
OR CONTAINS(LOWER([result_title]),	"equity"	)
OR CONTAINS(LOWER([result_title]),	"egalitar"	)
OR CONTAINS(LOWER([result_title]),	"representation"	)
OR CONTAINS(LOWER([result_title]),	"marginali"	)
OR CONTAINS(LOWER([result_title]),	"disparit"	)
OR CONTAINS(LOWER([result_title]),	"empower"	)
OR CONTAINS(LOWER([result_title]),	"inclusion"	)
OR CONTAINS(LOWER([result_title]),	"exclusion"	)
OR CONTAINS(LOWER([result_title]),	"inclusive"	)
OR CONTAINS(LOWER([result_title]),	"exclusive "	)
OR CONTAINS(LOWER([result_title]),	"excluding"	)
OR CONTAINS(LOWER([result_title]),	"belonging"	)
OR CONTAINS(LOWER([result_title]),	"otherness"	)
OR CONTAINS(LOWER([result_title]),	" othering"	)
OR CONTAINS(LOWER([result_title]),	"intersectional"	)
OR CONTAINS(LOWER([result_title]),	"discrimination"	)
OR CONTAINS(LOWER([result_title]),	"minority stress"	)
OR CONTAINS(LOWER([result_title]),	"minority language"	)
OR CONTAINS(LOWER([result_title]),	"stereotyp"	)
OR CONTAINS(LOWER([result_title]),	"criminali"	)
OR CONTAINS(LOWER([result_title]),	"racism"	)
OR CONTAINS(LOWER([result_title]),	"racial"	)

OR CONTAINS(LOWER([result_title]),	"colonial"	)
OR CONTAINS(LOWER([result_title]),	"colonialism"	)
OR CONTAINS(LOWER([result_title]),	"food insecurity"	)
OR CONTAINS(LOWER([result_title]),	"food security"	)
OR CONTAINS(LOWER([result_title]),	"right to food"	)

OR CONTAINS(LOWER([result_title]),	"right"	)
OR CONTAINS(LOWER([result_title]),	"justice"	)
OR CONTAINS(LOWER([result_title]),	"freedom"	)
OR CONTAINS(LOWER([result_title]),	"security"	)

OR CONTAINS(LOWER([result_title]),	"poverty"	)
OR CONTAINS(LOWER([result_title]),	"microfinance"	)
OR CONTAINS(LOWER([result_title]),	"microcredit"	)
OR CONTAINS(LOWER([result_title]),	"debt"	)
OR CONTAINS(LOWER([result_title]),	"financial inclusion"	)
OR CONTAINS(LOWER([result_title]),	"beggar"	)
OR CONTAINS(LOWER([result_title]),	"begging"	)
OR CONTAINS(LOWER([result_title]),	"homeless"	)
OR CONTAINS(LOWER([result_title]),	"slave"	)
OR CONTAINS(LOWER([result_title]),	"disadvantaged"	)
OR CONTAINS(LOWER([result_title]),	"social class"	)
OR CONTAINS(LOWER([result_title]),	"social sustainab"	)
OR CONTAINS(LOWER([result_title]),	"social welfare"	)
OR CONTAINS(LOWER([result_title]),	"social security"	)
OR CONTAINS(LOWER([result_title]),	"social policy"	)

OR CONTAINS(LOWER([result_title]),	"women"	)
OR CONTAINS(LOWER([result_title]),	"girls"	)
OR CONTAINS(LOWER([result_title]),	"gender"	)
OR CONTAINS(LOWER([result_title]),	"sexism"	)
 OR CONTAINS(LOWER([scientific_field_npi]),	"kjønnsforskning"	)
OR CONTAINS(LOWER([result_title]),	"homophob"	)
OR CONTAINS(LOWER([result_title]),	"gay"	)
OR CONTAINS(LOWER([result_title]),	"lesbian"	)
OR CONTAINS(LOWER([result_title]),	"bisexual"	)
OR CONTAINS(LOWER([result_title]),	"transgender"	)
OR CONTAINS(LOWER([result_title]),	"queer"	)
OR CONTAINS(LOWER([result_title]),	"LGBT"	)
OR CONTAINS(LOWER([result_title]),	"ageism"	)
OR CONTAINS(LOWER([result_title]),	"disab"	)
OR CONTAINS(LOWER([result_title]),	"intersectional"	)
))		
THEN "migration and inequality"		

ELSEIF ((		
CONTAINS(LOWER([result_title]),	"islam"	)
OR CONTAINS(LOWER([result_title]),	"muslim"	)
)		
AND (		
CONTAINS(LOWER([result_title]),	"far right"	)
OR CONTAINS(LOWER([result_title]),	"anti-islam"	)
OR CONTAINS(LOWER([result_title]),	"islamo"	)
))		
THEN 'migration and inequality'		

ELSEIF ((		
CONTAINS(LOWER([result_title]),	"smuggling"	)
OR CONTAINS(LOWER([result_title]),	"trafficking"	)
)		
AND (		
CONTAINS(LOWER([result_title]),	"victim"	)
OR CONTAINS(LOWER([result_title]),	"human"	)
OR CONTAINS(LOWER([result_title]),	"people"	)
OR CONTAINS(LOWER([result_title]),	"child"	)
OR CONTAINS(LOWER([result_title]),	"slave"	)
//OR CONTAINS(LOWER([result_title]),	"migrant"	)
//OR CONTAINS(LOWER([result_title]),	"migration"	)
//OR CONTAINS(LOWER([result_title]),	"refugee"	)
//OR CONTAINS(LOWER([result_title]),	"displaced person"	)
//OR CONTAINS(LOWER([result_title]),	"displaced people"	)
//OR CONTAINS(LOWER([result_title]),	"stateless person"	)
))		
THEN "migration and inequality"		

ELSEIF((		
CONTAINS(LOWER([result_title]),	"innvandr"	)
OR CONTAINS(LOWER([result_title]),	"migrasjon"	)
OR CONTAINS(LOWER([result_title]),	"flyktning"	)
OR CONTAINS(LOWER([result_title]),	"asyl"	)
)		
AND (		
CONTAINS(LOWER([result_title]),	"fattigdom"	)
OR CONTAINS(LOWER([result_title]),	"slavehandel"	)
OR CONTAINS(LOWER([result_title]),	"slaver"	)
OR CONTAINS(LOWER([result_title]),	"sosialt bærekraft"	)
OR CONTAINS(LOWER([result_title]),	"sosial bærekraft"	)
OR CONTAINS(LOWER([result_title]),	"rasisme"	)
OR CONTAINS(LOWER([result_title]),	"homofil"	)
OR CONTAINS(LOWER([result_title]),	"minoritet"	)
OR CONTAINS(LOWER([result_title]),	"forskjellsbehan"	)
OR CONTAINS(LOWER([result_title]),	"diskrim"	)
OR CONTAINS(LOWER([result_title]),	"likestilling"	)
OR CONTAINS(LOWER([result_title]),	"inkludering"	)
OR CONTAINS(LOWER([result_title]),	"utenforskap"	)

OR CONTAINS(LOWER([result_title]),	"rettigheter"	)
OR CONTAINS(LOWER([result_title]),	"politikk"	)
OR CONTAINS(LOWER([result_title]),	"represent"	)
OR CONTAINS(LOWER([result_title]),	"frihet"	)
OR CONTAINS(LOWER([result_title]),	"sikkerhet"	)
OR CONTAINS(LOWER([result_title]),	"makt"	)
))		
THEN "migration and inequality"		

ELSEIF((		
CONTAINS(LOWER([result_title_anthology]),	"migrant"	)
OR CONTAINS(LOWER([result_title_anthology]),	"migration"	)
OR CONTAINS(LOWER([result_title_anthology]),	"refugee"	)
OR CONTAINS(LOWER([result_title_anthology]),	"displaced person"	)
OR CONTAINS(LOWER([result_title_anthology]),	"displaced people"	)
OR CONTAINS(LOWER([result_title_anthology]),	"stateless person"	)
OR CONTAINS(LOWER([result_title_anthology]),	"returnee"	)
OR CONTAINS(LOWER([result_title_anthology]),	"asylum seeker"	)
)		
AND (		
CONTAINS(LOWER([result_title_anthology]),	"equal"	)
OR CONTAINS(LOWER([result_title_anthology]),	"equity"	)
OR CONTAINS(LOWER([result_title_anthology]),	"egalitar"	)
OR CONTAINS(LOWER([result_title_anthology]),	"representation"	)
OR CONTAINS(LOWER([result_title_anthology]),	"marginali"	)
OR CONTAINS(LOWER([result_title_anthology]),	"disparit"	)
OR CONTAINS(LOWER([result_title_anthology]),	"empower"	)
OR CONTAINS(LOWER([result_title_anthology]),	"inclusion"	)
OR CONTAINS(LOWER([result_title_anthology]),	"exclusion"	)
OR CONTAINS(LOWER([result_title_anthology]),	"inclusive"	)
OR CONTAINS(LOWER([result_title_anthology]),	"exclusive "	)
OR CONTAINS(LOWER([result_title_anthology]),	"excluding"	)
OR CONTAINS(LOWER([result_title_anthology]),	"belonging"	)
OR CONTAINS(LOWER([result_title_anthology]),	"otherness"	)
OR CONTAINS(LOWER([result_title_anthology]),	" othering"	)
OR CONTAINS(LOWER([result_title_anthology]),	"intersectional"	)
OR CONTAINS(LOWER([result_title_anthology]),	"discrimination"	)
OR CONTAINS(LOWER([result_title_anthology]),	"minority stress"	)
OR CONTAINS(LOWER([result_title_anthology]),	"minority language"	)
OR CONTAINS(LOWER([result_title_anthology]),	"stereotyp"	)
OR CONTAINS(LOWER([result_title_anthology]),	"criminali"	)
OR CONTAINS(LOWER([result_title_anthology]),	"racism"	)
OR CONTAINS(LOWER([result_title_anthology]),	"racial"	)

OR CONTAINS(LOWER([result_title_anthology]),	"colonial"	)
OR CONTAINS(LOWER([result_title_anthology]),	"colonialism"	)
OR CONTAINS(LOWER([result_title_anthology]),	"food insecurity"	)
OR CONTAINS(LOWER([result_title_anthology]),	"food security"	)
OR CONTAINS(LOWER([result_title_anthology]),	"right to food"	)

OR CONTAINS(LOWER([result_title_anthology]),	"right"	)
OR CONTAINS(LOWER([result_title_anthology]),	"justice"	)
OR CONTAINS(LOWER([result_title_anthology]),	"freedom"	)
OR CONTAINS(LOWER([result_title_anthology]),	"security"	)

OR CONTAINS(LOWER([result_title_anthology]),	"poverty"	)
OR CONTAINS(LOWER([result_title_anthology]),	"microfinance"	)
OR CONTAINS(LOWER([result_title_anthology]),	"microcredit"	)
OR CONTAINS(LOWER([result_title_anthology]),	"debt"	)
OR CONTAINS(LOWER([result_title_anthology]),	"financial inclusion"	)
OR CONTAINS(LOWER([result_title_anthology]),	"beggar"	)
OR CONTAINS(LOWER([result_title_anthology]),	"begging"	)
OR CONTAINS(LOWER([result_title_anthology]),	"homeless"	)
OR CONTAINS(LOWER([result_title_anthology]),	"slave"	)
OR CONTAINS(LOWER([result_title_anthology]),	"disadvantaged"	)
OR CONTAINS(LOWER([result_title_anthology]),	"social class"	)
OR CONTAINS(LOWER([result_title_anthology]),	"social sustainab"	)
OR CONTAINS(LOWER([result_title_anthology]),	"social welfare"	)
OR CONTAINS(LOWER([result_title_anthology]),	"social security"	)
OR CONTAINS(LOWER([result_title_anthology]),	"social policy"	)

OR CONTAINS(LOWER([result_title_anthology]),	"women"	)
OR CONTAINS(LOWER([result_title_anthology]),	"girls"	)
OR CONTAINS(LOWER([result_title_anthology]),	"gender"	)
OR CONTAINS(LOWER([result_title_anthology]),	"sexism"	)
 OR CONTAINS(LOWER([scientific_field_npi]),	"kjønnsforskning"	)
OR CONTAINS(LOWER([result_title_anthology]),	"homophob"	)
OR CONTAINS(LOWER([result_title_anthology]),	"gay"	)
OR CONTAINS(LOWER([result_title_anthology]),	"lesbian"	)
OR CONTAINS(LOWER([result_title_anthology]),	"bisexual"	)
OR CONTAINS(LOWER([result_title_anthology]),	"transgender"	)
OR CONTAINS(LOWER([result_title_anthology]),	"queer"	)
OR CONTAINS(LOWER([result_title_anthology]),	"LGBT"	)
OR CONTAINS(LOWER([result_title_anthology]),	"ageism"	)
OR CONTAINS(LOWER([result_title_anthology]),	"disab"	)
OR CONTAINS(LOWER([result_title_anthology]),	"intersectional"	)
))		
THEN "migration and inequality"		


ELSEIF ((		
CONTAINS(LOWER([result_title_anthology]),	"smuggling"	)
OR CONTAINS(LOWER([result_title_anthology]),	"trafficking"	)
)		
AND (		
CONTAINS(LOWER([result_title_anthology]),	"victim"	)
OR CONTAINS(LOWER([result_title_anthology]),	"human"	)
OR CONTAINS(LOWER([result_title_anthology]),	"people"	)
OR CONTAINS(LOWER([result_title_anthology]),	"child"	)
OR CONTAINS(LOWER([result_title_anthology]),	"slave"	)
))		
THEN "migration and inequality"		


ELSE "non"
END
```

## CC in LMCs

This section covers:
* Climate change and low and middle income countries (LMCs).
* Farming in LMCs
* Food security (all countries).

Note that climate change as related to the three main focus areas is already included under those sections - anything mentioning health and climate change (global health), specific groups of people/justice and climate change (inequality), or migrants/refugees and climate change (migration) will already be covered there. Other aspects of climate change research is not covered by this search string, but by the KE satsningsområde. 

Note that in the WoS version of this string, I have expanded farming to include more terms ("food production" OR "agriculture" OR "aquaculture" OR "smallhold*"). Aquaculture was added here in 2022.

```Ceylon =
IF ((		
CONTAINS(LOWER([result_title]),	"climate chang"	)
OR CONTAINS(LOWER([result_title_anthology]),	"climate chang"	)
OR CONTAINS(LOWER([result_title]),	"global chang"	)
OR CONTAINS(LOWER([result_title_anthology]),	"global chang"	)
OR CONTAINS(LOWER([result_title]),	"climatic chang"	)
OR CONTAINS(LOWER([result_title]),	"changing climate"	)
OR CONTAINS(LOWER([result_title]),	"global warming"	)
OR CONTAINS(LOWER([result_title]),	"climate extreme"	)
OR CONTAINS(LOWER([result_title]),	"extreme climate"	)
OR CONTAINS(LOWER([result_title]),	"heat wave"	)
OR CONTAINS(LOWER([result_title]),	"disaster"	)
OR CONTAINS(LOWER([result_title]),	"farming"	)
OR CONTAINS(LOWER([Result Title]),	"farming"	)
OR CONTAINS(LOWER([Result Title]),	"landbruk"	)
OR CONTAINS(LOWER([Result Title]),	"aquacultur"	)
OR CONTAINS(LOWER([Result Title]),	"akvakultur"	)
)		
AND (		
CONTAINS(LOWER([result_title]),	"developing count" 	)
OR CONTAINS(LOWER([result_title]),	"developing state" 	)
OR CONTAINS(LOWER([result_title]),	"afghanistan"	)
OR CONTAINS(LOWER([result_title]),	"angola" 	)
OR CONTAINS(LOWER([result_title]),	"bangladesh" 	)
OR CONTAINS(LOWER([result_title]),	"bhutan" 	)
OR CONTAINS(LOWER([result_title]),	"burkina faso" 	)
OR CONTAINS(LOWER([result_title]),	"burundi" 	)
OR CONTAINS(LOWER([result_title]),	"cambodia" 	)
OR CONTAINS(LOWER([result_title]),	"congo" 	)
OR CONTAINS(LOWER([result_title]),	"cuba" 	)
OR CONTAINS(LOWER([result_title]),	"eritrea" 	)
OR CONTAINS(LOWER([result_title]),	"ethiopia" 	)
OR CONTAINS(LOWER([result_title]),	"gambia" 	)
OR CONTAINS(LOWER([result_title]),	"haiti" 	)
OR CONTAINS(LOWER([result_title]),	"jamaica" 	)
OR CONTAINS(LOWER([result_title]),	"liberia" 	)
OR CONTAINS(LOWER([result_title]),	"madagascar" 	)
OR CONTAINS(LOWER([result_title]),	"malawi" 	)
OR CONTAINS(LOWER([result_title]),	"maldives" 	)
OR CONTAINS(LOWER([result_title]),	" mali " 	)
OR CONTAINS(LOWER([result_title]),	"mauritius" 	)
OR CONTAINS(LOWER([result_title]),	"mozambique" 	)
OR CONTAINS(LOWER([result_title]),	"myanmar" 	)
OR CONTAINS(LOWER([result_title]),	"nepal" 	)
OR CONTAINS(LOWER([result_title]),	"papua new guinea" 	)
OR CONTAINS(LOWER([result_title]),	"rwanda" 	)
OR CONTAINS(LOWER([result_title]),	"la reunion" 	)
OR CONTAINS(LOWER([result_title]),	"samoa" 	)
OR CONTAINS(LOWER([result_title]),	"sierra leone" 	)
OR CONTAINS(LOWER([result_title]),	"somalia" 	)
OR CONTAINS(LOWER([result_title]),	"sudan" 	)
OR CONTAINS(LOWER([result_title]),	"tanzania" 	)
OR CONTAINS(LOWER([result_title]),	"timor leste" 	)
OR CONTAINS(LOWER([result_title]),	"timor-leste" 	)
OR CONTAINS(LOWER([result_title]),	"tuvalu" 	)
OR CONTAINS(LOWER([result_title]),	"uganda" 	)
OR CONTAINS(LOWER([result_title]),	"yemen" 	)
OR CONTAINS(LOWER([result_title]),	"zambia" 	)
OR CONTAINS(LOWER([result_title]),	"africa" 	)
OR CONTAINS(LOWER([result_title]),	"nigeria"	)
OR CONTAINS(LOWER([result_title]),	"egypt"	)
OR CONTAINS(LOWER([result_title]),	"kenya"	)
OR CONTAINS(LOWER([result_title]),	"algeria"	)
OR CONTAINS(LOWER([result_title]),	"morocco"	)
OR CONTAINS(LOWER([result_title]),	"ghana"	)
OR CONTAINS(LOWER([result_title]),	"cameroon"	)
OR CONTAINS(LOWER([result_title]),	"zimbabwe"	)
OR CONTAINS(LOWER([result_title]),	"tunisia"	)
OR CONTAINS(LOWER([result_title]),	"libya"	)
OR CONTAINS(LOWER([result_title]),	"botswana"	)
OR CONTAINS(LOWER([result_title]),	"equatorial guinea"	)
OR CONTAINS(LOWER([result_title]),	"albania"	)
OR CONTAINS(LOWER([result_title]),	"argentina"	)
OR CONTAINS(LOWER([result_title]),	"armenia"	)
OR CONTAINS(LOWER([result_title]),	"azerbaijan"	)
OR CONTAINS(LOWER([result_title]),	"belarus"	)
OR CONTAINS(LOWER([result_title]),	"bolivia"	)
OR CONTAINS(LOWER([result_title]),	"bosnia"	)
OR CONTAINS(LOWER([result_title]),	"brazil"	)
OR CONTAINS(LOWER([result_title]),	"bulgaria"	)
OR CONTAINS(LOWER([result_title]),	"china"	)
OR CONTAINS(LOWER([result_title]),	"colombia"	)
OR CONTAINS(LOWER([result_title]),	"costa rica"	)
OR CONTAINS(LOWER([result_title]),	"ecuador"	)
OR CONTAINS(LOWER([result_title]),	"el salvador"	)
OR CONTAINS(LOWER([result_title]),	"guatemala"	)
OR CONTAINS(LOWER([result_title]),	"honduras"	)
OR CONTAINS(LOWER([result_title]),	"india"	)
OR CONTAINS(LOWER([result_title]),	"indonesia"	)
OR CONTAINS(LOWER([result_title]),	"iran"	)
OR CONTAINS(LOWER([result_title]),	"iraq"	)
OR CONTAINS(LOWER([result_title]),	"jordan"	)
OR CONTAINS(LOWER([result_title]),	"kazakhstan"	)
OR CONTAINS(LOWER([result_title]),	"kosovo"	)
OR CONTAINS(LOWER([result_title]),	"kyrgyz"	)
OR CONTAINS(LOWER([result_title]),	"lebanon"	)
OR CONTAINS(LOWER([result_title]),	"malaysia"	)
OR CONTAINS(LOWER([result_title]),	"mexico"	)
OR CONTAINS(LOWER([result_title]),	"micronesia"	)
OR CONTAINS(LOWER([result_title]),	"moldova"	)
OR CONTAINS(LOWER([result_title]),	"mongolia"	)
OR CONTAINS(LOWER([result_title]),	"montenegro"	)
OR CONTAINS(LOWER([result_title]),	"nicaragua"	)
OR CONTAINS(LOWER([result_title]),	"macedonia"	)
OR CONTAINS(LOWER([result_title]),	"pakistan"	)
OR CONTAINS(LOWER([result_title]),	"paraguay"	)
OR CONTAINS(LOWER([result_title]),	"phillipines"	)
OR CONTAINS(LOWER([result_title]),	"peru"	)
OR CONTAINS(LOWER([result_title]),	"romania"	)
OR CONTAINS(LOWER([result_title]),	"russia"	)
OR CONTAINS(LOWER([result_title]),	"serbia"	)
OR CONTAINS(LOWER([result_title]),	"sri lanka"	)
OR CONTAINS(LOWER([result_title]),	"syria"	)
OR CONTAINS(LOWER([result_title]),	"tajikistan"	)
OR CONTAINS(LOWER([result_title]),	"thailand"	)
OR CONTAINS(LOWER([result_title]),	"turkey"	)
OR CONTAINS(LOWER([result_title]),	"turkmenistan"	)
OR CONTAINS(LOWER([result_title]),	"ukraine"	)
OR CONTAINS(LOWER([result_title]),	"venezuela"	)
OR CONTAINS(LOWER([result_title]),	"vietnam"	)
OR CONTAINS(LOWER([result_title]),	"west bank"	)
OR CONTAINS(LOWER([result_title]),	" gaza"	)
))		
THEN "climate"

ELSEIF 		
CONTAINS(LOWER([result_title]),	"right to food"	)
OR CONTAINS(LOWER([result_title]),	"right to water"	)
OR CONTAINS(LOWER([result_title]),	"matsikkerhet"	)
OR CONTAINS(LOWER([result_title]),	"smallhold"	)
OR CONTAINS(LOWER([result_title]),	"small-hold"	)
THEN "climate"

ELSEIF ((		
CONTAINS(LOWER([result_title]),	"food"	)
OR CONTAINS(LOWER([result_title]),	"water"	)
)		
AND (		
CONTAINS(LOWER([result_title]),	"access"	)
OR CONTAINS(LOWER([result_title]),	"security"	)
OR CONTAINS(LOWER([result_title]),	"resilience"	)
))		
THEN "climate"

ELSE "non"
END
```
