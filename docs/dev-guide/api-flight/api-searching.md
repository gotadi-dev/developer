
## 1. API lấy danh sách sân bay

!!! info "GET: /metasrv/api/_search/airports"
    Tìm kiếm sân bay dựa theo từ khóa liên quan hoặc mã quốc gia/vùng lãnh thổ

    Cho phép sắp xếp kết quả trả về

### Parameter

=== "Parameters"
???+ example "Parameters"

    - query `query` (String, Optional)

        !!! quote ""

            Từ khóa tìm kiếm khu vực / tên sân bay (VD: SGN, Vietnam, Tokyo)

    - country `query` (String, Optional)

        !!! quote ""

            Mã quốc gia / vùng lãnh thổ (VD: VN)

    - page `query` (Integer, Optional)

        !!! quote ""

            Số trang đang muốn lấy kết quả (VD: 0)
        
    - size `query` (Integer, Optional)

        !!! quote ""

            Số kết quả muốn lấy trong 1 trang (VD: 20)

    - sort `query` (String, Optional) 

        !!! quote ""

            Sắp xếp kết quả theo giá trị của thuộc tính trả về tăng dần hay giảm dần (VD: propertiesName,desc / propertiesName,asc)

=== "Example"
    ?query=`ha`&country=`VN`&page=`0`&size=`20`&sort=`name,desc`

### Response

#### Code 200

> OK

=== "Model"
    ???+ example "Model"
        `Chỉ định danh những trường/field cần thiết`

        - Array[AirportDTO] (Optional)

            !!! quote ""

                Thông tin danh sách sân bay trả về

            - id (Long, Optional)

                !!! quote ""

                    Mã định danh danh sách sân bay

            - code (String, Optional)

                !!! quote ""

                    Mã ký hiệu sân bay
            
            - name (String, Optional)

                !!! quote ""

                    Tên sân bay
            
            - cityCode (String, Optional)

                !!! quote ""

                    Mã ký hiệu thành phố
            
            - city (String, Optional)

                !!! quote ""

                    Tên thành phố

            - countryCode (String, Optional)

                !!! quote ""

                    Mã ký hiệu quốc gia

            - country (String, Optional)

                !!! quote ""

                    Tên quốc gia
            - timeZone (Integer, Optional)

                !!! quote ""

                    Múi giờ
            - location (String, Optional)

                !!! quote ""

                    Vị trí
            
            - name2 (String, Optional)

                !!! quote ""

                    Tên sân bay tiếng anh (tên khác)

            - city2 (String, Optional)

                !!! quote ""

                    Tên thành phố tiếng anh (tên khác)

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

#### Code 400

> Bad Request

#### Code 401

> Unauthorized

#### Code 403

> Forbidden

#### Code 404

> Not Found

#### Code 500

> Unknown Internal Error

#### Code 503

> Service Unavailable

---

## 2. API tìm kiếm vé máy bay

!!! info "GET: /api/air-tickets/low-fare-search-async"

    Tìm kiếm chuyến bay  theo điểm khởi hành và điểm kết thúc / theo ngày giờ

### Parameter

=== "Paramter"
    ???+ example "Parameters"

        - origin_code `query` (String, Required)

            !!! quote ""

                Mã sân bay điểm đi

                VD: Sân bay ở Hồ Chí Minh có mã là SGN

        - destination_code `query` (String, Required)

            !!! quote ""
            
                Mã sân bay điểm đến

                VD: Sân bay ở Hà Nội có mã là HAN

        - departure_date `query` (String, Required)

            !!! quote ""

                Ngày khởi hành

                Định dạng theo MM-dd-YYYY

                VD: 07-07-2021
        
        - returnure_date `query` (String, Required)

            !!! quote ""

                Ngày về

                Định dạng theo MM-dd-YYYY

                VD: 08-20-2021

        - cabin_class `query` (String, Required)

            !!! quote ""

                Hạng ghế vé

                Truyền giá trị là E

        - route_type `query` (String, Optional)

            !!! quote ""

                Loại hành trình:

                - `ONEWAY`: Một chiều

                - `ROUNDTRIP`: Khứ hồi

                Nếu không truyền thì có giá trị là `ONEWAY`

        - aduts_qtt `query` (Integer, Optional)

            !!! quote ""

                Số lượng hành khách là người lớn ( `12 tuổi trở lên` )

                Nếu không truyền giá trị mặc định là 1
        
        - children_qtt `query` (Integer, Optional)

            !!! quote ""

                Số lượng hành khách là trẻ em ( `từ 2 tuổi và nhỏ hơn 12 tuổi` )

                Nếu không truyền giá trị mặc định là 0
        
        - infant_qtt `query` (Integer, Optional)

            !!! quote ""

                Số lượng hành khách là trẻ sơ sinh ( `dưới 2 tuổi` )

                Nếu không truyền giá trị mặc định là 0

        - time `query` (String, Optional)

            !!! quote ""

                Thời điểm gọi API (UnixTimeStamp)

                VD: 1625545845

        - key `query` (String, Optional)

            !!! quote ""

                Key để checksum

                !!! note "Cách tạo giá trị:" 
                
                    `MAC-SHA256(<origin_code><destination_code><departure_time><returnure_date><cabin_class><route_type><aduts_qtt><children_qtt><infant_qtt><page><size><time>, 'Gotadi')`
            
        - include-equivfare `query` (Boolean, Optional)

            !!! quote ""

                Yêu cầu trả thêm thông tin phí xuất vé (EquivFare)

        - page `query` (Integer, Optional)

            !!! quote ""

                Số trang đang muốn lấy kết quả (VD: 0)
            
        - size `query` (Integer, Optional)

            !!! quote ""

                Số kết quả muốn lấy trong 1 trang (VD: 20)

        - sort `query` (String, Optional) 

            !!! quote ""

                Sắp xếp kết quả theo giá trị của thuộc tính trả về tăng dần hay giảm dần (VD: propertiesName,desc / propertiesName,asc)

