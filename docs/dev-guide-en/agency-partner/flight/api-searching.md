
## Get airport list API

!!! info "GET: /metasrv/api/_search/airports"
    Search for airports by relevant keywords or country/region codes
    Allows to sort the returned results

### Parameter

| Parameter | Description |
| --- | --- |
| query query (String, Optional) | Search keyword area / airport name (eg: SGN, Vietnam, Tokyo) |
| country query (String, Optional) | Country/Region Code (Example: VN) |
| page query (Integer, Optional) | Number of pages you want to get results (eg: 0) |
| size query (Integer, Optional) | Number of results you want to get in 1 page (eg 20) |
| sort query(String, Optional) | Sort the results by the value of the returned property ascending or descending (eg: propertiesName,desc / propertiesName,asc) |

=== "Example"
    ?query=`ha`&country=`VN`&page=`0`&size=`20`&sort=`name,desc`

### Response

=== "Model"

| Parameter | Description |
| --- | --- |
|          Array\[AirportDTO\] (Optional) | Return airport list information |
|          id (Long, Optional) | Airport List Identifier |
|          code(String, Optional) | Airport code |
|          name(String, Optional) | Airport name |
|          cityCode(String, Optional) | City symbol code |
|          city(String, Optional) | City name |
|          countryCode(String, Optional) | Country symbol code |
|          country(String, Optional) | Country name |
|          timeZone(Integer, Optional) | Time zone |
|          location(String, Optional) | Location name |
|          name2(String, Optional) | English airport name (other name) |
|          city2(String, Optional) | English city name (other name) |

=== "Example"
    ```json

    [
        {
            "id": 4,
            "code": "SGN",
            "name": "Sân bay Tân Sơn Nhất",
            "cityCode": "SGN",
            "city": "Hồ Chí Minh",
            "countryCode": "VN",
            "country": "Vietnam",
            "iata": "SGN",
            "groupName": "Popular,INT_VN,Vietnam",
            "name2": "Tansonnhat Intl",
            "city2": "Ho Chi Minh City",
            "location": "Tp. Hồ Chí Minh",
            "timezone": 7,
            "index": 2,
            "icao": null,
            "latitude": null,
            "longitude": null,
            "altitude": null,
            "dts": null,
            "tzTimezone": null,
            "updatedAt": null,
            "connectedPorts": null,
            "stateCode": null,
            "status": null,
            "keywords": null
        }
    ]

    ```

## Search flight ticket API

!!! info "GET: /api/air-tickets/low-fare-search-async"

    Search for flights by departure and end points / by date and time

### Parameter

| Parameter | Description |
| --- | --- |
| origin_code query (String, Required) | Departure airport code
Example: The airport in Ho Chi Minh has the code SGN |
| destination_code query (String, Required) | Destination airport code
For example, the airport in Hanoi has the code HAN . |
| departure_date query (String, Required) | Departure day
Format in MM-dd-YYYY
Example: 07-07-2021 |
| returnure_date query (String, Required) | Return day
Format in MM-dd-YYYY
Example: 08-20-2021 |
| cabin_class query (String, Required) | Ticket class
Pass the value as E |
| route_type query (String, Optional) | Journey type:
- Oneway: One-way
- ROUNDTRIP: Round trip
  If not transmitted, the value is ONEWAY . |
  | aduts_qtt query (Integer, Optional) | Number of adult passengers (12 years old and above)
  Otherwise, the default value is 1 . |
  | children_qtt query (Integer, Optional) | Number of passengers who are children (from 2 years old and under 12 years old)
  Otherwise, the default value is 0 |
  | infant_qtt query (Integer, Optional) | Number of passengers who are infants (under 2 years old)
  Otherwise, the default value is 0 |
  | time query(String, Optional) | API Call Time (UnixTimeStamp)
  Example: 1625545845 |
  | key query (String, Optional) | Key to checksum. How to create value:MAC-SHA256(<origin_code><destination_code><departure_time><returnure_date><cabin_class><route_type><aduts_qtt><children_qtt><infant_qtt><page><size><time>, 'Gotadi') |
| include-equivfare query (Boolean, Optional) | Request to pay additional ticketing fee information (EquivFare) |
| page query (Integer, Optional) | Number of pages you want to get results (eg: 0) |
| size query (Integer, Optional) | Number of results you want to get in 1 page (eg 20) |
| sort query(String, Optional) | Sort the results by the value of the returned property ascending or descending (eg: propertiesName,desc / propertiesName,asc) |

=== "Example"
    ?origin_code=`SGN`&destination_code=`HAN`&departure_date=`07-21-2021`&returnture_date=`07-28-2021`&cabin_class=`E`&route_type=`ROUNDTRIP`&aduts_qtt=`1`&children_qtt=`0`&infants_qtt=`0`&time=`1625552814666`&key=`/xNr15RmY0dqSUkhvpKI1bIbKIuyZr1Q38rLi3bqxVk`=&page=`0`&size=`15`

### Response

=== "Model"

| Parameter | Description |
| --- | --- |
| searchId(String, Required) | The reference code to the search for air tickets, taken from the search results for air tickets |
| departureSearchId(String, Required) | Reference code to search for flight tickets
Retrieved from searchId |
| returnSearchId(String, Required) | Reference code to search for air tickets
Derived from searchID combined with -R at the end |
| groupPricedItineraries (Array[GroupPricedItineraryDTO], Optional) | Information about the list of journeys returned by search results |
|       airSupplier(String, Required) | Carriers (VietnamAirline - VNA, VjetJet - VJ, BamBoo - QH, ...) |
|       aircraft (String, Optional) | Type of aircraft (Airbus A330, Boeing 787, .....) |
|       airline(String, Optional) | Airlines (VJ, VNA, ...) |
|       airlineName(String, Optional) | Name of airline (Vietjet Air, Vietnam Airlines, Bamboo, ...) |
|       arrivalDateTime(String, Required) | Arrival date and time, using UTC/GMT+7 time zone |
|       departureDateTime (String, Required) | Split flight time, using UTC/GMT+7 time zone |
|       destinationLocationCode (String, Optional) | Flight end city code |
|       destinationCountry(String, Optional) | The name of the country where the flight ended |
|       destinationCountryCode (String, Optional) | Flight end country code |
|       destinationCity(String, Optional) | The name of the city where the flight ends |
|       destinationLocationName (String, Optional) | Airport name where the flight ends |
|       flightNo(String, Optional) | Airplane number |
|       flightNo(String, Optional) | Airplane number |
|       flightType(String, Optional) | Type of flight domestic or international?
Flight type:
DOMESTIC: domestic
INTERNATIONAL: international |
|       groupId(String, Required) | Journey identifier in the list of journeys returned by search results |
|       originCity(String, Optional) | City name at departure point |
|       originCountry(String, Optional) | Country name at departure point |
|       originCountryCode(String, Optional) | Country code at departure point |
|       originLocationCode(String, Optional) | Flight departure city code |
|       originLocationName(String, Optional) | Airport name at departure point |
|       totalPricedItinerary (Integer, Required) | Total number of detailed journeys |
|       pricedItineraries (Array[PricedItineraries], Required) | Itinerary details |
|             airItineraryPricingInfo (AirItineraryPricingInfo, Required) | Detailed price information of the itinerary |
|                   adultFare (FareBreakdown, Required) |  |
|                         passengerFare (PassengerFare, Required) | Adult fare information |
|                                baseFare(FareInfo, required) | Basic fare information |
|                                        amount (Double, Required) | Amount of money |
|                                        decimalPlaces(Integer, Optional) | Decimal places rounded to |
|                                equivFare (FareInfo, Optional) | Similar to baseFare
Ticketing fee information |
|                                serviceTax (FareInfo, Required) | Similar to baseFare
Service fee information |
|                                totalFare (FareInfo, Required)  | Similar to baseFare
Total ticket price information |
|                                surcharges (Array[Surcharge], Required) | Information about surcharges per booking / per segment |
|                         passengerTypeQuantities (PassengerTypeQuantities, Optional) | Number/type of passengers |
|                                code(String, Required) | Adult/Child/Infant Identifier
Includes: ADT - adult / CHD - child / INF - infant |
|                                quantity (Integer, Required) | Number of adults / children / infants |
|                   childFare(PassengerFare, Optional) | Child fare information
Similar to adult fare information |
|                   infantFare (PassengerFare, Optional) | Infant fare information
Similar to adult fare information |
|                   itinTotalFare (PassengerFare, Required) | Total fare information of the journey
Similar to adult fare information |
|                   fareSourceCode(String, Required) | Journey identifier information
Used to get ticket condition information |
|       allowHold (Boolean, Required) | Information to allow to hold a reservation or not |
|       cabinClassName(String, Required) | Seat class information:
ECONOMY - universal seat
PREMIUM - special economy seat
BUSINESS - business chair |
|       fightNo(String, Optional) | Displays aircraft number information |
|       originDestinationOptions (Array(OriginDestinationOptions), Required) | Cruise's blocking/stopping information |
|             flightDirection(String, Required) | Show flight direction information of the journey
D - departure direction
R - return direction |
|             journeyDuration (Integer, Required) | Show flight time |
|             flightSegments (Array(FlightSegments), Required) | Show detailed information of departure / end points in the journey |
| page (AirPage, Required) | Object that describes information about pagination.
Sequence number of each page returned, element of each page, total number of pages |
| duration(Integer, Optional), |  |
| errors (Array[Error], Optional) |  |
| infos(Array[Info], Optional) |  |
| success(Boolean, Optional) |  |
| textMessage(String, Optional) |  |

