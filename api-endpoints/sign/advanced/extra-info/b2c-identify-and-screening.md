# Aml person sanction/pep

Person screening with data enhancement enabled for nationalities where data enhancement is provided. For other nationalities the data enhancement will be skipped.

## Example request \(Create document request\)

```text
{
    ....
    "advanced": {
        ...
            "extraInfo": {
                "types": ["amlB2cIdentifyAndScreening"],
                "specialProperties": {
                    "amlMode": "identify_and_screen"
                }

            }

        ...        
    }
    ....
}
```

## Example response \(get document\)

```text
{
    ...
    "signers": [
        ...
        "links" : [{
            "href": "https://api.idfy.io/blablabla",
            "rel": "amlB2cIdentifyAndScreening",
            "type": "GET"
        }]
        ...
    ]
    ...   
}
```

## Example data \(Retrieved from links array on signer in response\)

```text
{
  "sanctionResults": [
    {
      "matchIndicator": 325,
      "comment": "(Mother’s name: Masouma Abd al-Rahman. Photo available for inclusion in the INTERPOL-UN Security Council Special Notice)",
      "aliasList": [
        "Najmuddin Faraj Ahmad",
        "Mullah Krekar",
        "Fateh Najm Eddine Farraj",
        "Faraj Ahmad Najmuddin"
      ],
      "addressList": [
        {
          "countryName": "Iraq",
          "countryCode": "IQ"
        },
        {
          "countryName": "Norway",
          "countryCode": "NO",
          "street": "10 Testesensgate",
          "postCode": "0101",
          "city": "Oslo"
        }
      ],
      "urlList": [
        "http://eur-lex.europa.eu/LexUriServ/LexUriServ.do?uri=OJ:L:2006:351:0009:0010:EN:PDF"
      ],
      "provider": "TRAPETS",
      "source": "EU_GLOBAL",
      "externalId": "3641",
      "lastUpdate": "2016-12-15T00:00:00",
      "firstUpdate": "2016-01-19T00:00:00",
      "name": "Najmuddin Faraj Ahmad",
      "gender": "UNKNOWN",
      "birthDate": "1956-07-07"
    },
    {
      "matchIndicator": 325,
      "comment": "Mother’s name: Masouma Abd al-Rahman. Photo available for inclusion in the INTERPOL-UN Security Council Special Notice. Review pursuant to Security Council resolution 1822 (2008) was concluded on 20 May 2010.",
      "aliasList": [
        "Mullah Krekar",
        "Fateh Najm Eddine Farraj",
        "Faraj Ahmad Najmuddin",
        "NAJMUDDIN FARAJ AHMAD "
      ],
      "addressList": [
        {
          "countryName": "Iraq",
          "countryCode": "IQ"
        },
        {
          "countryName": "Iraq",
          "countryCode": "IQ",
          "street": "Olaqloo Sharbajer"
        },
        {
          "countryName": "Norway",
          "countryCode": "NO",
          "street": "Testesensgate 1",
          "postCode": "0101",
          "city": "Oslo"
        }
      ],
      "provider": "TRAPETS",
      "source": "UN_CONSOLIDATED_1",
      "externalId": "2762998",
      "lastUpdate": "2016-12-15T00:00:00",
      "firstUpdate": "2006-12-07T00:00:00",
      "name": "Mullah Krekar",
      "gender": "UNKNOWN",
      "birthDate": "1956-07-07"
    }
  ],
  "pepResults": [
    {
      "matchIndicator": 500,
      "title": "Minister for Infrastructure",
      "aliasList": [
        "Anna Frida Wiktoria Johansson"
      ],
      "addressList": [
        {
          "countryName": "Sweden",
          "countryCode": "SE"
        }
      ],
      "urlList": [
        "http://www.government.se/government-of-sweden/ministry-of-enterprise-and-innovation/anna-johansson/",
        "https://sv.wikipedia.org/wiki/Anna_Johansson_(socialdemokrat)"
      ],
      "provider": "TRAPETS",
      "source": "PEP_Edge",
      "externalId": "SE.Government-372",
      "lastUpdate": "2016-12-15T00:00:00",
      "name": "Anna Frida Wiktoria Johansson",
      "gender": "UNKNOWN",
      "birthDate": "1971-05-29"
    }
  ],
  "verifiedPerson": {
    "provider": "BISNODE",
    "name": "Anna Frida Wiktoria Johansson",
    "gender": "FEMALE",
    "natIdNo": "195001011234",
    "nationality": "NO",
    "birthDate": "1971-05-29"
  },
  "message": "NO MESSAGE",
  "Report": "reference to PDF report, sealed and timestamped."
}
```

## Full response model

[https://developer.idfy.io/api\#operation/B2CIdentifyAndScreeningRequest](https://developer.idfy.io/api#operation/B2CIdentifyAndScreeningRequest)