=== "Example"
    ?origin_code=`SGN`&destination_code=`HAN`&departure_date=`07-21-2021`&returnture_date=`07-28-2021`&cabin_class=`E`&route_type=`ROUNDTRIP`&aduts_qtt=`1`&children_qtt=`0`&infants_qtt=`0`&time=`1625552814666`&key=`/xNr15RmY0dqSUkhvpKI1bIbKIuyZr1Q38rLi3bqxVk`=&page=`0`&size=`15`

### Response

#### Code 200

> OK

=== "Model"
    ???+ example "Model"
        `Chỉ định danh những trường/field cần thiết`

        - searchId (String, Required) 

            !!! quote ""

                Mã tham chiếu đến search vé máy bay, được lấy từ kết quả search vé máy bay


        - departureSearchId (String, Required)
        
            !!! quote ""

                Mã tham chiếu đến search chiều đi vé máy bay

                Được lấy từ searchId

        - returnSearchId (String, Required)
        
            !!! quote ""

                Mã tham chiếu đến search chiều về vé máy bay

                Được lấy từ searchID kết hợp với `-R` ở phía cuối
        
        - groupPricedItineraries (Array[GroupPricedItineraryDTO], Optional)

            !!! quote ""

                Thông tin danh sách hành trình trả về theo kết quả tìm kiếm

            - airSupplier (String, Required)

                !!! quote ""

                    Hãng cung cấp (VietnamAirline - VNA, VjetJet - VJ, BamBoo - QH, ...)
            
            - aircraft (String, Optional)

                !!! quote ""

                    Loại máy bay (Airbus A330, Boeing 787, .....)

            - airline (String, Optional)

                !!! quote ""

                    Hãng bay (VJ, VNA, ...)

            - airlineName (String, Optional) 

                !!! quote ""

                    Tên hãng bay (Vietjet Air, Vietnam Airline, Bamboo, ...)
            
            - arrivalDateTime (String, Required) 

                !!! quote ""

                    Ngày giờ đến, sử dụng múi giờ UTC/GMT+7

            - departureDateTime (String, Required)

                !!! quote ""

                    Ngãy giờ bay, sử dụng múi giờ UTC/GMT+7

            - destinationLocationCode (String, Optional)

                !!! quote ""

                    Mã thành phố kết thúc chuyến bay
            
            - destinationCountry (String, Optional)

                !!! quote ""

                    Tên quốc gia kết thúc chuyến bay

            - destinationCountryCode (String, Optional)

                !!! quote ""

                    Mã quốc gia kết thúc chuyến bay
            
            - destinationCity (String, Optional)

                !!! quote ""

                    Tên thành phố kết thúc chuyến bay
            
            - destinationLocationName (String, Optional)

                !!! quote ""

                    Tên sân bay ở điểm dừng
            
            - flightNo (String, Optional)

                !!! quote ""

                    Số hiệu máy bay
            
            - flightNo (String, Optional)

                !!! quote ""

                    Số hiệu máy bay

            - flightType (String, Optional)

                !!! quote ""

                    Loại hình bay bay trong nước hay quốc tế

                    !!! note "Loại hình bay:"

                    - `DOMESTIC`: trong nước

                    - `INTERNATIONAL`: quốc tế
            
            - groupId (String, Required)

                !!! quote ""

                    Mã định danh hành trình trong danh sách hành trình trả về theo kết quả tìm kiếm

            - originCity (String, Optional)

                !!! quote ""
                    
                    Tên thành phố ở điểm khởi hành
            
            - originCountry (String, Optional)

                !!! quote ""

                    Tên quốc gia ở điểm khởi hành
            
            - originCountryCode (String, Optional)

                !!! quote ""

                    Mã ký hiệu quốc gia ở điểm khởi hành
            
            - originLocationCode (String, Optional)

                !!! quote ""

                    Mã thành phố khởi hành chuyến bay

            - originLocationName (String, Optional)

                !!! quote ""

                    Tên sân bay ở điểm khởi hành
            
            - totalPricedItinerary (Integer, Required)

                !!! quote ""

                    Tổng số lượng hành trình chi tiết

            - pricedItineraries (Array[PricedItineraries], Required)

                !!! quote ""

                    Chi tiết hành trình
                
                - airItineraryPricingInfo (AirItineraryPricingInfo, Required)

                    !!! quote ""

                        Thông tin giá chi tiết của hành trình

                    - adultFare (FareBreakdown, Required) 
                    
                        - passengerFare (PassengerFare, Required)

                            !!! quote ""

                                Thông tin giá vé người lớn
                            
                            - baseFare (FareInfo, required)

                                !!! quote ""

                                Thông tin giá vé cơ bản

                                - amount (Double, Required)

                                    !!! quote ""

                                        Số tiền

                                - decimalPlaces (Integer, Optional)

                                    !!! quote ""

                                        Vị trí số thập phân làm tròn đến

                            - equivFare (FareInfo, Optional)
                                
                                !!! quote ""

                                    Tương tự như baseFare

                                    Thông tin phí xuất vé
                            
                            - serviceTax (FareInfo, Required)

                                !!! quote ""

                                    Tương tự như baseFare

                                    Thông tin phí dịch vụ
                            
                            - totalFare (FareInfo, Required)

                                !!! quote ""

                                    Tương tự như baseFare

                                    Thông tin tổng cộng giá vé
                            
                            - surcharges (Array[Surcharge], Required)

                                !!! quote ""

                                    Thông tin phụ phí tính trên mỗi booking / mỗi segment

                        - passengerTypeQuantities (PassengerTypeQuantities, Optional)

                            !!! quote ""

                                Số lượng / loại của hành khách
                            
                            - code (String, Required)

                                !!! quote ""

                                    Mã định danh người lớn / trẻ em / trẻ sơ sinh

                                    Bao gồm: `ADT` - người lớn / `CHD` - trẻ em / `INF` - trẻ sơ sinh

                            - quantity (Integer, Required)

                                !!! quote ""

                                    Số lượng người lớn / trẻ em / trẻ sơ sinh
                    
                    - childFare (PassengerFare, Optional)

                        !!! quote ""

                            Thông tin giá vé trẻ em

                            Tương tự thông tin giá vé người lớn
                    
                    - infantFare (PassengerFare, Optional)

                        !!! quote ""

                            Thông tin giá vé trẻ sơ sinh

                            Tương tự thông tin giá vé người lớn
                    
                    - itinTotalFare (PassengerFare, Required) 

                        !!! quote ""

                            Thông tin tổng giá vé của hành trình

                            Tương tự thông tin giá vé người lớn
                    
                    - fareSourceCode (String, Required) 

                        !!! quote ""

                            Thông tin mã định danh hành trình

                            Được sử dụng để đi lấy thông tin điều kiện vé

                - allowHold (Boolean, Required)

                    !!! quote ""

                        Thông tin cho phép giữ đặt chỗ hay không
                
                - cabinClassName (String, Required)

                    !!! quote ""

                        Thông tin hạng ghế: 

                        - `ECONOMY` - ghế phổ thông 
                        - `PREMIUM` - ghế phổ thông đặc biệt
                        - `BUSINESS` - ghế thương gia
                
                - fightNo (String, Optional)

                    !!! quote ""

                        Thể hiện thông tin số hiệu máy bay
                
                - originDestinationOptions (Array(OriginDestinationOptions), Required)

                    !!! quote ""

                        Thông tin chặn / dừng của hành trình

                    - flightDirection (String, Required)

                        !!! quote ""

                            Thể hiện thông tin chiều bay của hành trình

                            - `D` - chiều đi
                            - `R` - chiều về 
                    
                    - journeyDuration (Integer, Required)

                        !!! quote ""

                            Thể hiện thời gian bay
                    
                    - flightSegments (Array(FlightSegments), Required)

                        !!! quote ""

                            Thể hiện thông tin chi tiết điểm khởi hành / điểm kết thúc trong hành trình

        - page (AirPage, Required)

            !!! quote ""

                Đối tượng mô tả các thông tin về phân trang.

                Số thứ tự của mỗi trang được trả về, phần tử của mỗi trang, tổng số trang

        - duration (Integer, Optional),
        - errors (Array[Error], Optional),
        - infos (Array[Info], Optional),
        - success (Boolean, Optional),
        - textMessage (String, Optional)

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

