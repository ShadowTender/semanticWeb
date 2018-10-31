# Semantic Web Project 1
- Fei Liang - fei.liang@telecom-paristech.fr
- Li Xu - li.xu@telecom-paristech.fr
- Zhehui Bao - asasopo1@gmail.com

## Question 1
> Are lobsters spiders ?

```
endPoint: https://query.wikidata.org/sparql
```

1. Get the parent class of spider (wd:Q1357), which is wd:Q1358
```
select * from { 
  wd:Q1357 wdt:P171 ?d. 
}
```
Output is 
```
d: wd:Q1358
```

2. Get the parent class of wd:Q1358, which is wd:Q1359
`
select * from { 
  wd:Q1358 wdt:P171 ?d. 
}
`
Output is 
`
d
wd:Q1359
`

3. Ask if Lobster is an instance of Q1359 or Q1358
```
ASK { 
	wd:Q3621241 wdt:P171 wd:Q1359.
}
```
Output is
```
false
```

4. Ask if Lobster is an instance of  Q1358
```
ASK { 
	wd:Q3621241 wdt:P171 wd:Q1358. 
}
```
Output is 
```
false
```
5. Ask if Lobster is an instance of  spiders
```
ASK { 
	wd:Q3621241 wdt:P171 wd:Q1357. 
}
```
Output is 
```
false
```

## Question 2
> Chinese famous male athletes

```
endPoint: https://query.wikidata.org/sparql
```

1. Select Query
```
SELECT ?itemLabel ?itemDescription (SAMPLE(?dob) AS ?dob) ?sl WHERE {
  		?item wdt:P106 wd:Q2066131.
  		?item wdt:P27 wd:Q148.
 		 ?item wdt:P21 wd:Q6581097.
 		 MINUS { ?item wdt:P570 _:b0. }
  		OPTIONAL { ?item wdt:P569 ?dob. }
  		OPTIONAL { ?item wikibase:sitelinks ?sl. }
  		SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en". }
}
GROUP BY ?item ?itemLabel ?itemDescription ?sl
ORDER BY DESC(?sl)
LIMIT 20
```

Output:
```
[
   {
      "itemLabel":"李连杰",
      "itemDescription":"中国演员",
      "dob":"1963-04-26T00:00:00Z",
      "sl":"107"
   },
   {
      "itemLabel":"罗杰·袁",
      "itemDescription":"美国演员",
      "dob":"1961-01-25T00:00:00Z",
      "sl":"7"
   },
   {
      "itemLabel":"杨昊",
      "itemDescription":"中国跳水运动员",
      "dob":"1998-02-03T00:00:00Z",
      "sl":"7"
   },
   {
      "itemLabel":"天兵",
      "dob":"1994-04-14T00:00:00Z",
      "sl":"6"
   },
   {
      "itemLabel":"许银川",
      "itemDescription":"Xiangqi players",
      "dob":"1975-08-01T00:00:00Z",
      "sl":"5"
   },
   {
      "itemLabel":"王心迪",
      "itemDescription":"自由式滑雪运动员",
      "dob":"1995-05-02T00:00:00Z",
      "sl":"5"
   },
   {
      "itemLabel":"陈正雷",
      "itemDescription":"中国太极拳家",
      "dob":"1949-05-15T00:00:00Z",
      "sl":"4"
   },
   {
      "itemLabel":"Wáng Xī' An",
      "dob":"1944-01-01T00:00:00Z",
      "sl":"4"
   },
   {
      "itemLabel":"释德杨",
      "itemDescription":"中国佛教高僧",
      "dob":"1968-07-16T00:00:00Z",
      "sl":"4"
   },
   {
      "itemLabel":"Wang Qiang",
      "dob":"1993-04-23T00:00:00Z",
      "sl":"4"
   },
   {
      "itemLabel":"孙炜",
      "itemDescription":"中国棒球运动员",
      "dob":"1976-09-11T00:00:00Z",
      "sl":"3"
   },
   {
      "itemLabel":"常振明",
      "itemDescription":"中国企业家",
      "dob":"1956-10-01T00:00:00Z",
      "sl":"3"
   },
   {
      "itemLabel":"柳大華",
      "dob":"1950-01-01T00:00:00Z",
      "sl":"3"
   },
   {
      "itemLabel":"陳芴",
      "dob":"1924-12-31T00:00:00Z",
      "sl":"3"
   },
   {
      "itemLabel":"吳道源",
      "dob":"1934-12-04T00:00:00Z",
      "sl":"3"
   },
   {
      "itemLabel":"Gao Xin",
      "itemDescription":"Chinese tennis player",
      "dob":"1994-05-12T00:00:00Z",
      "sl":"3"
   },
   {
      "itemLabel":"鄭俊樑",
      "itemDescription":"香港男子滑浪風帆運動員",
      "dob":"1994-04-30T00:00:00Z",
      "sl":"3"
   },
   {
      "itemLabel":"卢卓",
      "itemDescription":"中国速滑运动员",
      "dob":"1980-11-18T00:00:00Z",
      "sl":"2"
   },
   {
      "itemLabel":"李雨",
      "itemDescription":"中国速滑运动员",
      "dob":"1976-03-16T00:00:00Z",
      "sl":"2"
   },
   {
      "itemLabel":"黄良财",
      "itemDescription":"中国击剑运动员",
      "dob":"1984-07-25T00:00:00Z",
      "sl":"2"
   }
]
```

