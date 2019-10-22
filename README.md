# Previo - test project

There is a list of reservations in JSON saved in file reservations.json. The content of the file is:

```json
[  
   {  
      "reservationId":123456,
      "guest":"Petr Klas",
      "room":"Double room",
      "type": "day",
      "prices":{  
         "2019-05-01":"25.3",
         "2019-05-02":"25.3",
         "2019-05-03":"25.3",
         "2019-05-04":"25.3"
      },
      "currency":"EUR",
      "alreadyPaid":"50"
   },
   {  
      "reservationId":569833,
      "guest":"Miro Zbirka",
      "room":"Sauna",
      "type": "hour",
      "prices":{  
         "2019-06-08T14:00:00":"900",
         "2019-06-08T15:00:00":"800",
         "2019-06-08T16:00:00":"800",
         "2019-06-08T17:00:00":"800",
      },
      "currency":"CZK",
      "alreadyPaid":"500" 
   }
]
```

Kde "type" je typ rezervace (day je rezervace na dny a hour je rezervace na hodiny) "prices" jsou ceny rezervace za každou noc / hodinu zvlášť. 
"alreadyPaid" je částka, která již byla klientem uhrazena


Vaším úkolem bude napsat co nejlépe objektově funkcionalitu, která soubor přečte, zpracuje a vytvoří JSON soubor "reservations_transformed.json" s výstupem pro všechny rezervace v tomto formátu:
```json
[  
   {  
      "reservationId":123456,
      "firstName":"Petr",
      "lastName":"Klas",
      "room":"Double room",
      "term":{  
         "from":"2019-05-01",
         "to":"2019-05-05", 
         "nights":4
      },
      "priceToBePaid":[  
         {  
            "currency":"CZK",
            "price":"1331.2"
         },
         {  
            "currency":"EUR",
            "price":"21.2"
         }
      ]
   },
   {  
      "reservationId":569833,
      "firstName":"Miro",
      "lastName":"Zbirka",
      "room":"Sauna",
      "term":{  
         "from":"2019-06-08T14:00:00",
         "to":"2019-06-08T17:00:00", 
         "hours":4
      },
      "priceToBePaid":[  
         {  
            "currency":"CZK",
            "price":"2800"
         },
         {  
            "currency":"EUR",
            "price":"107.69"
         }
      ]
   }
]
```

To znamená, že z denních / hodinových cen si vypočte datum OD a DO (datum DO je vždy o 1 větší než poslední denní cena v případě dnů) a počet nocí / hodin. A ze sumy denních cen a zaplacené částky udělá částku k zaplacení, která bude vždy v CZK i EUR měně. Do požadované měny přepočtěte částky kurzem 1 EUR = 26 CZK.

V uvedeném případě je tedy priceToBePaid vypočtena jako:

25,3 * 4  = 101,2 - 50 = 51,2 EUR

51,2 EUR * 26 = 1331,2 Kč.

Tento JSON výstup navíc uložte do souboru s názvem reservations.json do adresáře /tmp.

Pokuste se celé řešení napsat co nejlépe objektově (využitím interface, abstract classed, traits, ...), myslete i na ošetření různých chybových stavů.