#### Code 400

> Bad Request

#### Code 401

> Unauthorized

#### Code 403

> Forbidden

#### Code 404

> Not Found

#### Code 500

> Unknown Internal Error

#### Code 503

> Service Unavailable

---

## 3. API lấy thông tin danh sách bộ lọc

!!! info "POST: /api/air-tickets/filter-options"

    Lấy danh sách các giá trị có thể tham áp dụng trên bộ lọc trên kết quả tìm kiếm

### Request Body

=== "Model"
    ???+ example "Request Body"

        - searchId (String, Required)

            !!! quote ""

                Dữ liệu dùng để tham chiếu đến kết quả tìm kiếm 

                Dữ liệu này lấy từ kết quả trả về của tìm vé máy bay

        - departureItinerary (AirItineraryInfo, Optional)

            !!! quote ""

                Thông tin vé chiều đi trong trường hợp lấy filter-options cho vé chiều về

            - airlineCode (String, Required)

                !!! quote ""

                    Ký hiệu hãng bay

                    - `VN`: VietNam Airline
                    - `VJ`: VietJet
                    - `QH`: Bamboo
                    - `BL`: Pacific Airline ...
            
            - groupId (String, Required)    

                !!! quote ""

                    Mã định danh hành trình trong danh sách hành trình trả về theo kết quả tìm kiếm

            - fareSourceCode (String, Required)

                !!! quote ""

                    Thông tin mã định danh hành trình
            
            - supplierCode (String, Required)

                !!! quote ""

                    Mã hãng cũng cấp
            
            - searchId (String, Required)

                !!! quote ""

                    Dữ liệu dùng để tham chiếu đến kết quả tìm kiếm 
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

#### Code 200

> OK