=== "Example"
    ```json

    {
        "returnSearchId": "ATD::210706::519f4508-b6df-4d96-8d43-538c96a0d90b-R",
        "departureSearchId": "ATD::210706::519f4508-b6df-4d96-8d43-538c96a0d90b",
        "duration": 46854,
        "errors": null,
        "groupPricedItineraries": [
            {
            "airSupplier": "VJ",
            "aircraft": "Airbus A330",
            "vnaArea": null,
            "airline": "VJ",
            "airlineName": "VietJet Air",
            "arrivalDateTime": "2021-07-21T21:45:00.000Z",
            "departureDateTime": "2021-07-21T19:35:00.000Z",
            "destinationCity": "Hà Nội",
            "destinationCountry": "Vietnam",
            "destinationCountryCode": "VN",
            "destinationLocationCode": "HAN",
            "destinationLocationName": "Sân bay Nội Bài",
            "fightNo": "156",
            "flightType": "DOMESTIC",
            "groupId": "599a7a20-32b8-4e6b-b167-27feb4f324f5",
            "originCity": "Hồ Chí Minh",
            "originCountry": "Vietnam",
            "originCountryCode": "VN",
            "originLocationCode": "SGN",
            "originLocationName": "Sân bay Tân Sơn Nhất",
            "pricedItineraries": [
                {
                "airItineraryPricingInfo": {
                    "adultFare": {
                    "fareBasisCodes": null,
                    "passengerFare": {
                        "baseFare": {
                        "amount": 399000,
                        "currencyCode": null,
                        "decimalPlaces": 2
                        },
                        "comboMarkup": null,
                        "equivFare": null,
                        "serviceTax": {
                        "amount": 258900,
                        "currencyCode": null,
                        "decimalPlaces": 2
                        },
                        "surcharges": [
                        {
                            "amount": 0,
                            "indicator": "Ticket fee per segment",
                            "type": "Ticket fee per segment"
                        }
                        ],
                        "taxes": null,
                        "totalFare": {
                        "amount": 657900,
                        "currencyCode": null,
                        "decimalPlaces": 2
                        },
                        "totalPaxFee": null
                    },
                    "passengerTypeQuantities": {
                        "code": "ADT",
                        "quantity": 1
                    }
                    },
                    "childFare": null,
                    "divideInPartyIndicator": false,
                    "fareInfoReferences": null,
                    "fareSourceCode": "dom5226c7ae-e46c-48de-ae99-a7d4e3bf0782",
                    "fareType": "PUBLIC",
                    "infantFare": null,
                    "itinTotalFare": {
                    "baseFare": {
                        "amount": 399000,
                        "currencyCode": null,
                        "decimalPlaces": 2
                    },
                    "comboMarkup": null,
                    "equivFare": null,
                    "serviceTax": {
                        "amount": 258900,
                        "currencyCode": null,
                        "decimalPlaces": 2
                    },
                    "totalFare": {
                        "amount": 657900,
                        "currencyCode": null,
                        "decimalPlaces": 2
                    },
                    "totalPaxFee": null,
                    "totalTax": {
                        "amount": 0,
                        "currencyCode": null,
                        "decimalPlaces": 2
                    }
                    }
                },
                "allowHold": true,
                "baggageItems": [
                    {
                    "amount": 0,
                    "code": "air-tickets.baggage-items.vietnam.vj.economy.baggage.adult.free",
                    "direction": null,
                    "fareCode": null,
                    "id": "air-tickets.baggage-items.vietnam.vj.economy.baggage.adult.free",
                    "name": "7kg xách tay",
                    "serviceType": "BAGGAGE"
                    }
                ],
                "cabinClassName": "ECONOMY",
                "directionInd": "DEPARTURE",
                "fightNo": "156",
                "mealItems": null,
                "onlyPayLater": false,
                "originDestinationOptions": [
                    {
                    "cabinClassName": "ECONOMY",
                    "destinationCity": "Hà Nội",
                    "destinationDateTime": "2021-07-21T21:45:00.000Z",
                    "destinationLocationCode": "HAN",
                    "destinationLocationName": "Sân bay Nội Bài",
                    "flightDirection": "D",
                    "flightSegments": [
                        {
                        "adultBaggage": null,
                        "aircraft": "Airbus A330",
                        "arrivalAirportLocationCode": "HAN",
                        "arrivalAirportLocationName": "Sân bay Nội Bài",
                        "arrivalCity": "Hà Nội",
                        "arrivalDateTime": "2021-07-21T21:45:00.000Z",
                        "cabinClassCode": "Z1_ECO",
                        "cabinClassName": "ECONOMY",
                        "cabinClassText": "Economy",
                        "childBaggage": null,
                        "departureAirportLocationCode": "SGN",
                        "departureAirportLocationName": "Sân bay Tân Sơn Nhất",
                        "departureCity": "Hồ Chí Minh",
                        "departureDateTime": "2021-07-21T19:35:00.000Z",
                        "eticket": true,
                        "fareBasicCode": null,
                        "fareCode": null,
                        "flightDirection": "D",
                        "flightNumber": "156",
                        "infantBaggage": null,
                        "journeyDuration": 130,
                        "marketingAirlineCode": "VJ",
                        "marriageGroup": null,
                        "mealCode": null,
                        "operatingAirline": {
                            "code": "VJ",
                            "equipment": null,
                            "flightNumber": "156",
                            "name": "VietJet Air"
                        },
                        "resBookDesignCode": "Z1_ECO",
                        "seatsRemaining": null,
                        "stopQuantity": 0,
                        "stopQuantityInfo": null,
                        "supplierFareKey": null,
                        "supplierJourneyKey": "qPHglSL8tSGƒ3tYhxs32unUB07y8mK5BDYQX2BnPQJuYvXBionML¥MStNiƒK98yyAOIpSQgCYƒdoFP¥a2VnwgUPQJAmkk89BX1s9VLDde6FRhlAFf34qJAHS3DNEEwbaCBRcmqPevNTjFuizmUVPBSKBj6HlNSuyrpPZEREJgN8ThsfKqQnB6zAkEhnwV0rNNPzwWYQqRMFAZYiXy5p0roZGgAxbnU6itFQzVmWzpƒƒd1GUseZ6vDwLWRqbO2lnJcw7qbRbSƒ9Lw0btZKtBHz2zAUgpGG97MNdAf1xN2g2cFSƒxTc7lrjWfIJsC53YbqXvqMhzgmUSDj¥B5dxg4bloOeLI5¥YWAlkIGawk57IcgpyzGprHK5Pn3Bv2CR4sMsg7ey0Z5eGFvalCScS72idlrgHBzOYnbwZ21mkGjsXVus¥ƒoEJSpWVB3meJug14SIGSd88mzGXtT4ƒQg1Tam4wvySRzi9gO4QGGXpcbBF4ƒs="
                        }
                    ],
                    "journeyDuration": 130,
                    "originCity": "Hồ Chí Minh",
                    "originDateTime": "2021-07-21T19:35:00.000Z",
                    "originLocationCode": "SGN",
                    "originLocationName": "Sân bay Tân Sơn Nhất"
                    }
                ],
                "passportMandatory": true,
                "refundable": false,
                "sequenceNumber": "ibe3541984955292126",
                "ticketType": "ETICKET",
                "validReturnCabinClasses": null,
                "validatingAirlineCode": "VJ",
                "validatingAirlineName": "VietJet Air"
                }
            ],
            "requiredFields": null,
            "returnDateTime": null,
            "roundType": "ROUNDTRIP",
            "totalPricedItinerary": 3
            }
        ],
        "infos": null,
        "page": {
            "nextPageNumber": 1,
            "offset": 15,
            "pageNumber": 0,
            "previousPageNumber": -1,
            "totalElements": 57,
            "totalPage": 4
        },
        "searchId": "ATD::210706::519f4508-b6df-4d96-8d43-538c96a0d90b",
        "success": true,
        "textMessage": null
    }

    ```
---

## Get filter list information API

!!! info "POST: /api/air-tickets/filter-options"

    Get a list of values that can be applied on the filter on the search results

### Request Body