2. Construct Query
```
CONSTRUCT {
 		 ?item wdt:P106 wd:Q2066131.
}
WHERE {
		?item wdt:P106 wd:Q2066131.
  		?item wdt:P27 wd:Q148.
  		?item wdt:P21 wd:Q6581097.
  		MINUS { ?item wdt:P570 _:b0. }
 		 OPTIONAL { ?item wdt:P569 ?dob. }
 		 OPTIONAL { ?item wikibase:sitelinks ?sl. }
 		 SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en". }
}
LIMIT 20
```

Output
```
[
   {
      "subject":"http://www.wikidata.org/entity/Q159577",
      "predicate":"http://www.wikidata.org/prop/direct/P106",
      "object":"http://www.wikidata.org/entity/Q2066131"
   },
   {
      "subject":"http://www.wikidata.org/entity/Q855682",
      "predicate":"http://www.wikidata.org/prop/direct/P106",
      "object":"http://www.wikidata.org/entity/Q2066131"
   },
   {
      "subject":"http://www.wikidata.org/entity/Q1069813",
      "predicate":"http://www.wikidata.org/prop/direct/P106",
      "object":"http://www.wikidata.org/entity/Q2066131"
   },
   {
      "subject":"http://www.wikidata.org/entity/Q1435207",
      "predicate":"http://www.wikidata.org/prop/direct/P106",
      "object":"http://www.wikidata.org/entity/Q2066131"
   },
   {
      "subject":"http://www.wikidata.org/entity/Q1751567",
      "predicate":"http://www.wikidata.org/prop/direct/P106",
      "object":"http://www.wikidata.org/entity/Q2066131"
   },
   {
      "subject":"http://www.wikidata.org/entity/Q1800658",
      "predicate":"http://www.wikidata.org/prop/direct/P106",
      "object":"http://www.wikidata.org/entity/Q2066131"
   },
   {
      "subject":"http://www.wikidata.org/entity/Q2171430",
      "predicate":"http://www.wikidata.org/prop/direct/P106",
      "object":"http://www.wikidata.org/entity/Q2066131"
   },
   {
      "subject":"http://www.wikidata.org/entity/Q2365865",
      "predicate":"http://www.wikidata.org/prop/direct/P106",
      "object":"http://www.wikidata.org/entity/Q2066131"
   },
   {
      "subject":"http://www.wikidata.org/entity/Q2545453",
      "predicate":"http://www.wikidata.org/prop/direct/P106",
      "object":"http://www.wikidata.org/entity/Q2066131"
   },
   {
      "subject":"http://www.wikidata.org/entity/Q2581526",
      "predicate":"http://www.wikidata.org/prop/direct/P106",
      "object":"http://www.wikidata.org/entity/Q2066131"
   },
   {
      "subject":"http://www.wikidata.org/entity/Q3566097",
      "predicate":"http://www.wikidata.org/prop/direct/P106",
      "object":"http://www.wikidata.org/entity/Q2066131"
   },
   {
      "subject":"http://www.wikidata.org/entity/Q3787371",
      "predicate":"http://www.wikidata.org/prop/direct/P106",
      "object":"http://www.wikidata.org/entity/Q2066131"
   },
   {
      "subject":"http://www.wikidata.org/entity/Q4017665",
      "predicate":"http://www.wikidata.org/prop/direct/P106",
      "object":"http://www.wikidata.org/entity/Q2066131"
   },
   {
      "subject":"http://www.wikidata.org/entity/Q4024360",
      "predicate":"http://www.wikidata.org/prop/direct/P106",
      "object":"http://www.wikidata.org/entity/Q2066131"
   },
   {
      "subject":"http://www.wikidata.org/entity/Q4778557",
      "predicate":"http://www.wikidata.org/prop/direct/P106",
      "object":"http://www.wikidata.org/entity/Q2066131"
   },
   {
      "subject":"http://www.wikidata.org/entity/Q4809088",
      "predicate":"http://www.wikidata.org/prop/direct/P106",
      "object":"http://www.wikidata.org/entity/Q2066131"
   },
   {
      "subject":"http://www.wikidata.org/entity/Q5071692",
      "predicate":"http://www.wikidata.org/prop/direct/P106",
      "object":"http://www.wikidata.org/entity/Q2066131"
   },
   {
      "subject":"http://www.wikidata.org/entity/Q5651481",
      "predicate":"http://www.wikidata.org/prop/direct/P106",
      "object":"http://www.wikidata.org/entity/Q2066131"
   },
   {
      "subject":"http://www.wikidata.org/entity/Q5698523",
      "predicate":"http://www.wikidata.org/prop/direct/P106",
      "object":"http://www.wikidata.org/entity/Q2066131"
   },
   {
      "subject":"http://www.wikidata.org/entity/Q6581602",
      "predicate":"http://www.wikidata.org/prop/direct/P106",
      "object":"http://www.wikidata.org/entity/Q2066131"
   }
]
```