=== "Model"
    ???+ example "Model"
        `Chỉ định danh những trường/field cần thiết`

        - searchId (String, Required) 

            !!! quote ""

                Mã tham chiếu đến search vé máy bay, được lấy từ kết quả search vé máy bay

        - itineraryFilter (ItineraryFilter, Required)

            !!! quote ""

                Thông tin thể hiện các giá trị có thể áp dụng trên kết quả bộ lọc tìm kiếm
            
            - airlineOptions (Array[String], Optional)

                !!! quote ""

                    Thông tin thể hiện các hãng bay với vé có giá thấp nhất

            - cabinClassOptions (Array[String], Optional)

                !!! quote ""

                    Thông tin thể hiện hạng ghế hiện hành
            
            - stopOptions (Array[String], Optional)

                !!! quote ""

                    Thông tin thể hiện chặn dừng hiện hành
            
            - filterToPrice (Double, Optional)

                !!! quote ""

                    Thông tin thể hiện giá vé cao nhất hiện hành
            
            - filterFromPrice (Double, Optional)

                !!! quote ""

                    Thông tin thể hiện giá vé thấp nhất hiện hành

        - duration (Integer, Optional),
        - errors (Array[Error], Optional),
        - infos (Array[Info], Optional),
        - success (Boolean, Optional),
        - textMessage (String, Optional)

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

#### Code 400

> Bad Request

#### Code 401

> Unauthorized

#### Code 403

> Forbidden

#### Code 404

> Not Found

#### Code 500

> Unknown Internal Error

#### Code 503

> Service Unavailable

---

## 4.API lọc / sắp xếp kết quả tìm kiếm chuyến bay

!!! info "POST: /api/air-tickets/filter-availability"

    Lọc và sắp xếp kết quả tìm kiếm chuyến bay

### Paramaters

=== "Parameter"
    ???+ example "Parameters"

        - include-equivfare `query` (Boolean, Optional) 

            Yêu cầu trả thêm thông tin phí xuất vé
        
        - page `query` (Integer, Optional)

            !!! quote ""

                Số trang đang muốn lấy kết quả (VD: 0)
        
        - size `query` (Integer, Optional)

            !!! quote ""

                Số kết quả muốn lấy trong 1 trang (VD: 20)

        - sort `query` (String, Optional) 

            !!! quote ""

                Sắp xếp kết quả theo giá trị của thuộc tính trả về tăng dần hay giảm dần (VD: propertiesName,desc / propertiesName,asc)

=== "Example"
    ?include-equivfare=`false`&page=`0`&size=`20`&sort=`departureDate,asc`

### Request Body

=== "Model"
    ???+ example "Request Body"

        - searchId (String, Required)

            !!! quote ""

                Dữ liệu dùng để tham chiếu đến kết quả tìm kiếm 

                Dữ liệu này lấy từ kết quả trả về của tìm vé máy bay

        - departureItinerary (AirItineraryInfo, Optional)

            !!! quote ""

                Thông tin vé chiều đi trong trường hợp lấy filter-availability cho vé chiều về

            - airlineCode (String, Required)

                !!! quote ""

                    Ký hiệu hãng bay

                    - `VN`: VietNam Airline
                    - `VJ`: VietJet
                    - `QH`: Bamboo
                    - `BL`: Pacific Airline ...
            
            - groupId (String, Optional)    

                !!! quote ""

                    Mã định danh hành trình trong danh sách hành trình trả về theo kết quả tìm kiếm

            - fareSourceCode (String, Required)

                !!! quote ""

                    Thông tin mã định danh hành trình
            
            - supplierCode (String, Required)

                !!! quote ""

                    Mã hãng cũng cấp
            
            - searchId (String, Required)

                !!! quote ""

                    Dữ liệu dùng để tham chiếu đến kết quả tìm kiếm 

        - filter (ItineraryFilter, Required)

            !!! quote ""

                Dùng để đưa các tiêu chí lọc và sắp xếp mong muốn vào 
            
            - cabinClassOptions (Array[String], Optional)

                !!! quote ""

                    Thông tin hạng ghế muốn đưa vào lọc và sắp xếp
            
            - step (String, Required)

                !!! quote ""

                    Thông tin dùng để phân biệt giữa chiều đi và chiều về

                    - `1` : chiều đi
                    - `2` : chiều về
            
            - flightType (String, Required)

                !!! quote ""

                    Thông tin loại chuyến bay

                    - `DOMESTIC`: trong nước
                    - `INTERNATIONAL`: quốc tế
            
            - stopOption (Array[String], Optional) 

                !!! quote ""

                    Thông tin điểm dừng

            - airlineOptions (Array[String], Optional) 

                !!! quote ""

                    Thông tin hãng bay
            
            - departureDateTimeOptions (Array[String], Optional)

                !!! quote ""

                    Thông tin giờ khởi hành bắt đầu ở khoảng hay thời điểm nào
                    
                    VD: departureDateTimeOptions: `["+18", "+12-18"]`

                    - `+18`: từ 18h đến 24h
                    - `+12-18`: từ 12h đến 18h
            
            - arrivalDateTimeReturnOptions (Array[String], Optional)

                !!! quote ""

                    Thông tin giờ kết thúc bắt đầu ở khoảng hay thời điểm nào
                    
                    VD: arrivalDateTimeReturnOptions: `["+18", "+12-18"]`

                    - `+18`: từ 18h đến 24h
                    - `+12-18`: từ 12h đến 18h
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

#### Code 200

> OK