| Parameter | Description |
| --- | --- |
| searchId(String, Required) | Data used to refer to search results
This data is taken from the return results of airline ticket search |
| departureItinerary (AirItineraryInfo, Optional) | Outbound ticket information in case of getting filter-options for return ticket |
| airlineCode(String, Required) | Airline code
VN: Vietnam Airlines
VJ: VietJet
QH: Bamboo
BL: Pacific Airlines… |
| groupId(String, Required) | Journey identifier in the list of journeys returned by search results |
| fareSourceCode(String, Required) | Journey identifier information |
| supplierCode(String, Required) | The company code is also provided |
| searchId(String, Required) | Data used to refer to search results |

=== "Example"

    ```json
    {
        "searchId": "ATD::210707::01a59301-d1f7-4302-954a-7047ee06e001-R",
        "departureItinerary": {
            "groupId": "01e650b9-2771-48cb-80fa-3004d0bd9eef",
            "airlineCode": "VN",
            "fareSourceCode": "dom5fb76509-3ac6-4c7b-baaa-b1ea844e3d7e",
            "supplierCode": "VN",
            "searchId": "ATD::210707::01a59301-d1f7-4302-954a-7047ee06e001"
        }
    }

    ```

### Response

| Parameter | Description |
| --- | --- |
| searchId(String, Required) | The reference code to the search for air tickets, taken from the search results for air tickets |
| itineraryFilter (ItineraryFilter, Required) | Information representing applicable values on search filter results |
| airlineOptions(Array[String], Optional) | Information showing airlines with the lowest fares |
| cabinClassOptions(Array[String], Optional) | Information showing current seat class |
| stopOptions(Array[String], Optional) | Information showing current stop |
| filterToPrice(Double, Optional) | Information showing the current highest ticket price |
| filterFromPrice(Double, Optional) | Information showing the current lowest fares |
| duration (Integer, Optional), |  |
| errors (Array[Error], Optional), |  |
| infos (Array[Info], Optional), |  |
| success (Boolean, Optional), |  |
| textMessage (String, Optional) |  |

=== "Example"
    ```json

    {
        "isSuccess" : true,
        "duration" : 1131,
        "textMessage" : null,
        "errors" : null,
        "infos" : null,
        "searchId" : "ATD::210707::01a59301-d1f7-4302-954a-7047ee06e001-R",
        "itineraryFilter" : {
            "airlineOptions" : [ "VJ:VietJet Air:657900.0", "QH:Bamboo Airways:1461000.0", "BL:Pacific Airlines:2054000.0", "VN:Vietnam Airlines:2164000.0" ],
            "arrivalDateTimeOptions" : null,
            "arrivalDateTimeReturnOptions" : null,
            "cabinClassOptions" : [ "ECONOMY", "PREMIUM", "BUSINESS" ],
            "departureDateTimeOptions" : null,
            "departureDateTimeReturnOptions" : null,
            "flightType" : null,
            "groupId" : null,
            "loadMore" : null,
            "minPrice" : null,
            "filterToPrice" : 5202000.0,
            "filterFromPrice" : 657900.0,
            "priceItineraryId" : null,
            "step" : null,
            "stopOptions" : [ "1" ],
            "ticketPolicyOptions" : null
        },
        "success" : true
    }

    ```

## Filter/sort flight search results API

!!! info "POST: /api/air-tickets/filter-availability"

    Filter and sort flight search results

### Paramaters

| Parameter | Description |
| --- | --- |
| include-equivfare query (Boolean, Optional) | Request to pay more ticketing fee information |
| page query (Integer, Optional) | Number of pages you want to get results (eg: 0) |
| size query (Integer, Optional) | Number of results you want to get in 1 page (eg 20) |
| sort query(String, Optional) | Sort the results by the value of the returned property ascending or descending (eg: propertiesName,desc / propertiesName,asc) |

=== "Example"
    ?include-equivfare=`false`&page=`0`&size=`20`&sort=`departureDate,asc`

### Request Body

| Parameter | Description |
| --- | --- |
| searchId(String, Required) | Data used to refer to search results
This data is taken from the return results of airline ticket search |
| departureItinerary (AirItineraryInfo, Optional) | Outbound ticket information in case of getting filter-availability for return ticket |
|       airlineCode(String, Required) | Airline symbol
VN: Vietnam Airlines
VJ: VietJet
QH: Bamboo
BL: Pacific Airlines… |
|       groupId(String, Optional) | Journey identifier in the list of journeys returned by search results |
|       fareSourceCode(String, Required) | Journey identifier information |
|       supplierCode(String, Required) | The company code is also provided |
|       searchId(String, Required) | Data used to refer to search results |
| filter (ItineraryFilter, Required) | Used to input the desired filtering and sorting criteria |
|       cabinClassOptions(Array[String], Optional) | Information about the seat class you want to filter and sort |
|       step(String, Required) | Information used to distinguish between departure and return
1: Departure direction
2: Return direction |
|       flightType(String, Required) | Flight type information
DOMESTIC: domestic
INTERNATIONAL: international |
|       stopOption(Array[String], Optional) | Stop Information |
|       airlineOptions(Array[String], Optional) | Airline information |
|       departureDateTimeOptions (Array[String], Optional) | Information about departure time starts at around or at what time
Ex: departureDateTimeOptions: ["+18", "+12-18"]
+18: from 18h to 24h
+12-18: from 12pm to 6pm |
|       arrivalDateTimeReturnOptions (Array[String], Optional) | The end time information starts at what time or interval
Ex: arrivalDateTimeReturnOptions: ["+18", "+12-18"]
+18: from 18h to 24h
+12-18: from 12pm to 6pm |

=== "Example"

    ```json
        {
            "searchId": "ATD::210707::01a59301-d1f7-4302-954a-7047ee06e001",
            "filter": {
                "cabinClassOptions": [],
                "ticketPolicyOptions": [],
                "airlineOptions": [],
                "stopOptions": [],
                "step": "1",
                "flightType": "DOMESTIC",
                "departureDateTimeOptions": [],
                "arrivalDateTimeReturnOptions": [],
                "arrivalDateTimeOptions": [],
                "priceItineraryId": "",
                "loadMore": false,
                "departureDateTimeReturnOptions": []
            },
            "departureItinerary": null
        }

    ```

### Response
### Model

| Parameter | Description |
| --- | --- |
| searchId(String, Required) | The reference code to the search for air tickets, taken from the search results for air tickets |
| groupPricedItineraries (Array[GroupPricedItineraryDTO], Optional) | Information about the list of journeys returned by search results |
|       airSupplier(String, Required) | Carriers (VietnamAirline - VNA, VjetJet - VJ, BamBoo - QH, ...) |
|       aircraft (String, Optional) | Type of aircraft (Airbus A330, Boeing 787, .....) |
|       airline(String, Optional) | Airlines (VJ, VNA, ...) |
|       airlineName(String, Optional) | Name of airline (Vietjet Air, Vietnam Airlines, Bamboo, ...) |
|       arrivalDateTime(String, Required) | Arrival date and time, using UTC/GMT+7 time zone |
|       departureDateTime (String, Required) | Split flight time, using UTC/GMT+7 time zone |
|       destinationLocationCode (String, Optional) | Flight end city code |
|       destinationCountry(String, Optional) | The name of the country where the flight ended |
|       destinationCountryCode (String, Optional) | Flight end country code |
|       destinationCity(String, Optional) | The name of the city where the flight ends |
|       destinationLocationName (String, Optional) | Airport name where the flight ends |
|       flightNo(String, Optional) | Airplane number |
|       flightNo(String, Optional) | Airplane number |
|       flightType(String, Optional) | Type of flight domestic or international?
Flight type:
DOMESTIC: domestic
INTERNATIONAL: international |
|       groupId(String, Required) | Journey identifier in the list of journeys returned by search results |
|       originCity(String, Optional) | City name at departure point |
|       originCountry(String, Optional) | Country name at departure point |
|       originCountryCode(String, Optional) | Country code at departure point |
|       originLocationCode(String, Optional) | Flight departure city code |
|       originLocationName(String, Optional) | Airport name at departure point |
|       totalPricedItinerary (Integer, Required) | Total number of detailed journeys |
|       pricedItineraries (Array[PricedItineraries], Required) | Itinerary details |
|             airItineraryPricingInfo (AirItineraryPricingInfo, Required) | Detailed price information of the itinerary |
|                   adultFare (FareBreakdown, Required) |  |
|                         passengerFare (PassengerFare, Required) | Adult fare information |
|                                baseFare(FareInfo, required) | Basic fare information |
|                                        amount (Double, Required) | Amount of money |
|                                        decimalPlaces(Integer, Optional) | Decimal places rounded to |
|                                equivFare (FareInfo, Optional) | Similar to baseFare
Ticketing fee information |
|                                serviceTax (FareInfo, Required) | Similar to baseFare
Service fee information |
|                                totalFare (FareInfo, Required)  | Similar to baseFare
Total ticket price information |
|                                surcharges (Array[Surcharge], Required) | Information about surcharges per booking / per segment |
|                         passengerTypeQuantities (PassengerTypeQuantities, Optional) | Number/type of passengers |
|                                code(String, Required) | Adult/Child/Infant Identifier
Includes: ADT - adult / CHD - child / INF - infant |
|                                quantity (Integer, Required) | Number of adults / children / infants |
|                   childFare(PassengerFare, Optional) | Child fare information
Similar to adult fare information |
|                   infantFare (PassengerFare, Optional) | Infant fare information
Similar to adult fare information |
|                   itinTotalFare (PassengerFare, Required) | Total fare information of the journey
Similar to adult fare information |
|                   fareSourceCode(String, Required) | Journey identifier information
Used to get ticket condition information |
|       allowHold (Boolean, Required) | Information to allow to hold a reservation or not |
|       cabinClassName(String, Required) | Seat class information:
ECONOMY - universal seat
PREMIUM - special economy seat
BUSINESS - business chair |
|       fightNo(String, Optional) | Displays aircraft number information |
|       originDestinationOptions (Array(OriginDestinationOptions), Required) | Cruise's blocking/stopping information |
|             flightDirection(String, Required) | Show flight direction information of the journey
D - departure direction
R - return direction |
|             journeyDuration (Integer, Required) | Show flight time |
|             flightSegments (Array(FlightSegments), Required) | Show detailed information of departure / end points in the journey |
| page (AirPage, Required) | Object that describes information about pagination.
Sequence number of each page returned, element of each page, total number of pages |
| duration(Integer, Optional), |  |
| errors (Array[Error], Optional) |  |
| infos(Array[Info], Optional) |  |
| success(Boolean, Optional) |  |
| textMessage(String, Optional) |  |

=== "Example"
    ```json

    {
        "searchId": "ATD::210707::1f5e34da-24d5-46bf-993e-8cda8d716d15",
        "duration": 1034,
        "errors": null,
        "groupPricedItineraries": [
            {
            "airSupplier": "VN",
            "aircraft": "Airbus A321",
            "vnaArea": "NorthTrip",
            "airline": "VN",
            "airlineName": "Vietnam Airlines",
            "arrivalDateTime": "2021-07-23T07:15:00.000Z",
            "departureDateTime": "2021-07-23T05:00:00.000Z",
            "destinationCity": "Hồ Chí Minh",
            "destinationCountry": "Vietnam",
            "destinationCountryCode": "VN",
            "destinationLocationCode": "SGN",
            "destinationLocationName": "Sân bay Tân Sơn Nhất",
            "fightNo": "205",
            "flightType": "DOMESTIC",
            "groupId": "8527f1e5-5291-42cf-8b76-c6874889b6c6",
            "originCity": "Hà Nội",
            "originCountry": "Vietnam",
            "originCountryCode": "VN",
            "originLocationCode": "HAN",
            "originLocationName": "Sân bay Nội Bài",
            "pricedItineraries": [
                {
                "airItineraryPricingInfo": {
                    "adultFare": {
                    "fareBasisCodes": null,
                    "passengerFare": {
                        "baseFare": {
                        "amount": 2739000,
                        "currencyCode": null,
                        "decimalPlaces": 2
                        },
                        "comboMarkup": null,
                        "equivFare": null,
                        "serviceTax": {
                        "amount": 844000,
                        "currencyCode": null,
                        "decimalPlaces": 2
                        },
                        "surcharges": [
                        {
                            "amount": 0,
                            "indicator": "Ticket fee per segment",
                            "type": "Ticket fee per segment"
                        }
                        ],
                        "taxes": null,
                        "totalFare": {
                        "amount": 3583000,
                        "currencyCode": null,
                        "decimalPlaces": 2
                        },
                        "totalPaxFee": null
                    },
                    "passengerTypeQuantities": {
                        "code": "ADT",
                        "quantity": 1
                    }
                    },
                    "childFare": null,
                    "divideInPartyIndicator": false,
                    "fareInfoReferences": null,
                    "fareSourceCode": "dom2ac8e775-85a1-4a3a-a945-7c2e8eee905e",
                    "fareType": "PUBLIC",
                    "infantFare": null,
                    "itinTotalFare": {
                    "baseFare": {
                        "amount": 2739000,
                        "currencyCode": null,
                        "decimalPlaces": 2
                    },
                    "comboMarkup": null,
                    "equivFare": null,
                    "serviceTax": {
                        "amount": 844000,
                        "currencyCode": null,
                        "decimalPlaces": 2
                    },
                    "totalFare": {
                        "amount": 3583000,
                        "currencyCode": null,
                        "decimalPlaces": 2
                    },
                    "totalPaxFee": null,
                    "totalTax": {
                        "amount": 0,
                        "currencyCode": null,
                        "decimalPlaces": 2
                    }
                    }
                },
                "allowHold": true,
                "baggageItems": [
                    {
                    "amount": 0,
                    "code": "air-tickets.baggage-items.vn.adult-child.12kg-1x23kg.free",
                    "direction": null,
                    "fareCode": null,
                    "id": "air-tickets.baggage-items.vn.adult-child.12kg-1x23kg.free",
                    "name": "Xách tay 12kg + Ký gửi 1x23kg",
                    "serviceType": "BAGGAGE"
                    }
                ],
                "cabinClassName": "ECONOMY",
                "directionInd": "DEPARTURE",
                "fightNo": "205",
                "mealItems": null,
                "onlyPayLater": false,
                "originDestinationOptions": [
                    {
                    "cabinClassName": "ECONOMY",
                    "destinationCity": "Hồ Chí Minh",
                    "destinationDateTime": "2021-07-23T07:15:00.000Z",
                    "destinationLocationCode": "SGN",
                    "destinationLocationName": "Sân bay Tân Sơn Nhất",
                    "flightDirection": "D",
                    "flightSegments": [
                        {
                        "adultBaggage": null,
                        "aircraft": "Airbus A321",
                        "arrivalAirportLocationCode": "SGN",
                        "arrivalAirportLocationName": "Sân bay Tân Sơn Nhất",
                        "arrivalCity": "Hồ Chí Minh",
                        "arrivalDateTime": "2021-07-23T07:15:00.000Z",
                        "cabinClassCode": "M",
                        "cabinClassName": "ECONOMY",
                        "cabinClassText": "Economy Flex",
                        "childBaggage": null,
                        "departureAirportLocationCode": "HAN",
                        "departureAirportLocationName": "Sân bay Nội Bài",
                        "departureCity": "Hà Nội",
                        "departureDateTime": "2021-07-23T05:00:00.000Z",
                        "eticket": true,
                        "fareBasicCode": null,
                        "fareCode": null,
                        "flightDirection": "D",
                        "flightNumber": "205",
                        "infantBaggage": null,
                        "journeyDuration": 135,
                        "marketingAirlineCode": "VN",
                        "marriageGroup": null,
                        "mealCode": null,
                        "operatingAirline": {
                            "code": "VN",
                            "equipment": null,
                            "flightNumber": "205",
                            "name": "Vietnam Airlines"
                        },
                        "resBookDesignCode": "M",
                        "seatsRemaining": null,
                        "stopQuantity": 0,
                        "stopQuantityInfo": null,
                        "supplierFareKey": null,
                        "supplierJourneyKey": "b+T7Lz8Bk6JHev8ZaYn6JdksP71z9ZD2metfP5B9ooYsM9jko+XIuxjgA14ghnjgUaj450N5VDUtJjP9AGhuOW+4XTufOS5VZDXm0TvXcwMXZzjJrTD4yzKE2HcSkpV2GU4fA4JI8HBo2DdLJAOlMuSGTpcN0/ylBtnM8MWr9faFvtwUUNLcIEma87mvAT2djGS7D2B65bkfIudjgUgMzxbClvY862C1Fkqt6J1iU8QvNRJygV+tIM581jkWISXEqEBWynub65QcCSh37U/HZ7vCCNWM0CbjqbnEJDbIFDJMWEPs/reBsAdLJ1oQVj/XMMOfVyWYykSzqBjrSxEbjlC2kfUf/qcH2a+VjzSftFZ4xgxv9BVcyjEvt6nfFl9eNxB0u2sH6O6Jr+V4yhqo8MHUvHs61leE3ihqaZr2WOW0tagXPQjFe/IRySSO/gsZvNE8SnbYsjkmvY0YDSdfgzGbkxJQVHTcIztxg1JG5c0MlwrGdbVINsLXyL9s5TOANlBpNtr9ArzEcr2/M7lZy4PjAlRZqPhyAl6dK4cR1gZaz/P+LivHga86vjAGHUcMqbZsicH4D44YFGqjeYKbhTmudhnn5KWfWJcR+ES9bumTSt+dw5VYbIybf83v3nGVuiAe30K2Jmuc58pHcTlxSbUMaevMbegAHSVUreKGVI9Rzh69kmTuVo3uFsEeAgMKIGPXSuHX0T6SY0wFXhEPk9xpFbMEs3fHicGr5KwZGGQHXZyCzD2BcWJhFCfWvTBwzL517DWLdUl7I4ac9b9DrGu1hUkt0Tr1999yumGvley4csmh5p/BiJJryCF7/igdMlBV8oXwHiWF8zfscyHfodL4xYL+jWseqE00zGfgKUvRY8kMyOtxfR0yEWP3sJjQ9AXfMjpTdCCIpulJfwAkY9pgvipjnwN4P2URX7Vfk+dvm0lAOo8QtEqupcQNeUaNv/H0jO1OHwpdUFRzUzALfJycZXI0aq0gBPNrz+4VWUF4EXXss1DJRVLBO4Z1SLNW+yxrB3uK3g9QDbkKfcsmvdGd/5LA9NuSSqXqzD5O92kn0TtDH5Ne4IuN2B8/6UqJWz5VNUVeT+ph1k24Uv9/iotAuUYfvsqosCb2BvokHpa4rIvDLTLAsmC5f1WeMsY8Ydnwf2e0cmZLXPVwQcKDE3zP8PnI91Fd+oL5Zx7+sdGa4QFs8dtV9y2hgYarchiugXf5tcIzDdDOm7FnBj8/Y64D7ZuSZCu16w7VvBEjHcuJwIf/Z/OhKKTv50JKU8a5RNcD3/7CCCrIvtxOK8F57arqMPJHtOXkD7dtns4NpRaghfCGX6OphkRNdJxzzx2KQzo39Lj4xEaWqwYD/3FRJiRap+5WGLonTpOIlN5ryMLLyL59lXSa7ZvfuAipLvm5TrmBlVt7FHvVj/BZ/PmpLUSTNg25tw+hJVpXCGOn+4EI7AH0Ph0SuVGKv8dnEM0P/mFWnSjpKNUb6mmm3ippgIjQwonVKbnhO3eDF9F7Ll0="
                        }
                    ],
                    "journeyDuration": 135,
                    "originCity": "Hà Nội",
                    "originDateTime": "2021-07-23T05:00:00.000Z",
                    "originLocationCode": "HAN",
                    "originLocationName": "Sân bay Nội Bài"
                    }
                ],
                "passportMandatory": true,
                "refundable": false,
                "sequenceNumber": "ibe3638861560249232",
                "ticketType": "ETICKET",
                "validReturnCabinClasses": null,
                "validatingAirlineCode": "VN",
                "validatingAirlineName": "Vietnam Airlines"
                }
            ],
            "requiredFields": null,
            "returnDateTime": null,
            "roundType": "ROUNDTRIP",
            "totalPricedItinerary": 1
            }
        ],
        "infos": null,
        "page": {
            "nextPageNumber": 1,
            "offset": 15,
            "pageNumber": 0,
            "previousPageNumber": -1,
            "totalElements": 67,
            "totalPage": 5
        },
        "success": true,
        "textMessage": null
    }

    ```