=== "Model"
    ???+ example "Model"
        `Chỉ định danh những trường/field cần thiết`

        - searchId (String, Required) 

            !!! quote ""

                Mã tham chiếu đến search vé máy bay, được lấy từ kết quả search vé máy bay
        
        - groupPricedItineraries (Array[GroupPricedItineraryDTO], Optional)

            !!! quote ""

                Thông tin danh sách hành trình trả về theo kết quả tìm kiếm

            - airSupplier (String, Required)

                !!! quote ""

                    Hãng cung cấp (VietnamAirline - VNA, VjetJet - VJ, BamBoo - QH, ...)
            
            - aircraft (String, Optional)

                !!! quote ""

                    Loại máy bay (Airbus A330, Boeing 787, .....)

            - airline (String, Optional)

                !!! quote ""

                    Hãng bay (VJ, VNA, ...)

            - airlineName (String, Optional) 

                !!! quote ""

                    Tên hãng bay (Vietjet Air, Vietnam Airline, Bamboo, ...)
            
            - arrivalDateTime (String, Required) 

                !!! quote ""

                    Ngày giờ đến, sử dụng múi giờ UTC/GMT+7

            - departureDateTime (String, Required)

                !!! quote ""

                    Ngãy giờ bay, sử dụng múi giờ UTC/GMT+7

            - destinationLocationCode (String, Optional)

                !!! quote ""

                    Mã thành phố kết thúc chuyến bay
            
            - destinationCountry (String, Optional)

                !!! quote ""

                    Tên quốc gia kết thúc chuyến bay

            - destinationCountryCode (String, Optional)

                !!! quote ""

                    Mã quốc gia kết thúc chuyến bay
            
            - destinationCity (String, Optional)

                !!! quote ""

                    Tên thành phố kết thúc chuyến bay
            
            - destinationLocationName (String, Optional)

                !!! quote ""

                    Tên sân bay ở điểm dừng
            
            - flightNo (String, Optional)

                !!! quote ""

                    Số hiệu máy bay
            
            - flightNo (String, Optional)

                !!! quote ""

                    Số hiệu máy bay

            - flightType (String, Optional)

                !!! quote ""

                    Loại hình bay bay trong nước hay quốc tế

                    !!! note "Loại hình bay:"

                    - `DOMESTIC`: trong nước

                    - `INTERNATIONAL`: quốc tế
            
            - groupId (String, Required)

                !!! quote ""

                    Mã định danh hành trình trong danh sách hành trình trả về theo kết quả tìm kiếm

            - originCity (String, Optional)

                !!! quote ""
                    
                    Tên thành phố ở điểm khởi hành
            
            - originCountry (String, Optional)

                !!! quote ""

                    Tên quốc gia ở điểm khởi hành
            
            - originCountryCode (String, Optional)

                !!! quote ""

                    Mã ký hiệu quốc gia ở điểm khởi hành
            
            - originLocationCode (String, Optional)

                !!! quote ""

                    Mã thành phố khởi hành chuyến bay

            - originLocationName (String, Optional)

                !!! quote ""

                    Tên sân bay ở điểm khởi hành
            
            - totalPricedItinerary (Integer, Required)

                !!! quote ""

                    Tổng số lượng hành trình chi tiết

            - pricedItineraries (Array[PricedItineraries], Required)

                !!! quote ""

                    Chi tiết hành trình
                
                - airItineraryPricingInfo (AirItineraryPricingInfo, Required)

                    !!! quote ""

                        Thông tin giá chi tiết của hành trình

                    - adultFare (FareBreakdown, Required) 
                    
                        - passengerFare (PassengerFare, Required)

                            !!! quote ""

                                Thông tin giá vé người lớn
                            
                            - baseFare (FareInfo, required)

                                !!! quote ""

                                Thông tin giá vé cơ bản

                                - amount (Double, Required)

                                    !!! quote ""

                                        Số tiền

                                - decimalPlaces (Integer, Optional)

                                    !!! quote ""

                                        Vị trí số thập phân làm tròn đến

                            - equivFare (FareInfo, Optional)
                                
                                !!! quote ""

                                    Tương tự như baseFare

                                    Thông tin phí xuất vé
                            
                            - serviceTax (FareInfo, Required)

                                !!! quote ""

                                    Tương tự như baseFare

                                    Thông tin phí dịch vụ
                            
                            - totalFare (FareInfo, Required)

                                !!! quote ""

                                    Tương tự như baseFare

                                    Thông tin tổng cộng giá vé
                            
                            - surcharges (Array[Surcharge], Required)

                                !!! quote ""

                                    Thông tin phụ phí tính trên mỗi booking / mỗi segment

                        - passengerTypeQuantities (PassengerTypeQuantities, Optional)

                            !!! quote ""

                                Số lượng / loại của hành khách
                            
                            - code (String, Required)

                                !!! quote ""

                                    Mã định danh người lớn / trẻ em / trẻ sơ sinh

                                    Bao gồm: `ADT` - người lớn / `CHD` - trẻ em / `INF` - trẻ sơ sinh

                            - quantity (Integer, Required)

                                !!! quote ""

                                    Số lượng người lớn / trẻ em / trẻ sơ sinh
                    
                    - childFare (PassengerFare, Optional)

                        !!! quote ""

                            Thông tin giá vé trẻ em

                            Tương tự thông tin giá vé người lớn
                    
                    - infantFare (PassengerFare, Optional)

                        !!! quote ""

                            Thông tin giá vé trẻ sơ sinh

                            Tương tự thông tin giá vé người lớn
                    
                    - itinTotalFare (PassengerFare, Required) 

                        !!! quote ""

                            Thông tin tổng giá vé của hành trình

                            Tương tự thông tin giá vé người lớn
                    
                    - fareSourceCode (String, Required) 

                        !!! quote ""

                            Thông tin mã định danh hành trình

                            Được sử dụng để đi lấy thông tin điều kiện vé

                - allowHold (Boolean, Required)

                    !!! quote ""

                        Thông tin cho phép giữ đặt chỗ hay không
                
                - cabinClassName (String, Required)

                    !!! quote ""

                        Thông tin hạng ghế: 

                        - `ECONOMY` - ghế phổ thông 
                        - `PREMIUM` - ghế phổ thông đặc biệt
                        - `BUSINESS` - ghế thương gia
                
                - fightNo (String, Optional)

                    !!! quote ""

                        Thể hiện thông tin số hiệu máy bay
                
                - originDestinationOptions (Array(OriginDestinationOptions), Required)

                    !!! quote ""

                        Thông tin chặn / dừng của hành trình

                    - flightDirection (String, Required)

                        !!! quote ""

                            Thể hiện thông tin chiều bay của hành trình

                            - `D` - chiều đi
                            - `R` - chiều về 
                    
                    - journeyDuration (Integer, Required)

                        !!! quote ""

                            Thể hiện thời gian bay
                    
                    - flightSegments (Array(FlightSegments), Required)

                        !!! quote ""

                            Thể hiện thông tin chi tiết điểm khởi hành / điểm kết thúc trong hành trình

        - page (AirPage, Required)

            !!! quote ""

                Đối tượng mô tả các thông tin về phân trang.

                Số thứ tự của mỗi trang được trả về, phần tử của mỗi trang, tổng số trang

        - duration (Integer, Optional),
        - errors (Array[Error], Optional),
        - infos (Array[Info], Optional),
        - success (Boolean, Optional),
        - textMessage (String, Optional)

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
#### Code 400