---

## Get the list of tickets open for sale on a flight API

!!! info "POST: /api/air-tickets/group-itinerary/{id}"

    Get a list of tickets available for sale on a specific flight

### Paramaters

| Parameter | Description |
| --- | --- |
| id path (String, Required) | Used to refer to the list of tickets available for sale on a flight |
| include-equivfare query (Boolean, Optional) | Request to pay more ticketing fee information |
| page query (Integer, Optional) | Number of pages you want to get results (eg: 0) |
| size query (Integer, Optional) | Number of results you want to get in 1 page (eg 20) |
| sort query(String, Optional) | Sort the results by the value of the returned property ascending or descending (eg: propertiesName,desc / propertiesName,asc) |

=== "Example"
    `052a9f35-12eb-430b-baa0-7ea85a98e8b3`?include-equivfare=`false`&page=`0`&size=`20`&sort=`departureDate,asc`

### Request Body
### Parameter

| Parameter | Description |
| --- | --- |
| searchId(String, Required) | Data used to refer to search results
This data is taken from the return results of airline ticket search |
| departureItinerary (AirItineraryInfo, Optional) | Outbound ticket information in case of getting filter-availability for return ticket |
|       airlineCode(String, Required) | Airline symbol
VN: Vietnam Airlines
VJ: VietJet
QH: Bamboo
BL: Pacific Airlines… |
|       groupId(String, Optional) | Journey identifier in the list of journeys returned by search results |
|       fareSourceCode(String, Required) | Journey identifier information |
|       supplierCode(String, Required) | The company code is also provided |
|       searchId(String, Required) | Data used to refer to search results |
| filter (ItineraryFilter, Required) | Used to input the desired filtering and sorting criteria |
|       cabinClassOptions(Array[String], Optional) | Information about the seat class you want to filter and sort |
|       step(String, Required) | Information used to distinguish between departure and return
1: Departure direction
2: Return direction |
|       flightType(String, Required) | Flight type information
DOMESTIC: domestic
INTERNATIONAL: international |
|       stopOption(Array[String], Optional) | Stop Information |
|       airlineOptions(Array[String], Optional) | Airline information |
|       departureDateTimeOptions (Array[String], Optional) | Information about departure time starts at around or at what time
Ex: departureDateTimeOptions: ["+18", "+12-18"]
+18: from 18h to 24h
+12-18: from 12pm to 6pm |
|       arrivalDateTimeReturnOptions (Array[String], Optional) | The end time information starts at what time or interval
Ex: arrivalDateTimeReturnOptions: ["+18", "+12-18"]
+18: from 18h to 24h
+12-18: from 12pm to 6pm |
|      groupId(String, Required) | Itinerary identifier in the itinerary list retrieved from the search results |

=== "Example"

    ```json
        {
            "searchId": "ATD::210707::66c84a6f-fa81-4526-a2d9-2f7b7975214b",
            "departureItinerary": null,
            "filter": {
                "stopOptions": [],
                "airlineOptions": [],
                "cabinClassOptions": [],
                "ticketPolicyOptions": [],
                "departureDateTimeOptions": [],
                "arrivalDateTimeOptions": [],
                "departureDateTimeReturnOptions": [],
                "arrivalDateTimeReturnOptions": [],
                "flightType": "DOMESTIC",
                "groupId": "052a9f35-12eb-430b-baa0-7ea85a98e8b3",
                "loadMore": true,
                "step": "1"
            }
        }

    ```

### Response

| Parameter | Description |
| --- | --- |
| searchId(String, Required) | The reference code to the search for air tickets, taken from the search results for air tickets |
| groupPricedItineraries (Array[GroupPricedItineraryDTO], Optional) | Information about the list of journeys returned by search results |
|       airSupplier(String, Required) | Carriers (VietnamAirline - VNA, VjetJet - VJ, BamBoo - QH, ...) |
|       aircraft (String, Optional) | Type of aircraft (Airbus A330, Boeing 787, .....) |
|       airline(String, Optional) | Airlines (VJ, VNA, ...) |
|       airlineName(String, Optional) | Name of airline (Vietjet Air, Vietnam Airlines, Bamboo, ...) |
|       arrivalDateTime(String, Required) | Arrival date and time, using UTC/GMT+7 time zone |
|       departureDateTime (String, Required) | Split flight time, using UTC/GMT+7 time zone |
|       destinationLocationCode (String, Optional) | Flight end city code |
|       destinationCountry(String, Optional) | The name of the country where the flight ended |
|       destinationCountryCode (String, Optional) | Flight end country code |
|       destinationCity(String, Optional) | The name of the city where the flight ends |
|       destinationLocationName (String, Optional) | Airport name where the flight ends |
|       flightNo(String, Optional) | Airplane number |
|       flightNo(String, Optional) | Airplane number |
|       flightType(String, Optional) | Type of flight domestic or international?
Flight type:
DOMESTIC: domestic
INTERNATIONAL: international |
|       groupId(String, Required) | Journey identifier in the list of journeys returned by search results |
|       originCity(String, Optional) | City name at departure point |
|       originCountry(String, Optional) | Country name at departure point |
|       originCountryCode(String, Optional) | Country code at departure point |
|       originLocationCode(String, Optional) | Flight departure city code |
|       originLocationName(String, Optional) | Airport name at departure point |
|       totalPricedItinerary (Integer, Required) | Total number of detailed journeys |
|       pricedItineraries (Array[PricedItineraries], Required) | Itinerary details |
|             airItineraryPricingInfo (AirItineraryPricingInfo, Required) | Detailed price information of the itinerary |
|                   adultFare (FareBreakdown, Required) |  |
|                         passengerFare (PassengerFare, Required) | Adult fare information |
|                                baseFare(FareInfo, required) | Basic fare information |
|                                        amount (Double, Required) | Amount of money |
|                                        decimalPlaces(Integer, Optional) | Decimal places rounded to |
|                                equivFare (FareInfo, Optional) | Similar to baseFare
Ticketing fee information |
|                                serviceTax (FareInfo, Required) | Similar to baseFare
Service fee information |
|                                totalFare (FareInfo, Required)  | Similar to baseFare
Total ticket price information |
|                                surcharges (Array[Surcharge], Required) | Information about surcharges per booking / per segment |
|                         passengerTypeQuantities (PassengerTypeQuantities, Optional) | Number/type of passengers |
|                                code(String, Required) | Adult/Child/Infant Identifier
Includes: ADT - adult / CHD - child / INF - infant |
|                                quantity (Integer, Required) | Number of adults / children / infants |
|                   childFare(PassengerFare, Optional) | Child fare information
Similar to adult fare information |
|                   infantFare (PassengerFare, Optional) | Infant fare information
Similar to adult fare information |
|                   itinTotalFare (PassengerFare, Required) | Total fare information of the journey
Similar to adult fare information |
|                   fareSourceCode(String, Required) | Journey identifier information
Used to get ticket condition information |
|       allowHold (Boolean, Required) | Information to allow to hold a reservation or not |
|       cabinClassName(String, Required) | Seat class information:
ECONOMY - universal seat
PREMIUM - special economy seat
BUSINESS - business chair |
|       fightNo(String, Optional) | Displays aircraft number information |
|       originDestinationOptions (Array(OriginDestinationOptions), Required) | Cruise's blocking/stopping information |
|             flightDirection(String, Required) | Show flight direction information of the journey
D - departure direction
R - return direction |
|             journeyDuration (Integer, Required) | Show flight time |
|             flightSegments (Array(FlightSegments), Required) | Show detailed information of departure / end points in the journey |
| page (AirPage, Required) | Object that describes information about pagination.
Sequence number of each page returned, element of each page, total number of pages |
| duration(Integer, Optional), |  |
| errors (Array[Error], Optional) |  |
| infos(Array[Info], Optional) |  |
| success(Boolean, Optional) |  |
| textMessage(String, Optional) |  |

=== "Example"
    ```json

    {
        "duration" : 1025,
        "errors" : null,
        "groupPricedItinerary" : {
            "airSupplier" : "VJ",
            "aircraft" : "Airbus A321",
            "vnaArea" : null,
            "airline" : "VJ",
            "airlineName" : "VietJet Air",
            "arrivalDateTime" : "2021-07-23T07:20:00.000Z",
            "departureDateTime" : "2021-07-23T05:10:00.000Z",
            "destinationCity" : "Hồ Chí Minh",
            "destinationCountry" : "Vietnam",
            "destinationCountryCode" : "VN",
            "destinationLocationCode" : "SGN",
            "destinationLocationName" : "Sân bay Tân Sơn Nhất",
            "fightNo" : "135",
            "flightType" : "DOMESTIC",
            "groupId" : "052a9f35-12eb-430b-baa0-7ea85a98e8b3",
            "originCity" : "Hà Nội",
            "originCountry" : "Vietnam",
            "originCountryCode" : "VN",
            "originLocationCode" : "HAN",
            "originLocationName" : "Sân bay Nội Bài",
            "pricedItineraries" : [ {
            "airItineraryPricingInfo" : {
                "adultFare" : {
                "fareBasisCodes" : null,
                "passengerFare" : {
                    "baseFare" : {
                    "amount" : 1319000.0,
                    "currencyCode" : null,
                    "decimalPlaces" : 2
                    },
                    "comboMarkup" : null,
                    "equivFare" : null,
                    "serviceTax" : {
                    "amount" : 350900.0,
                    "currencyCode" : null,
                    "decimalPlaces" : 2
                    },
                    "surcharges" : [ {
                    "amount" : 0.0,
                    "indicator" : "Ticket fee per segment",
                    "type" : "Ticket fee per segment"
                    } ],
                    "taxes" : null,
                    "totalFare" : {
                    "amount" : 1669900.0,
                    "currencyCode" : null,
                    "decimalPlaces" : 2
                    },
                    "totalPaxFee" : null
                },
                "passengerTypeQuantities" : {
                    "code" : "ADT",
                    "quantity" : 1
                }
                },
                "childFare" : null,
                "divideInPartyIndicator" : false,
                "fareInfoReferences" : null,
                "fareSourceCode" : "dom95053f40-3fd0-4f62-a96c-d4afa489c283",
                "fareType" : "PUBLIC",
                "infantFare" : null,
                "itinTotalFare" : {
                "baseFare" : {
                    "amount" : 1319000.0,
                    "currencyCode" : null,
                    "decimalPlaces" : 2
                },
                "comboMarkup" : null,
                "equivFare" : null,
                "serviceTax" : {
                    "amount" : 350900.0,
                    "currencyCode" : null,
                    "decimalPlaces" : 2
                },
                "totalFare" : {
                    "amount" : 1669900.0,
                    "currencyCode" : null,
                    "decimalPlaces" : 2
                },
                "totalPaxFee" : null,
                "totalTax" : {
                    "amount" : 0.0,
                    "currencyCode" : null,
                    "decimalPlaces" : 2
                }
                }
            },
            "allowHold" : true,
            "baggageItems" : [ {
                "amount" : 0.0,
                "code" : "air-tickets.baggage-items.vietnam.vj.economy.baggage.adult.free",
                "direction" : null,
                "fareCode" : null,
                "id" : "air-tickets.baggage-items.vietnam.vj.economy.baggage.adult.free",
                "name" : "7kg xách tay",
                "serviceType" : "BAGGAGE"
            } ],
            "cabinClassName" : "ECONOMY",
            "directionInd" : "DEPARTURE",
            "fightNo" : "135",
            "mealItems" : null,
            "onlyPayLater" : false,
            "originDestinationOptions" : [ {
                "cabinClassName" : "ECONOMY",
                "destinationCity" : "Hồ Chí Minh",
                "destinationDateTime" : "2021-07-23T07:20:00.000Z",
                "destinationLocationCode" : "SGN",
                "destinationLocationName" : "Sân bay Tân Sơn Nhất",
                "flightDirection" : "D",
                "flightSegments" : [ {
                "adultBaggage" : null,
                "aircraft" : "Airbus A321",
                "arrivalAirportLocationCode" : "SGN",
                "arrivalAirportLocationName" : "Sân bay Tân Sơn Nhất",
                "arrivalCity" : "Hồ Chí Minh",
                "arrivalDateTime" : "2021-07-23T07:20:00.000Z",
                "cabinClassCode" : "L1_ECO",
                "cabinClassName" : "ECONOMY",
                "cabinClassText" : "Economy",
                "childBaggage" : null,
                "departureAirportLocationCode" : "HAN",
                "departureAirportLocationName" : "Sân bay Nội Bài",
                "departureCity" : "Hà Nội",
                "departureDateTime" : "2021-07-23T05:10:00.000Z",
                "eticket" : true,
                "fareBasicCode" : null,
                "fareCode" : null,
                "flightDirection" : "D",
                "flightNumber" : "135",
                "infantBaggage" : null,
                "journeyDuration" : 130,
                "marketingAirlineCode" : "VJ",
                "marriageGroup" : null,
                "mealCode" : null,
                "operatingAirline" : {
                    "code" : "VJ",
                    "equipment" : null,
                    "flightNumber" : "135",
                    "name" : "VietJet Air"
                },
                "resBookDesignCode" : "L1_ECO",
                "seatsRemaining" : null,
                "stopQuantity" : 0,
                "stopQuantityInfo" : null,
                "supplierFareKey" : null,
                "supplierJourneyKey" : "FE1G3mI6J96guNcAzJB8yTeBzLZRAYEOnwn9YGOFJJztƒS7kLTBSBi25njFnV5B0HNFbXtvvIQiUDfNE¥Pqx3WSriPxr9IlTddLHufsqIM0oNnapPeNa1YAcBL4BUZyzjPyb¥0vzaCP¥5Bk9LpFxJTyFThaƒJiL7Tkƒhz4a¥FVSƒXfpqmsCaQWijrGgcOExEM7¥YXajB5L1W9SjqIYUUSewƒSb7BuyBX9sYii0QbSnQ8BdSvR4f2sq3pzUPx3AdCb2hZzEbIfpSEF8q5JAvRjuANKRqQhVei1eyTI72ZPbI0lKƒvrLemkP6OyE88rTƒuvxxHDe¥6K9dKwVV4GtkXj3J3lQOMsH2HKNOmpwG5TR4L1RiOI75PJ4YkC62AHux5vvTƒ¥R8vac6V9lKlMeMFra27Bv3qYhfwSWCgGNOcFsrs2yO1W¥WWXNMvWA2jNKUJl1H65iX18UHyzANy9Vrcthtjjr6PXKZHhQPnLP¥flZA="
                } ],
                "journeyDuration" : 130,
                "originCity" : "Hà Nội",
                "originDateTime" : "2021-07-23T05:10:00.000Z",
                "originLocationCode" : "HAN",
                "originLocationName" : "Sân bay Nội Bài"
            } ],
            "passportMandatory" : true,
            "refundable" : false,
            "sequenceNumber" : "ibe3640395997485504",
            "ticketType" : "ETICKET",
            "validReturnCabinClasses" : null,
            "validatingAirlineCode" : "VJ",
            "validatingAirlineName" : "VietJet Air"
            }, {
            "airItineraryPricingInfo" : {
                "adultFare" : {
                "fareBasisCodes" : null,
                "passengerFare" : {
                    "baseFare" : {
                    "amount" : 1499000.0,
                    "currencyCode" : null,
                    "decimalPlaces" : 2
                    },
                    "comboMarkup" : null,
                    "equivFare" : null,
                    "serviceTax" : {
                    "amount" : 368900.0,
                    "currencyCode" : null,
                    "decimalPlaces" : 2
                    },
                    "surcharges" : [ {
                    "amount" : 0.0,
                    "indicator" : "Ticket fee per segment",
                    "type" : "Ticket fee per segment"
                    } ],
                    "taxes" : null,
                    "totalFare" : {
                    "amount" : 1867900.0,
                    "currencyCode" : null,
                    "decimalPlaces" : 2
                    },
                    "totalPaxFee" : null
                },
                "passengerTypeQuantities" : {
                    "code" : "ADT",
                    "quantity" : 1
                }
                },
                "childFare" : null,
                "divideInPartyIndicator" : false,
                "fareInfoReferences" : null,
                "fareSourceCode" : "domb8304899-04b8-4ff4-9262-9ad713608507",
                "fareType" : "PUBLIC",
                "infantFare" : null,
                "itinTotalFare" : {
                "baseFare" : {
                    "amount" : 1499000.0,
                    "currencyCode" : null,
                    "decimalPlaces" : 2
                },
                "comboMarkup" : null,
                "equivFare" : null,
                "serviceTax" : {
                    "amount" : 368900.0,
                    "currencyCode" : null,
                    "decimalPlaces" : 2
                },
                "totalFare" : {
                    "amount" : 1867900.0,
                    "currencyCode" : null,
                    "decimalPlaces" : 2
                },
                "totalPaxFee" : null,
                "totalTax" : {
                    "amount" : 0.0,
                    "currencyCode" : null,
                    "decimalPlaces" : 2
                }
                }
            },
            "allowHold" : true,
            "baggageItems" : [ {
                "amount" : 0.0,
                "code" : "air-tickets.baggage-items.vietnam.vj.premium.baggage.adult.free",
                "direction" : null,
                "fareCode" : null,
                "id" : "air-tickets.baggage-items.vietnam.vj.premium.baggage.adult.free",
                "name" : "7kg xách tay + 20kg ký gửi",
                "serviceType" : "BAGGAGE"
            } ],
            "cabinClassName" : "PREMIUM",
            "directionInd" : "DEPARTURE",
            "fightNo" : "135",
            "mealItems" : null,
            "onlyPayLater" : false,
            "originDestinationOptions" : [ {
                "cabinClassName" : "PREMIUM",
                "destinationCity" : "Hồ Chí Minh",
                "destinationDateTime" : "2021-07-23T07:20:00.000Z",
                "destinationLocationCode" : "SGN",
                "destinationLocationName" : "Sân bay Tân Sơn Nhất",
                "flightDirection" : "D",
                "flightSegments" : [ {
                "adultBaggage" : null,
                "aircraft" : "Airbus A321",
                "arrivalAirportLocationCode" : "SGN",
                "arrivalAirportLocationName" : "Sân bay Tân Sơn Nhất",
                "arrivalCity" : "Hồ Chí Minh",
                "arrivalDateTime" : "2021-07-23T07:20:00.000Z",
                "cabinClassCode" : "B1_DLX",
                "cabinClassName" : "PREMIUM",
                "cabinClassText" : "Premium",
                "childBaggage" : null,
                "departureAirportLocationCode" : "HAN",
                "departureAirportLocationName" : "Sân bay Nội Bài",
                "departureCity" : "Hà Nội",
                "departureDateTime" : "2021-07-23T05:10:00.000Z",
                "eticket" : true,
                "fareBasicCode" : null,
                "fareCode" : null,
                "flightDirection" : "D",
                "flightNumber" : "135",
                "infantBaggage" : null,
                "journeyDuration" : 130,
                "marketingAirlineCode" : "VJ",
                "marriageGroup" : null,
                "mealCode" : null,
                "operatingAirline" : {
                    "code" : "VJ",
                    "equipment" : null,
                    "flightNumber" : "135",
                    "name" : "VietJet Air"
                },
                "resBookDesignCode" : "B1_DLX",
                "seatsRemaining" : null,
                "stopQuantity" : 0,
                "stopQuantityInfo" : null,
                "supplierFareKey" : null,
                "supplierJourneyKey" : "FE1G3mI6J96guNcAzJB8ySG7yJpj7V0vJxur9hB00jyNcwƒ20DdiB6fj9ƒvf9GgUPS3rI8a¥ƒYn83OMqVXPoZwCp649T3OB0aQ7ItYXABxYRfM6ZiDbfC62m¥¥yAZf5jf7NBG6IJSBVQnsJZWUMvrv6CtZ9j1N5OQ5sUtFN37WkEjJEfSORxmB2ZQdKamFtKHi¥dgP¥7EYIHXmy1f6hdavIhehIqx9Kl¥0gPaxg2ycItGrM0ZkRcUFypKbAlYoUw8DaNiLc3Q3XcNkHy0LJlg4QzLcoWk6uwDkBMr3KUnCxyBR1beBxMhopJovzMvnRZWaWuTMfz¥7dhh32SnQ9OzYwz0uZ¥FreZDsZLp1kzrXPZDcmzsxpvfVaclBhMlJPxz¥ByUpAMUKCQyhfbDINrCiqXDKG5aFEXYs5AFl2SyTl12¥ghZJ8nfkZve9QoEA0EEfsSomUdKcaNƒrCH1H1Esj8jVUthM3fCppoSJPGjOjI="
                } ],
                "journeyDuration" : 130,
                "originCity" : "Hà Nội",
                "originDateTime" : "2021-07-23T05:10:00.000Z",
                "originLocationCode" : "HAN",
                "originLocationName" : "Sân bay Nội Bài"
            } ],
            "passportMandatory" : true,
            "refundable" : false,
            "sequenceNumber" : "ibe3640395997554532",
            "ticketType" : "ETICKET",
            "validReturnCabinClasses" : null,
            "validatingAirlineCode" : "VJ",
            "validatingAirlineName" : "VietJet Air"
            }, {
            "airItineraryPricingInfo" : {
                "adultFare" : {
                "fareBasisCodes" : null,
                "passengerFare" : {
                    "baseFare" : {
                    "amount" : 3200000.0,
                    "currencyCode" : null,
                    "decimalPlaces" : 2
                    },
                    "comboMarkup" : null,
                    "equivFare" : null,
                    "serviceTax" : {
                    "amount" : 539000.0,
                    "currencyCode" : null,
                    "decimalPlaces" : 2
                    },
                    "surcharges" : [ {
                    "amount" : 0.0,
                    "indicator" : "Ticket fee per segment",
                    "type" : "Ticket fee per segment"
                    } ],
                    "taxes" : null,
                    "totalFare" : {
                    "amount" : 3739000.0,
                    "currencyCode" : null,
                    "decimalPlaces" : 2
                    },
                    "totalPaxFee" : null
                },
                "passengerTypeQuantities" : {
                    "code" : "ADT",
                    "quantity" : 1
                }
                },
                "childFare" : null,
                "divideInPartyIndicator" : false,
                "fareInfoReferences" : null,
                "fareSourceCode" : "dom1c7a82fb-83f9-4fe0-9451-bb023179deaa",
                "fareType" : "PUBLIC",
                "infantFare" : null,
                "itinTotalFare" : {
                "baseFare" : {
                    "amount" : 3200000.0,
                    "currencyCode" : null,
                    "decimalPlaces" : 2
                },
                "comboMarkup" : null,
                "equivFare" : null,
                "serviceTax" : {
                    "amount" : 539000.0,
                    "currencyCode" : null,
                    "decimalPlaces" : 2
                },
                "totalFare" : {
                    "amount" : 3739000.0,
                    "currencyCode" : null,
                    "decimalPlaces" : 2
                },
                "totalPaxFee" : null,
                "totalTax" : {
                    "amount" : 0.0,
                    "currencyCode" : null,
                    "decimalPlaces" : 2
                }
                }
            },
            "allowHold" : true,
            "baggageItems" : [ {
                "amount" : 0.0,
                "code" : "air-tickets.baggage-items.vietnam.vj.business.baggage.adult.free",
                "direction" : null,
                "fareCode" : null,
                "id" : "air-tickets.baggage-items.vietnam.vj.business.baggage.adult.free",
                "name" : "10kg xách tay + 30kg ký gửi",
                "serviceType" : "BAGGAGE"
            } ],
            "cabinClassName" : "BUSINESS",
            "directionInd" : "DEPARTURE",
            "fightNo" : "135",
            "mealItems" : null,
            "onlyPayLater" : false,
            "originDestinationOptions" : [ {
                "cabinClassName" : "BUSINESS",
                "destinationCity" : "Hồ Chí Minh",
                "destinationDateTime" : "2021-07-23T07:20:00.000Z",
                "destinationLocationCode" : "SGN",
                "destinationLocationName" : "Sân bay Tân Sơn Nhất",
                "flightDirection" : "D",
                "flightSegments" : [ {
                "adultBaggage" : null,
                "aircraft" : "Airbus A321",
                "arrivalAirportLocationCode" : "SGN",
                "arrivalAirportLocationName" : "Sân bay Tân Sơn Nhất",
                "arrivalCity" : "Hồ Chí Minh",
                "arrivalDateTime" : "2021-07-23T07:20:00.000Z",
                "cabinClassCode" : "V_SBoss",
                "cabinClassName" : "BUSINESS",
                "cabinClassText" : "SkyBoss",
                "childBaggage" : null,
                "departureAirportLocationCode" : "HAN",
                "departureAirportLocationName" : "Sân bay Nội Bài",
                "departureCity" : "Hà Nội",
                "departureDateTime" : "2021-07-23T05:10:00.000Z",
                "eticket" : true,
                "fareBasicCode" : null,
                "fareCode" : null,
                "flightDirection" : "D",
                "flightNumber" : "135",
                "infantBaggage" : null,
                "journeyDuration" : 130,
                "marketingAirlineCode" : "VJ",
                "marriageGroup" : null,
                "mealCode" : null,
                "operatingAirline" : {
                    "code" : "VJ",
                    "equipment" : null,
                    "flightNumber" : "135",
                    "name" : "VietJet Air"
                },
                "resBookDesignCode" : "V_SBoss",
                "seatsRemaining" : null,
                "stopQuantity" : 0,
                "stopQuantityInfo" : null,
                "supplierFareKey" : null,
                "supplierJourneyKey" : "FE1G3mI6J96guNcAzJB8yZ¥FGw7p5Weqh1jFldOtANHbBsM1ZM4xm9eJCMdqbmYTODQA1GPi0yHK6bYrz1U6SPAnrzCjhNqS6fuU9vMGIlpY3BwX937d9zbpx5aotYD2Hkad7SVACsbXLfkhQm2Bu0X¥k9ƒAQbtCjpXj6rFƒKBXVZSRY4hOF8GQQZ2IFqdegJGFHN6kEeNGHYeJt39SUgpDDRMq0OtLvm0iic¥1YGj1AJVIaj6FUƒxPo4OkVIUB83axadxG7pbDxZCn28¥85bUM50I2Bcp4yxrKnHC7YkXWAKN5JhIQzRHTrt1HbQzF9MP3FP7PWoNvG0BHUndiYelƒ653zOv0dSzƒSX2Tzomz11Rf2fHWHPXwigUvBA74Zsy5vKwDNZxYYv9aJC3c33pEƒ6LsD5NDmdiSRtXzrl8tzStLzyjYapGU0fDSh9bThcZCxpeejWyEVyjHdgqV4e77ncQTeUWUKNa1ggƒrerpRc="
                } ],
                "journeyDuration" : 130,
                "originCity" : "Hà Nội",
                "originDateTime" : "2021-07-23T05:10:00.000Z",
                "originLocationCode" : "HAN",
                "originLocationName" : "Sân bay Nội Bài"
            } ],
            "passportMandatory" : true,
            "refundable" : false,
            "sequenceNumber" : "ibe3640395997606506",
            "ticketType" : "ETICKET",
            "validReturnCabinClasses" : null,
            "validatingAirlineCode" : "VJ",
            "validatingAirlineName" : "VietJet Air"
            } ],
            "requiredFields" : null,
            "returnDateTime" : null,
            "roundType" : "ROUNDTRIP",
            "totalPricedItinerary" : 3
        },
        "infos" : null,
        "searchId" : "ATD::210707::66c84a6f-fa81-4526-a2d9-2f7b7975214b",
        "success" : true,
        "textMessage" : null
    }

    ```