> Bad Request

#### Code 401

> Unauthorized

#### Code 403

> Forbidden

#### Code 404

> Not Found

#### Code 500

> Unknown Internal Error

#### Code 503

> Service Unavailable

---

## 5.API lấy danh sách vé mở bán trên một chuyến bay

!!! info "POST: /api/air-tickets/group-itinerary/{id}"

    Lấy danh sách vé được mở bán trên một chuyến bay cụ thể

### Paramaters

=== "Parameter"
    ???+ example "Parameters"

        - id `path` (String, Required)

            !!! quote ""

                Dùng để tham chiếu đến danh sách các vé được mở bán trên một chuyến bay

        - include-equivfare `query` (Boolean, Optional) 

            !!! quote ""

             Yêu cầu trả thêm thông tin phí xuất vé
        
        - page `query` (Integer, Optional)

            !!! quote ""

                Số trang đang muốn lấy kết quả (VD: 0)
        
        - size `query` (Integer, Optional)

            !!! quote ""

                Số kết quả muốn lấy trong 1 trang (VD: 20)

        - sort `query` (String, Optional) 

            !!! quote ""

                Sắp xếp kết quả theo giá trị của thuộc tính trả về tăng dần hay giảm dần (VD: propertiesName,desc / propertiesName,asc)

=== "Example"
    `052a9f35-12eb-430b-baa0-7ea85a98e8b3`?include-equivfare=`false`&page=`0`&size=`20`&sort=`departureDate,asc`

### Request Body

=== "Model"
    ???+ example "Request Body"

        - searchId (String, Required)

            !!! quote ""

                Dữ liệu dùng để tham chiếu đến kết quả tìm kiếm 

                Dữ liệu này lấy từ kết quả trả về của tìm vé máy bay

        - departureItinerary (AirItineraryInfo, Optional)

            !!! quote ""

                Thông tin vé chiều đi trong trường hợp lấy filter-availability cho vé chiều về

            - airlineCode (String, Required)

                !!! quote ""

                    Ký hiệu hãng bay

                    - `VN`: VietNam Airline
                    - `VJ`: VietJet
                    - `QH`: Bamboo
                    - `BL`: Pacific Airline ...
            
            - groupId (String, Required)    

                !!! quote ""

                    Mã định danh hành trình trong danh sách hành trình trả về theo kết quả tìm kiếm

            - fareSourceCode (String, Required)

                !!! quote ""

                    Thông tin mã định danh hành trình
            
            - supplierCode (String, Required)

                !!! quote ""

                    Mã hãng cũng cấp
            
            - searchId (String, Required)

                !!! quote ""

                    Dữ liệu dùng để tham chiếu đến kết quả tìm kiếm 

        - filter (ItineraryFilter, Required)

            !!! quote ""

                Dùng để đưa các tiêu chí lọc và sắp xếp mong muốn vào 
            
            - cabinClassOptions (Array[String], Optional)

                !!! quote ""

                    Thông tin hạng ghế muốn đưa vào lọc và sắp xếp
            
            - step (String, Required)

                !!! quote ""

                    Thông tin dùng để phân biệt giữa chiều đi và chiều về

                    - `1` : chiều đi
                    - `2` : chiều về
            
            - flightType (String, Required)

                !!! quote ""

                    Thông tin loại chuyến bay
                    
                    - `DOMESTIC`: trong nước
                    - `INTERNATIONAL`: quốc tế
            
            - stopOption (Array[String], Optional) 

                !!! quote ""

                    Thông tin điểm dừng

            - airlineOptions (Array[String], Optional) 

                !!! quote ""

                    Thông tin hãng bay
            
            - departureDateTimeOptions (Array[String], Optional)

                !!! quote ""

                    Thông tin giờ khởi hành bắt đầu ở khoảng hay thời điểm nào
                    
                    VD: departureDateTimeOptions: `["+18", "+12-18"]`

                    - `+18`: từ 18h đến 24h
                    - `+12-18`: từ 12h đến 18h
            
            - arrivalDateTimeReturnOptions (Array[String], Optional)

                !!! quote ""

                    Thông tin giờ kết thúc bắt đầu ở khoảng hay thời điểm nào
                    
                    VD: arrivalDateTimeReturnOptions: `["+18", "+12-18"]`

                    - `+18`: từ 18h đến 24h
                    - `+12-18`: từ 12h đến 18h
            
            - groupId (String, Required)

                !!! quote ""

                    Mã định danh hành trình trong danh sách hành trình lấy được từ kết quả tìm kiếm
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