---

## Get flight ticket condition API

!!! info "POST: /api/air-tickets/farerules"

    Get the ticket conditions of the flight

### Paramaters

| Parameter | Description |
| --- | --- |
| language query (Boolean, Optional) | The language you want to get |

=== "Example"
    `?language=vi`

### Request Body

| Parameter | Description |
| --- | --- |
| searchId(String, Required) | Data used to refer to search results
This data is taken from the return results of airline ticket search |
| groupId(String, Required) | Journey identifier in the list of journeys returned by search results |
| fareSourceCode(String, Required) | Journey identifier information |

=== "Example"

    ```json
        {
            "fareSourceCode": "dom07b2da7b-3232-4294-9278-b35fb6307714",
            "groupId": "27b091a7-62b8-4ce2-b45b-eda3340d7673",
            "searchId": "ATD::210720::dc96e1a9-c39e-4f48-974e-e0be6abb45c7"
        }

    ```

### Response

| Parameter | Description |
| --- | --- |
| fareRules(Array[FareRules], Required) | Return ticket conditions list |
| arrivalAirportLocationCode (String, Required) | Destination location code |
| departureAirportLocationCode (String, Required) | Departure location code |
| departureDateTime(String, Required) | Departure time
Identified by yyyy-MM-dd'T'HH:mm:ss'Z' |
| arrivalDateTime(String, Required) | Arrival time
Format in yyyy-MM-dd'T'HH:mm:ss'Z' |
| fareRuleItems (Array[FareRuleItem], Required) | Detailed list of ticket conditions |
| detail(String, Required) | Detailed information about ticket conditions
HTML format |
| title(String, Required) | Information about the conditions of the return ticket / the condition of the return ticket |
| duration(Integer, Optional), |  |
| errors (Array[Error], Optional), |  |
| infos(Array[Info], Optional), |  |
| success(Boolean, Optional), |  |
| textMessage(String, Optional) |  |