#### Code 200

> OK

=== "Model"
    ???+ example "Model"
        `Chỉ định danh những trường/field cần thiết`

        - searchId (String, Required) 

            !!! quote ""

                Mã tham chiếu đến search vé máy bay, được lấy từ kết quả search vé máy bay
        
        - groupPricedItineraries (Array[GroupPricedItineraryDTO], Optional)

            !!! quote ""

                Thông tin danh sách hành trình trả về theo kết quả tìm kiếm

            - airSupplier (String, Required)

                !!! quote ""

                    Hãng cung cấp (VietnamAirline - VNA, VjetJet - VJ, BamBoo - QH, ...)
            
            - aircraft (String, Optional)

                !!! quote ""

                    Loại máy bay (Airbus A330, Boeing 787, .....)

            - airline (String, Optional)

                !!! quote ""

                    Hãng bay (VJ, VNA, ...)

            - airlineName (String, Optional) 

                !!! quote ""

                    Tên hãng bay (Vietjet Air, Vietnam Airline, Bamboo, ...)
            
            - arrivalDateTime (String, Required) 

                !!! quote ""

                    Ngày giờ đến, sử dụng múi giờ UTC/GMT+7

            - departureDateTime (String, Required)

                !!! quote ""

                    Ngãy giờ bay, sử dụng múi giờ UTC/GMT+7

            - destinationLocationCode (String, Optional)

                !!! quote ""

                    Mã thành phố kết thúc chuyến bay
            
            - destinationCountry (String, Optional)

                !!! quote ""

                    Tên quốc gia kết thúc chuyến bay

            - destinationCountryCode (String, Optional)

                !!! quote ""

                    Mã quốc gia kết thúc chuyến bay
            
            - destinationCity (String, Optional)

                !!! quote ""

                    Tên thành phố kết thúc chuyến bay
            
            - destinationLocationName (String, Optional)

                !!! quote ""

                    Tên sân bay ở điểm dừng
            
            - flightNo (String, Optional)

                !!! quote ""

                    Số hiệu máy bay
            
            - flightNo (String, Optional)

                !!! quote ""

                    Số hiệu máy bay

            - flightType (String, Optional)

                !!! quote ""

                    Loại hình bay bay trong nước hay quốc tế

                    !!! note "Loại hình bay:"

                    - `DOMESTIC`: trong nước

                    - `INTERNATIONAL`: quốc tế
            
            - groupId (String, Required)

                !!! quote ""

                    Mã định danh hành trình trong danh sách hành trình trả về theo kết quả tìm kiếm

            - originCity (String, Optional)

                !!! quote ""
                    
                    Tên thành phố ở điểm khởi hành
            
            - originCountry (String, Optional)

                !!! quote ""

                    Tên quốc gia ở điểm khởi hành
            
            - originCountryCode (String, Optional)

                !!! quote ""

                    Mã ký hiệu quốc gia ở điểm khởi hành
            
            - originLocationCode (String, Optional)

                !!! quote ""

                    Mã thành phố khởi hành chuyến bay

            - originLocationName (String, Optional)

                !!! quote ""

                    Tên sân bay ở điểm khởi hành
            
            - totalPricedItinerary (Integer, Required)

                !!! quote ""

                    Tổng số lượng hành trình chi tiết

            - pricedItineraries (Array[PricedItineraries], Required)

                !!! quote ""

                    Chi tiết hành trình
                
                - airItineraryPricingInfo (AirItineraryPricingInfo, Required)

                    !!! quote ""

                        Thông tin giá chi tiết của hành trình

                    - adultFare (FareBreakdown, Required) 
                    
                        - passengerFare (PassengerFare, Required)

                            !!! quote ""

                                Thông tin giá vé người lớn
                            
                            - baseFare (FareInfo, required)

                                !!! quote ""

                                Thông tin giá vé cơ bản

                                - amount (Double, Required)

                                    !!! quote ""

                                        Số tiền

                                - decimalPlaces (Integer, Optional)

                                    !!! quote ""

                                        Vị trí số thập phân làm tròn đến

                            - equivFare (FareInfo, Optional)
                                
                                !!! quote ""

                                    Tương tự như baseFare

                                    Thông tin phí xuất vé
                            
                            - serviceTax (FareInfo, Required)

                                !!! quote ""

                                    Tương tự như baseFare

                                    Thông tin phí dịch vụ
                            
                            - totalFare (FareInfo, Required)

                                !!! quote ""

                                    Tương tự như baseFare

                                    Thông tin tổng cộng giá vé
                            
                            - surcharges (Array[Surcharge], Required)

                                !!! quote ""

                                    Thông tin phụ phí tính trên mỗi booking / mỗi segment

                        - passengerTypeQuantities (PassengerTypeQuantities, Optional)

                            !!! quote ""

                                Số lượng / loại của hành khách
                            
                            - code (String, Required)

                                !!! quote ""

                                    Mã định danh người lớn / trẻ em / trẻ sơ sinh

                                    Bao gồm: `ADT` - người lớn / `CHD` - trẻ em / `INF` - trẻ sơ sinh

                            - quantity (Integer, Required)

                                !!! quote ""

                                    Số lượng người lớn / trẻ em / trẻ sơ sinh
                    
                    - childFare (PassengerFare, Optional)

                        !!! quote ""

                            Thông tin giá vé trẻ em

                            Tương tự thông tin giá vé người lớn
                    
                    - infantFare (PassengerFare, Optional)

                        !!! quote ""

                            Thông tin giá vé trẻ sơ sinh

                            Tương tự thông tin giá vé người lớn
                    
                    - itinTotalFare (PassengerFare, Required) 

                        !!! quote ""

                            Thông tin tổng giá vé của hành trình

                            Tương tự thông tin giá vé người lớn
                    
                    - fareSourceCode (String, Required) 

                        !!! quote ""

                            Thông tin mã định danh hành trình

                            Được sử dụng để đi lấy thông tin điều kiện vé

                - allowHold (Boolean, Required)

                    !!! quote ""

                        Thông tin cho phép giữ đặt chỗ hay không
                
                - cabinClassName (String, Required)

                    !!! quote ""

                        Thông tin hạng ghế: 

                        - `ECONOMY` - ghế phổ thông 
                        - `PREMIUM` - ghế phổ thông đặc biệt
                        - `BUSINESS` - ghế thương gia
                
                - fightNo (String, Optional)

                    !!! quote ""

                        Thể hiện thông tin số hiệu máy bay
                
                - originDestinationOptions (Array(OriginDestinationOptions), Required)

                    !!! quote ""

                        Thông tin chặn / dừng của hành trình

                    - flightDirection (String, Required)

                        !!! quote ""

                            Thể hiện thông tin chiều bay của hành trình

                            - `D` - chiều đi
                            - `R` - chiều về 
                    
                    - journeyDuration (Integer, Required)

                        !!! quote ""

                            Thể hiện thời gian bay
                    
                    - flightSegments (Array(FlightSegments), Required)

                        !!! quote ""

                            Thể hiện thông tin chi tiết điểm khởi hành / điểm kết thúc trong hành trình

        - page (AirPage, Required)

            !!! quote ""

                Đối tượng mô tả các thông tin về phân trang.

                Số thứ tự của mỗi trang được trả về, phần tử của mỗi trang, tổng số trang

        - duration (Integer, Optional),
        - errors (Array[Error], Optional),
        - infos (Array[Info], Optional),
        - success (Boolean, Optional),
        - textMessage (String, Optional)

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
#### Code 400