=== "Example"
    ```json

    {
        "duration": 1444,
        "errors": null,
        "fareRules": [
            {
            "arrivalAirportLocationCode": "SGN",
            "arrivalAirportLocationName": null,
            "arrivalCity": null,
            "arrivalDateTime": "2021-08-16T07:55:00.000Z",
            "departureAirportLocationCode": "HAN",
            "departureAirportLocationName": null,
            "departureCity": null,
            "departureDateTime": "2021-08-16T05:45:00.000Z",
            "fareRuleItems": [
                {
                "detail": "\n            \n            <br /><strong>- Hạng đặt chỗ:</strong> Economy Saver\n            <br /><strong>- Thay đổi:</strong>  Trước 3h tính từ giờ khởi hành từng chặng bay : 270.000 VND . Trong/sau 3h tính từ giờ khởi hành từng chặng bay: Không áp dụng\n            <br /><strong>- Hoàn/hủy vé:</strong> Không áp dụng\n            <br /><strong>- Đổi tên:</strong> Chỉ áp dụng đối với vé chưa sử dụng. Thay đổi trước giờ khởi hành 3h của chuyến bay đầu tiên và phải đổi tên cho cả hành trình, thu phí thay đổi tên 350.000 VND\n            <br /><strong>- Hành lý:</strong> Xách tay 7kg + Ký gửi 20kg\n            <br /><strong>- Suất ăn:</strong> Đã bao gồm\n            <br /><strong>- Hệ số cộng điểm Bamboo Club:</strong> 0.25\n\t        <br /><strong>- Ghi chú:</strong> Mọi thay đổi trên vé phải thực hiện trước 3h so với giờ khởi hành hoặc theo quy định của từng loại vé. Tất cả phí áp dụng chưa bao gồm VAT và được tính cho từng khách/chặng + chênh lệch vé (nếu có). Tết Nguyên Đán 2022: 17/01/2022 – 16/02/2022\n\t\t    <br /><strong>- Ghi chú Covid-19:</strong> HÀNH KHÁCH KHI ĐẶT CHỖ MUA VÉ CẦN THỰC HIỆN KHAI BÁO Y TẾ ĐIỆN TỬ BẮT BUỘC TRƯỚC KHI TỚI SÂN BAY\n            <br /><br/><strong> Tham khảo thêm <a href='https://www.bambooairways.com/vn-vi/thong-tin-dat-ve/dat-chuyen-bay/cac-hang-ve-gia-ve/' target='_blank'>Điều kiện giá vé áp dụng cho các vé xuất và khởi hành từ ngày 01/03/2021</a>\n\t\t\t\n        ",
                "title": "Điều kiện chiều đi"
                }
            ],
            "operatingAirline": {
                "code": "VN",
                "equipment": null,
                "flightNumber": null,
                "name": null
            }
            }
        ],
        "fareSourceCode": null,
        "groupId": null,
        "infos": null,
        "searchId": null,
        "success": true,
        "textMessage": null
    }

    ```
---