> Bad Request

#### Code 401

> Unauthorized

#### Code 403

> Forbidden

#### Code 404

> Not Found

#### Code 500

> Unknown Internal Error

#### Code 503

> Service Unavailable

---

## 6.API lấy điều kiện vé

!!! info "POST: /api/air-tickets/farerules"

    Lấy điều kiện vé của chuyến bay

### Paramaters

=== "Parameter"
    ???+ example "Parameters"

        - language `query` (Boolean, Optional) 

            !!! quote ""

                Ngôn ngữ muốn lấy

=== "Example"
    `?language=vi`

### Request Body

=== "Model"
    ???+ example "Request Body"

        - searchId (String, Required)

            !!! quote ""

                Dữ liệu dùng để tham chiếu đến kết quả tìm kiếm 

                Dữ liệu này lấy từ kết quả trả về của tìm vé máy bay

        - groupId (String, Required)    

            !!! quote ""

                Mã định danh hành trình trong danh sách hành trình trả về theo kết quả tìm kiếm
        
        - fareSourceCode(String, Required)

            !!! quote ""

                Thông tin mã định danh hành trình

=== "Example"

    ```json
        {
            "fareSourceCode": "dom07b2da7b-3232-4294-9278-b35fb6307714",
            "groupId": "27b091a7-62b8-4ce2-b45b-eda3340d7673",
            "searchId": "ATD::210720::dc96e1a9-c39e-4f48-974e-e0be6abb45c7"
        }

    ```

### Response

#### Code 200

> OK

=== "Model"
    ???+ example "Model"
        `Chỉ định danh những trường/field cần thiết`

        - fareRules (Array[FareRules], Required)

            !!! quote ""

                Danh sách điều kiện vé trả về
            
            - arrivalAirportLocationCode (String, Required)

                !!! quote ""

                    Điểm đến
            
            - departureAirportLocationCode (String, Required)

                !!! quote ""

                    Điểm khởi hành

            - departureDateTime (String, Required)

                !!! quote ""

                    Giờ khởi hành 

                    Định danh theo  `yyyy-MM-dd'T'HH:mm:ss'Z'`

            - arrivalDateTime (String, Required)

                !!! quote ""

                    Giờ đến

                    Định dạng theo `yyyy-MM-dd'T'HH:mm:ss'Z'`
            - fareRuleItems (Array[FareRuleItem], Required) 

                !!! quote ""

                    Danh sách chi tiết điều kiện vé

                - detail (String, Required)

                    !!! quote ""

                        Chi tiết thông tin điều kiện vé

                        Định dạng HTML
                    
                - title (String, Required) 

                    !!! quote ""

                        Thông tin cho biết điều kiện vé chiều đi / điều kiện vé chiều về

        - duration (Integer, Optional),
        - errors (Array[Error], Optional),
        - infos (Array[Info], Optional),
        - success (Boolean, Optional),
        - textMessage (String, Optional)

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
#### Code 400

> Bad Request

#### Code 401

> Unauthorized

#### Code 403

> Forbidden

#### Code 404

> Not Found

#### Code 500

> Unknown Internal Error

#### Code 503

> Service Unavailable

---