# Document Hotel API Searching

---

## 1. API Tìm kiếm địa điểm, khách sạn theo từ khoá 

!!! info "GET: api/v3/hotel/search-keyword"
    Tìm kiếm địa điểm, khách sạn theo từ khoá.

### Parameters
=== "Parameters"
    ???+ example "Parameters"
        - keyword `query` (String, optional)

            !!! quote "" 
            
                  Từ khoá tìm kiếm 

        - language `query` (String, Required)

            !!! quote "" 
            
                Ngôn ngữ 

                - `vi` : Tiếng Việt 
                
                - `en`: Tiếng Anh 
        
        - pageNumber `query` (String, Optional)
            
            !!! quote "" 
                
                Trang số

        - pageSize `query` (String, Optional)
            
            !!! quote "" 
                
                Số phần tử trên trang

=== "Example"
    - Tìm kiếm theo từ khoá `ho` 
    ```
    ?keyword=ho&language=vi&pageNumber=0&pageSize=15
    ```

### Response
#### Code 200
=== "Model" 
    ???+ example "Model"
        - result (SearchKeywordResult, optional)

            !!! quote ""
        
                Thông tin kết quả trả về 
        
            - contents (Array[Content], optional),
            
                !!! quote "" 
                    
                    Danh sách khu vực, khách sạn 

                - searchCode (String, optional),
            
                    !!! quote "" 

                        Mã định danh tìm kiếm  

                - searchType (string, optional) = [`CONTINENT`, `COUNTRY`, `PROVINCE_STATE`, `HIGH_LEVEL_REGION`, `MULTI_CITY_VICINITY`, `CITY`, `NEIGHBORHOOD`, `AIRPORT`, `POINT_OF_INTEREST`, `TRAIN_STATION`, `METRO_STATION`, `HOTEL`],
            
                    !!! quote "" 

                        Loại tìm kiếm  

                - name (String, optional),
            
                    !!! quote "" 

                        Tên khu vực, khách sạn   

                - supplier (String, optional) = [`EXPEDIA`, `AXISROOM`, `BEDLINKER`, `VINPEARL`],
            
                    !!! quote "" 

                        Nhà cung cấp  

                - address (Address, optional)
                
                    !!! quote "" 
                        
                        Thông tin địa chỉ khách sạn

                    - city (string, optional),
                    
                    !!! quote "" 
                        
                        Thành phố

                    - countryCode (string, optional),
                    
                        !!! quote "" 
                        
                            Mã quốc gia

                    - countryName (string, optional),
                    
                        !!! quote "" 
                        
                            Tên quốc gia

                    - lineOne (string, optional),
                    
                        !!! quote "" 
                        
                            Địa chỉ dòng 1

                    - lineTow (string, optional),
                    
                        !!! quote "" 
                        
                            Địa chỉ dòng 2

                    - postalCode (string, optional),
                    
                        !!! quote "" 
                        
                            Mã bưu điện

                    - stateProvinceCode (string, optional),
                    
                        !!! quote "" 
                        
                            Mã tỉnh thành

                    - stateProvinceName (string, optional)
            
                        !!! quote "" 

                            Tên tỉnh thành

                - tags (Array[String], optional),
                    
                    !!! quote "" 
        
                        Thẻ  

        - duration (integer, optional),
        - errors (Array[Error], optional),
        - infos (Array[Info], optional),
        - success (boolean, optional),
        - textMessage (string, optional)
=== "Example"
    ```json
    {
        "result":
        {
            "page":
            {
                "pageSize": 15,
                "pageNumber": 0,
                "totalPage": 1,
                "totalItems": 9
            },
            "contents":
            [
                {
                    "name": "Thành phố Hồ Chí Minh",
                    "searchCode": "178262",
                    "searchType": "MULTI_CITY_VICINITY",
                    "supplier": "EXPEDIA",
                    "address":
                    {
                        "lineOne": "Thành phố Hồ Chí Minh, Việt Nam",
                        "lineTow": "",
                        "stateProvinceCode": "",
                        "stateProvinceName": "",
                        "postalCode": "",
                        "city": "",
                        "countryCode": "",
                        "countryName": ""
                    },
                    "propertyCount": 1815,
                    "tags":
                    [
                        "popular"
                    ]
                },
                {
                    "name": "Hội An",
                    "searchCode": "6034264",
                    "searchType": "MULTI_CITY_VICINITY",
                    "supplier": "EXPEDIA",
                    "address":
                    {
                        "lineOne": "Quảng Nam, Việt Nam",
                        "lineTow": "",
                        "stateProvinceCode": "",
                        "stateProvinceName": "",
                        "postalCode": "",
                        "city": "",
                        "countryCode": "",
                        "countryName": ""
                    },
                    "propertyCount": 745,
                    "tags":
                    [
                        "popular"
                    ]
                },
                {
                    "name": "Nha Trang",
                    "searchCode": "6054439",
                    "searchType": "MULTI_CITY_VICINITY",
                    "supplier": "EXPEDIA",
                    "address":
                    {
                        "lineOne": "Khánh Hòa, Việt Nam",
                        "lineTow": "",
                        "stateProvinceCode": "",
                        "stateProvinceName": "",
                        "postalCode": "",
                        "city": "",
                        "countryCode": "",
                        "countryName": ""
                    },
                    "propertyCount": 698,
                    "tags":
                    [
                        "popular"
                    ]
                },
                {
                    "name": "Hòa Bình",
                    "searchCode": "6257831",
                    "searchType": "PROVINCE_STATE",
                    "supplier": "EXPEDIA",
                    "address":
                    {
                        "lineOne": "Việt Nam",
                        "lineTow": "",
                        "stateProvinceCode": "",
                        "stateProvinceName": "",
                        "postalCode": "",
                        "city": "",
                        "countryCode": "",
                        "countryName": ""
                    },
                    "propertyCount": 28,
                    "tags":
                    []
                },
                {
                    "name": "Khánh Hòa",
                    "searchCode": "6257974",
                    "searchType": "PROVINCE_STATE",
                    "supplier": "EXPEDIA",
                    "address":
                    {
                        "lineOne": "Việt Nam",
                        "lineTow": "",
                        "stateProvinceCode": "",
                        "stateProvinceName": "",
                        "postalCode": "",
                        "city": "",
                        "countryCode": "",
                        "countryName": ""
                    },
                    "propertyCount": 701,
                    "tags":
                    []
                },
                {
                    "name": "Thanh Hóa",
                    "searchCode": "6257865",
                    "searchType": "PROVINCE_STATE",
                    "supplier": "EXPEDIA",
                    "address":
                    {
                        "lineOne": "Việt Nam",
                        "lineTow": "",
                        "stateProvinceCode": "",
                        "stateProvinceName": "",
                        "postalCode": "",
                        "city": "",
                        "countryCode": "",
                        "countryName": ""
                    },
                    "propertyCount": 49,
                    "tags":
                    []
                },
                {
                    "name": "Huyện Mai Châu",
                    "searchCode": "553248635964611967",
                    "searchType": "PROVINCE_STATE",
                    "supplier": "EXPEDIA",
                    "address":
                    {
                        "lineOne": "Hòa Bình, Việt Nam",
                        "lineTow": "",
                        "stateProvinceCode": "",
                        "stateProvinceName": "",
                        "postalCode": "",
                        "city": "",
                        "countryCode": "",
                        "countryName": ""
                    },
                    "propertyCount": 21,
                    "tags":
                    []
                },
                {
                    "name": "Huyện Hòa An",
                    "searchCode": "553248635975748781",
                    "searchType": "PROVINCE_STATE",
                    "supplier": "EXPEDIA",
                    "address":
                    {
                        "lineOne": "Cao Bằng, Việt Nam",
                        "lineTow": "",
                        "stateProvinceCode": "",
                        "stateProvinceName": "",
                        "postalCode": "",
                        "city": "",
                        "countryCode": "",
                        "countryName": ""
                    },
                    "propertyCount": 9,
                    "tags":
                    []
                },
                {
                    "name": "Huyện Hòa Thành",
                    "searchCode": "553248635975750551",
                    "searchType": "PROVINCE_STATE",
                    "supplier": "EXPEDIA",
                    "address":
                    {
                        "lineOne": "Tây Ninh, Việt Nam",
                        "lineTow": "",
                        "stateProvinceCode": "",
                        "stateProvinceName": "",
                        "postalCode": "",
                        "city": "",
                        "countryCode": "",
                        "countryName": ""
                    },
                    "propertyCount": 1,
                    "tags":
                    []
                }
            ]
        },
        "duration": 0,
        "textMessage": null,
        "errors": null,
        "infos": null,
        "success": true
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

## 2. API Tìm kiếm khách sạn với lựa chọn giá tốt nhất (search-best-rate)

!!! info "GET: /api/v3/hotel/search-best-rates"
    Trả về kết quả tìm kiếm khách sạn với lựa chọn giá tốt nhất.

    Dữ liệu sẽ được caching trong một khoảng thời gian theo với key là searchId. Thời gian caching khoảng 15 phút, thời gian này có thể bị thay đổi.

    Cho phép lọc và sắp xếp kết quả trả về.

    !!! note "Chú ý"
        Lọc theo tọa độ, khoảng cách yêu cầu 3 tham số: 
        
        - filterGeoDistanceLat  
        - filterGeoDistanceLon
        - filterGeoDistanceMeters

### Parameters 
???+ example "Parameters"
    - rateOption `query` (String, optional)

        !!! quote ""

            Tuỳ chọn giá. Có 2 tuỳ chọn giá là `OTA, TA`. Mặc định là `OTA`.

            !!! note "Chú ý"

                - Chỉ nhưng đối tác ký hợp đồng TA mới được sử dụng tuỳ chọn giá TA.  
                
                - Muốn lấy cả 2 option giá thì `?rateOption=TA,OTA&...`
 

    - searchCode `query` (String, Required)

        !!! quote ""

            Mã khu vực hoặc mã khách sạn.

            - Trường hợp mong muốn tìm kiếm theo danh sách khách sạn, trước tiên phải [lấy danh sách khách sạn](/dev-guide/api-hotel/api-searching/#4-api-lay-danh-sach-khach-san) có chứa id để tìm kiếm. 
            
            - Cú pháp tìm nhiều khách sạn `...&searchCode=id1,id2,id3&searchType=HOTEL&supplier=GOTADI&...` 

    - searchType `query` (String, Required)

        !!! quote "" 
            
            Kiểu mã khu vực. Vd: CITY, HOTEL, ...

    - language `query` (String, Required)

        !!! quote "" 
            
            Ngôn ngữ. (vi, en)

    - currency `query` (String, Required)

        !!! quote "" 
            
            Tiền tệ. (VND, USD)

    - checkIn `query` (String, Required)
        
        !!! quote ""

            Ngày nhận phòng.  
            Định dạng: `yyyy-MM-dd`

    - checkOut `query` (String, Required)

        !!! quote "" 
            
            Ngày trả phòng.  
            Định dạng: `yyyy-MM-dd`

    - paxInfos `query` (String[], Required)
        
        !!! quote ""

            Thông tin phòng và khách ở   
            Định dạng: `SoNguoiLon-TuoiTreEm1,TuoiTreEm2`  

            Ví dụ:

            - 2 người lớn và 2 trẻ em, 1 trẻ 4 tuổi, 1 trẻ 6 tuổi: `...&paxInfos=2-4,6&...`

            - 2 phòng, phòng 1 gồm 2 người lớn, phòng 2 gồm 2 người lớn và 2 trẻ em, 1 trẻ em 4 tuổi và 1 trẻ em 6 tuổi: `...&paxInfos=2&paxInfos=2-4,6&...`  

    - supplier `query` (String, Required)

        !!! quote "" 
        
            Nhà cung cấp, Lấy thông tin từ kết quả trả về mục 4.2

    - filterHotelName `query` (String, Optional)

        !!! quote "" 
            
            Lọc theo tên bắt đầu bằng

    - filterHotelCategories `query` (String, Optional)

        !!! quote "" 
        
            Lọc theo danh mục khách sạn

    - filterFromPrice `query` (Double, Optional)
        
        !!! quote "" 
            
            Lọc theo giá bắt đầu từ

    - filterToPrice `query` (Double, Optional)
        
        !!! quote "" 
            
            Lọc theo giá kết thúc đến

    - filterFromStarRating `query` (Double, Optional)
        
        !!! quote "" 
            
            Lọc theo hạng sao bắt đầu từ

    - filterToStarRating `query` (Double, Optional)
        
        !!! quote "" 
            
            Lọc theo hạng sao kết thúc đến 

    - filterFromGuestRating `query` (Double, Optional)
        
        !!! quote "" 
            
            Lọc theo đánh giá của khách bắt đầu từ

    - filterToGuestRating `query` (Double, Optional)
        
        !!! quote "" 
            
            Lọc theo đánh giá của khách kết thúc đến 

    - filterAmenities `query` (String[], Optional)
        
        !!! quote "" 
            
            Lọc theo tiên nghi khách sạn

    - filterRoomAmenities `query` (String[], Optional)
        
        !!! quote "" 
            
            Lọc theo tiện nghi phòng

    - filterRoomViews `query` (String[], Optional)
        
        !!! quote "" 
            
            Lọc theo hướng nhìn của phòng

    - filterThemes `query` (String[], Optional)
        
        !!! quote "" 
        
            Lọc theo chủ đề của khách sạn

    - filterMealPlans `query` (String[], Optional)
        
        !!! quote "" 
            
            Lọc theo bữa ăn

    - filterGeoDistanceLat `query` (Double, Optional)
        
        !!! quote "" 
            
            Lọc theo tọa độ lat

    - filterGeoDistanceLon `query` (Double, Optional)   
        
        !!! quote "" 
            
            Lọc theo tọa độ lon

    - filterGeoDistanceMeters `query` (Integer, Optional)
        
        !!! quote "" 
            
            Lọc theo tọa độ và khoảng cách. Đơn vị mét

    - sortField `query` (String, Optional)
        
        !!! quote "" 
            
            Sắp xếp theo: price, starRating, guestRating

    - sortOrder `query` (String, Optional)
        
        !!! quote "" 
        
            Sắp xếp theo thứ tự: ASC, DESC

    - pageNumber `query` (String, Optional)
        
        !!! quote "" 
            
            Trang số

    - pageSize `query` (String, Optional)
        
        !!! quote "" 
            
            Số phần tử trên trang

### Response 
#### Code 200
> OK

=== "Model" 
    ???+ example "Model"
        
        - result (Object, Optional)

            !!! quote ""

                Thông tin kết quả trả về 

            - searchId (String, Optional)
            
                !!! quote "" 

                    - Mã tham chiếu đến kết quả tìm kiếm  

                    - searchId được tạo ra dựa trên các tham số bắt buộc, nếu các tham số không thay đổi thì searchId sẽ không thay đổi  

                    - Được dùng làm tham số khi search-all-rates 

            - propertyAvailable (Array[PropertyAvailable], Optional)
            
                !!! quote "" 

                    Mảng chứa đối tượng thông tin khách sạn 

                - address (Address, optional), 
                
                    !!! quote ""

                        Thông tin địa chỉ khách sạn

                    - city (string, optional),
                        
                        !!! quote "" 
                            
                            Thành phố

                    - countryCode (string, optional),
            
                        !!! quote "" 

                            Mã quốc gia 

                    - countryName (string, optional),
                        
                        !!! quote "" 
                            
                            Tên quốc gia

                    - lineOne (string, optional),
            
                        !!! quote ""

                            Địa chỉ dòng 1

                    - lineTow (string, optional),
                        
                        !!! quote "" 
                            
                            Địa chỉ dòng 2

                    - postalCode (string, optional),
            
                        !!! quote "" 
                            
                            Mã bưu điện 

                    - stateProvinceCode (string, optional),
                        
                        !!! quote "" 
                            
                            Mã tỉnh thành

                    - stateProvinceName (string, optional)
                        
                        !!! quote "" 

                            Tên tỉnh thành 

                - amenities (Array[Amenity], optional),
            
                    !!! quote "" 

                        Thông tin danh sách tện nghi kèm theo của tùy chọn giá

                    - id (string, optional), 
            
                        !!! quote "" 
                            
                            Id của tiện nghi

                    - name (string, optional)
                        
                        !!! quote "" 
                            
                            Tên của tiện nghi 

                    - ~~value (string, optional)~~
                    
                    - ~~group (string, optional)~~
                    
                - basePrice (number, optional),
                    
                    !!! quote "" 
                        
                        Giá cơ bản 

                - basePriceBeforePromo (number, optional),
                    
                    !!! quote "" 
                        
                        Giá cơ bản trước khuyến mãi. Nếu không có khuyến mãi thì giá trị là 0

                - breakfastIncluded (boolean, optional),
                        
                    !!! quote "" 
                    
                        Có bao gồm bữa ăn sáng hay không 

                - cancelFree (boolean, optional),
            
                    !!! quote "" 
                        
                        Cho phép hủy phòng miễn phí hay không 

                - currency (string, optional) = ['VND', 'USD'],
                    
                    !!! quote "" 
                        
                        Tiền tệ 

                - images (Array[HotelImage], optional),
                    
                    !!! quote "" 
                        
                        Thông tin hình ảnh của khách sạn 

                    - caption (string, optional),
            
                        !!! quote "" 
                            
                            Tiêu đề hình ảnh  

                    - link (string, optional),
                            
                        !!! quote "" 

                            Liên kết hình ảnh, là đường dẫn tuyệt đối 

                    - position (integer, optional)
                        
                        !!! quote "" 

                            Vị trí sắp xếp của hình ảnh

                - language (string, optional) = ['vi', 'en'],
            
                    !!! quote "" 
                        
                        Ngôn ngữ

                - latitude (number, optional),
                        
                    !!! quote "" 
                        
                        Vĩ độ 

                - longitude (number, optional),
            
                    !!! quote "" 
                        
                        Kinh độ 

                - promo (boolean, optional),
            
                    !!! quote "" 
                        
                        Có khuyến mãi hay không

                - propertyCategory (PropertyCategory, optional),
                    
                    !!! quote "" 
                        
                        Danh mục khách sạn 

                    - id (string, optional), 
                        
                        !!! quote "" 
                            
                            Id danh mục khách sạn

                    - name (string, optional)
                        
                        !!! quote "" 
                            
                            Tên danh mục khách sạn 

                - propertyId (string, optional),
                        
                    !!! quote "" 
                        
                        Id định danh khách sạn 

                - propertyName (string, optional),
                    
                    !!! quote "" 
                        
                        Tên khách sạn 

                - refundable (boolean, optional),
            
                    !!! quote "" 

                        Có được trả tiền khi hủy phòng hay không 

                - reviewCount (string, optional),
            
                    !!! quote "" 
            
                        Số lượng đánh giá của khách 

                - ~~reviewRecommendPercent (string, optional),~~
                
                - reviewScore (string, optional),
            
                    !!! quote "" 
                        
                        Điểm đánh giá trung bình của khách. Lớn nhất là 5

                - stars (string, optional),
                    
                    !!! quote "" 
                        
                        Hạng sao khách sạn 

                - supplier (string, optional) = ['EXPEDIA', 'AXISROOM', 'BEDLINKER'],
                    
                    !!! quote "" 

                        Nguồn cung cấp khách sạn

                - tags (Array[string], optional),
                    
                    !!! quote "" 
                    
                        Thẻ cuả khách sạn

                - taxAndServiceFree (number, optional),
                    
                    !!! quote "" 
                        
                        Thuế và phí kèm theo 

                - totalPrice (number, optional),
                    
                    !!! quote "" 
                        
                        Tổng giá tiền tạm tính

                - totalRooms (integer, optional),
                    
                    !!! quote "" 
                        
                        Số lượng phòng còn trống có thể book

                - ~~tripAdvisor (TripAdvisor, optional)~~

                - rateOption (String, optional)

                    !!! quote ""

                        Tuỳ chọn giá. Có 2 tuỳ chọn giá là `OTA, TA`. Mặc định là `OTA`.

                - masterPropertyId (Long, optional)

                    !!! quote ""

                        Mã định danh khách sạn chính.
                
            - pageResult (Object, Optional)
                    
                !!! quote "" 

                    Thông tin trang trả về 

                - pageSize (Integer, Optional)
                    
                    !!! quote "" 
                        
                        Kích thước trang 

                - pageNumber (Integer, Optional)
                
                    !!! quote "" 
                        
                        Thứ tự trang 

                - totalPage (Integer, Optional)
                    
                    !!! quote "" 
                        
                        Tổng số trang 

                - totalItems (Integer, Optional)
                        
                    !!! quote "" 
                        
                        Tổng số phần tử

        - duration (Integer, Optional)
        - success (Integer, Bool)
        - infos (Array[InfosDTO], Optional)
        - errors (Array[ErrorsDTO], Optional)
        - textMessage (String, Optional)

=== "Example"
    ```json 
    {
        "result": {
            "searchId": "eyJzZWFyY2hJZCI6IiIsImNoZWNrSW4iOiIyMDIxLTA3LTIzIiwiY2hlY2tPdXQiOiIyMDIxLTA3LTI0IiwicGF4SW5mb3MiOlt7ImFkdWx0UXVhbnRpdHkiOjIsImNoaWxkUXVhbnRpdHkiOjAsImluZmFudFF1YW50aXR5IjowLCJjaGlsZEFnZXMiOltdfV0sImxhbmd1YWdlIjoidmkiLCJjdXJyZW5jeSI6IlZORCIsInN1cHBsaWVyIjoiRVhQRURJQSIsInNlYXJjaENvZGUiOiIxNzgyNjIiLCJzZWFyY2hUeXBlIjoiTVVMVElfQ0lUWV9WSUNJTklUWSJ9",
            "propertyAvailable": [
            {
                "propertyId": "481659",
                "propertyName": "Khách sạn Continental Sài Gòn",
                "stars": "4.0",
                "address": {
                    "lineOne": "132 - 134 Đồng Khởi, Q.1",
                    "lineTow": "",
                    "stateProvinceCode": "",
                    "stateProvinceName": "",
                    "postalCode": "70000",
                    "city": "TP.Hồ Chí Minh",
                    "countryCode": "VN",
                    "countryName": ""
                },
                "latitude": 10.776629,
                "longitude": 106.702459,
                "rateOption": "OTA",
                "masterPropertyId": 1,
                "propertyCategory": {
                    "id": "1",
                    "name": "Khách sạn"
                },
                "images": [
                    {
                        "caption": "Ảnh nổi bật",
                        "position": 1,
                        "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/cbe48cdd_z.jpg"
                    },
                    {
                        "caption": "Tiền sảnh",
                        "position": 2,
                        "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/580dff7d_z.jpg"
                    },
                    {
                        "caption": "Phòng",
                        "position": 3,
                        "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/394e4ca3_z.jpg"
                    },
                    {
                        "caption": "Phòng",
                        "position": 4,
                        "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/b6e21a19_z.jpg"
                    },
                    {
                        "caption": "Phòng",
                        "position": 5,
                        "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/03f49af2_z.jpg"
                    }
                ],
                "amenities": [
                    {
                        "id": "2205",
                        "name": "Bữa sáng buffet",
                        "value": "",
                        "group": ""
                    },
                    {
                        "id": "1073742786",
                        "name": "Bữa sáng miễn phí",
                        "value": "",
                        "group": ""
                    },
                    {
                        "id": "2109",
                        "name": "Đậu xe miễn phí",
                        "value": "",
                        "group": ""
                    },
                    {
                        "id": "2192",
                        "name": "Wifi miễn phí",
                        "value": "",
                        "group": ""
                    }
                ],
                "supplier": "EXPEDIA",
                "language": "vi",
                "currency": "VND",
                "breakfastIncluded": true,
                "cancelFree": true,
                "totalPrice": 1205450.0,
                "basePrice": 1043680.0,
                "taxAndServiceFree": 161770.0,
                "basePriceBeforePromo": 1490972.0,
                "reviewCount": "995",
                "reviewScore": "4.133333333333333",
                "reviewRecommendPercent": "80.2",
                "tripAdvisor": {
                    "rating": "",
                    "count": "",
                    "image": ""
                },
                "totalRooms": 5,
                "tags": [],
                "promo": true,
                "refundable": true
            },
            ...
            ],
            "pageResult": {
                "pageSize": 15,
                "pageNumber": 0,
                "totalPage": 70,
                "totalItems": 1045
            }
        },
        "duration": 0,
        "textMessage": null,
        "errors": null,
        "infos": null,
        "success": true
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

## 3. API Tùy chọn bộ lọc 

!!! info "GET: /api/v3/hotel/filter-options"
    Lấy danh sách các giá trị có thể áp dụng trên bộ lọc trên kết quả tìm kiếm. Có thể áp dụng cùng lúc nhiều bộ lọc với nhau.

### Parameters
???+ example "Parameters"
    - language `query` (String, Required)

        !!! quote "" 
        
            Ngôn ngữ 

            - `vi` : Tiếng Việt 
            
            - `en`: Tiếng Anh 

### Response
#### Code 200
=== "Model" 
    ???+ example "Model"
        - result (FilterOptionsResult, optional)

            !!! quote ""
        
                Thông tin kết quả trả về 
        
            - guestRatings (Array[FilterItemDouble], optional),
            
                !!! quote "" 
                    
                    Thông tin đánh giá khách sạn của khách. Cao nhất là 5

                - name (string, optional),
            
                    !!! quote "" 

                        Tên bộ lọc đánh giá của khách 

                - value (number, optional)
                    
                    !!! quote "" 
                        
                        Giá trị bộ lọc đánh gía của khách 

            - language (string, optional) = ['vi', 'en'],
                
                !!! quote "" 
                    
                    Ngôn ngữ trả về 

            - mealPlans (Array[FilterItemString], optional),
                
                !!! quote "" 
    
                    Thông tin tùy chọn bộ lọc theo bữa ăn

                - name (string, optional),
                    
                    !!! quote "" 
                        
                        Mô tả bữa ăn 

                - value (string, optional)
                    
                    !!! quote "" 
                        
                        Id của bộ lọc bữa ăn  

            - prices (Array[FilterPrice], optional),
                
                !!! quote "" 
    
                    Thông tin tùy chọn theo bộ lọc giá 

                - operator (string, optional), 
                    
                    !!! quote "" 
                        
                        Phương thức so sánh  

                    - `less_than`: Giá nhỏ hơn

                    - `range`: Giá trong khoảng

                    - `greater_than`: Giá lớn hơn
                    
                - from (number, optional),
                    
                    !!! quote "" 
                        
                        Giá từ 

                - to (number, optional)
                    
                    !!! quote "" 
                        
                        Giá đến

            - propertyAmenities (Array[FilterItemString], optional),
                    
                !!! quote "" 
                        
                    Thông tin bộ lọc theo tiện nghi khách sạn 

                - name (string, optional),
                    
                    !!! quote "" 
                        
                        Mô tả tiện nghi 

                - value (string, optional)
                    
                    !!! quote "" 
                        
                        Id của bộ lọc tiện nghi 

            - propertyCategories (Array[FilterItemString], optional),
                    
                !!! quote "" 
                        
                    Thông tin bộ lọc theo danh mục khách sạn 

                - name (string, optional),
                    
                    !!! quote "" 
                        
                        Mô tả danh mục khách sạn 

                - value (string, optional)
                    
                    !!! quote "" 
                        
                        Id của bộ lọc theo danh mục khách sạn 

            - propertyRatings (Array[FilterItemDouble], optional),
                    
                !!! quote "" 
                        
                    Thông tin bộ lọc theo hạng sao 

                - name (string, optional),
                    
                    !!! quote "" 
                        
                        Mô tả hạng sao 

                - value (number, optional)
            
                    !!! quote "" 

                        Giá trị hạng sao 

            - roomAmenities (Array[FilterItemString], optional),
                    
                !!! quote "" 
                        
                    Thông tin bộ lọc theo tiện nghi trong phòng 

                - name (string, optional),
                    
                    !!! quote "" 
                        
                        Mô tả tiện nghi trong phòng 

                - value (string, optional)
            
                    !!! quote "" 

                        Id của bộ lọc theo tiện nghi trong phòng 

            - roomViews (Array[FilterItemString], optional),
                    
                !!! quote "" 
                        
                    Thông tin bộ lọc theo hướng nhìn phòng 

                - name (string, optional),
                    
                    !!! quote "" 
                        
                        Mô tả hướng nhìn phòng 

                - value (string, optional)
            
                    !!! quote "" 

                        Id của bộ lọc theo hướng nhìn phòng 

            - themes (Array[FilterItemString], optional)
            
                !!! quote "" 

                    Thông tin bộ lọc theo chủ đề của khách sạn 

                - name (string, optional),
                    
                    !!! quote "" 
                        
                        Mô tả chủ đề của khách sạn 

                - value (string, optional)
            
                    !!! quote "" 

                        Id của bộ lọc theo chủ đề 

        - duration (integer, optional),
        - errors (Array[Error], optional),
        - infos (Array[Info], optional),
        - success (boolean, optional),
        - textMessage (string, optional)
=== "Example"
    ```json 
    {
        "result": {
            "language": "vi",
            "prices": [
            {
                "from": 0.0,
                "to": 500.0,
                "operator": "less_than"
            },
            {
                "from": 500.0,
                "to": 1500000.0,
                "operator": "range"
            },
            {
                "from": 1500000.0,
                "to": 3000000.0,
                "operator": "range"
            },
            {
                "from": 3000000.0,
                "to": 5000000.0,
                "operator": "range"
            },
            {
                "from": 5000000.0,
                "to": 0.0,
                "operator": "greater_than"
            }
            ],
            "guestRatings": [
            {
                "name": "Tuyệt vời 4,5+",
                "value": 4.5
            },
            {
                "name": "Rất tốt 4+",
                "value": 4.0
            },
            {
                "name": "Tốt 3,5+",
                "value": 3.5
            }
            ],
            "propertyRatings": [
            {
                "name": "1 Sao",
                "value": 1.0
            },
            {
                "name": "2 Sao",
                "value": 2.0
            },
            {
                "name": "3 Sao",
                "value": 3.0
            },
            {
                "name": "4 Sao",
                "value": 4.0
            },
            {
                "name": "5 Sao",
                "value": 5.0
            }
            ],
            "propertyAmenities": [
            {
                "name": "Nhà hàng",
                "value": "5fd08875bf27565360ba5f7b"
            },
            {
                "name": "Hồ bơi",
                "value": "5fd08875bf27565360ba5f7d"
            },
            {
                "name": "Lò nướng BBQ",
                "value": "5fd08875bf27565360ba5f7e"
            },
            {
                "name": "Quán cafe",
                "value": "5fd08875bf27565360ba5f7c"
            },
            {
                "name": "Xe đạp",
                "value": "5fd08874bf27565360ba5f6c"
            },
            {
                "name": "Câu lạc bộ đêm",
                "value": "5fd08874bf27565360ba5f6d"
            },
            {
                "name": "Khu dã ngoại",
                "value": "5fd08874bf27565360ba5f6e"
            },
            {
                "name": "Phòng tập thể dục",
                "value": "5fd08875bf27565360ba5f6f"
            },
            {
                "name": "Phòng họp",
                "value": "5fd08875bf27565360ba5f70"
            },
            {
                "name": "Nhận/trả phòng nhanh",
                "value": "5fd08875bf27565360ba5f71"
            },
            {
                "name": "Spa & chăm sóc sức khỏe",
                "value": "5fd08875bf27565360ba5f72"
            },
            {
                "name": "Wifi miễn phí",
                "value": "5fd08875bf27565360ba5f73"
            },
            {
                "name": "Câu lạc bộ trẻ em",
                "value": "5fd08875bf27565360ba5f74"
            },
            {
                "name": "Khách sạn không khói thuốc",
                "value": "5fd08875bf27565360ba5f75"
            },
            {
                "name": "Đưa đón sân bay",
                "value": "5fd08875bf27565360ba5f76"
            },
            {
                "name": "Trông coi trẻ",
                "value": "5fd08875bf27565360ba5f77"
            },
            {
                "name": "Bãi đậu xe",
                "value": "5fd08875bf27565360ba5f78"
            },
            {
                "name": "Lễ tân phục vụ 24/24",
                "value": "5fd08875bf27565360ba5f79"
            },
            {
                "name": "Quầy bar / Phòng chờ",
                "value": "5fd08875bf27565360ba5f7a"
            }
            ],
            "propertyCategories": [
            {
                "name": "Nhà trên cây",
                "value": "5fd088e056eb614a490cb1fb"
            },
            {
                "name": "Lều",
                "value": "5fd088e056eb614a490cb1fc"
            },
            {
                "name": "Giường & bữa sáng (B&B)",
                "value": "5fd088e056eb614a490cb1fd"
            },
            {
                "name": "Khách sạn khoang ngủ (capsule)",
                "value": "5fd088e056eb614a490cb1fe"
            },
            {
                "name": "Khu nghỉ dưỡng",
                "value": "5fd088e056eb614a490cb1ff"
            },
            {
                "name": "Motels",
                "value": "5fd088e056eb614a490cb200"
            },
            {
                "name": "Khách sạn Căn hộ",
                "value": "5fd088e056eb614a490cb201"
            },
            {
                "name": "Dinh thự",
                "value": "5fd088e056eb614a490cb202"
            },
            {
                "name": "Biệt thự",
                "value": "5fd088e056eb614a490cb203"
            },
            {
                "name": "Khu cắm trại",
                "value": "5fd088e056eb614a490cb204"
            },
            {
                "name": "Homestays",
                "value": "5fd088e056eb614a490cb205"
            },
            {
                "name": "Nhà khách",
                "value": "5fd088e056eb614a490cb206"
            },
            {
                "name": "Nhà trọ",
                "value": "5fd088e056eb614a490cb207"
            },
            {
                "name": "Khách sạn",
                "value": "5fd088e056eb614a490cb208"
            }
            ],
            "roomAmenities": [
            {
                "name": "Phòng cách âm",
                "value": "5fd08897c68e297f0b6632c0"
            },
            {
                "name": "Máy pha cà phê / trà",
                "value": "5fd08897c68e297f0b6632c1"
            },
            {
                "name": "Dịch vụ phòng 24/24",
                "value": "5fd08897c68e297f0b6632c2"
            },
            {
                "name": "Nhà bếp / Bếp nhỏ",
                "value": "5fd08897c68e297f0b6632c3"
            },
            {
                "name": "Tivi màn hình phẳng",
                "value": "5fd08897c68e297f0b6632c4"
            },
            {
                "name": "Ấm đun nước điện",
                "value": "5fd08897c68e297f0b6632c5"
            },
            {
                "name": "Máy sấy tóc",
                "value": "5fd08897c68e297f0b6632c6"
            },
            {
                "name": "Tắm hơi",
                "value": "5fd08897c68e297f0b6632c7"
            },
            {
                "name": "Bồn tắm",
                "value": "5fd08897c68e297f0b6632c8"
            },
            {
                "name": "Điều hòa không khí",
                "value": "5fd08897c68e297f0b6632c9"
            },
            {
                "name": "Máy giặt",
                "value": "5fd08897c68e297f0b6632ca"
            }
            ],
            "roomViews": [
            {
                "name": "Quang cảnh sông",
                "value": "5fd088bbca43d86432e3d098"
            },
            {
                "name": "Quang cảnh hồ bơi",
                "value": "5fd088bbca43d86432e3d099"
            },
            {
                "name": "Quang cảnh núi",
                "value": "5fd088bbca43d86432e3d09a"
            },
            {
                "name": "Hướng ra vườn",
                "value": "5fd088bbca43d86432e3d09b"
            },
            {
                "name": "Quang cảnh hồ",
                "value": "5fd088bbca43d86432e3d09c"
            },
            {
                "name": "Quang cảnh Landmark",
                "value": "5fd088bbca43d86432e3d095"
            },
            {
                "name": "Quang cảnh thành phố",
                "value": "5fd088bbca43d86432e3d096"
            },
            {
                "name": "Quang cảnh biển",
                "value": "5fd088bbca43d86432e3d097"
            }
            ],
            "themes": [
            {
                "name": "Boutique",
                "value": "5fd089045f77a544feda9e23"
            },
            {
                "name": "Sang trọng",
                "value": "5fd089045f77a544feda9e24"
            },
            {
                "name": "Mua sắm",
                "value": "5fd089045f77a544feda9e25"
            },
            {
                "name": "Phù hợp cho gia đình",
                "value": "5fd089055f77a544feda9e26"
            },
            {
                "name": "Phù hợp cho thú cưng",
                "value": "5fd089055f77a544feda9e27"
            },
            {
                "name": "Lãng mạn",
                "value": "5fd089055f77a544feda9e28"
            },
            {
                "name": "Spa & Sức khỏe",
                "value": "5fd089045f77a544feda9e1e"
            },
            {
                "name": "Biển",
                "value": "5fd089045f77a544feda9e1f"
            },
            {
                "name": "Lịch sử",
                "value": "5fd089045f77a544feda9e20"
            },
            {
                "name": "Công việc",
                "value": "5fd089045f77a544feda9e21"
            },
            {
                "name": "Phiêu lưu",
                "value": "5fd089045f77a544feda9e22"
            }
            ],
            "mealPlans": [
            {
                "name": "Bữa sáng",
                "value": "5fd0892dcc812e12c8689c86"
            },
            {
                "name": "Bữa trưa",
                "value": "5fd0892dcc812e12c8689c87"
            },
            {
                "name": "Bữa tối",
                "value": "5fd0892dcc812e12c8689c88"
            }
            ]
        },
        "duration": 0,
        "textMessage": null,
        "errors": null,
        "infos": null,
        "success": true
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

## 4. API Tìm kiếm khách sạn với tất cả tùy chọn giá (search-all-rates)

!!! info "GET: /api/v3/hotel/search-all-rates"
    Kết quả trả về thông tin chi tiết của một khách sạn, thông tin phòng và thông tin của tất cả tùy chọn giá. 

    Mỗi một khách sạn có thể có 1 hoặc nhiều phòng, mỗi phòng sẽ có một hoặc nhiều tùy chọn giá khác nhau tùy theo bữa ăn và dịch vụ kèm theo.


### Parameters
???+ examble "Parameters"

    - searchId `query` (string, required)
        
        !!! quote "" 

            Mã tìm kiếm, được lấy từ mục search-all-rate

    - propertyId `query` (string, required)
        
        !!! quote "" 

            Mã định danh khách sạn theo supplier. Được lấy từ kết quả trả về của search-best-rate 

    - supplier `query` (String, required)
        
        !!! quote "" 

            Nhà cung cấp. Được lấy từ kết quả trả về của search-best-rate

    - checkIn `query` (String, required)
        
        !!! quote "" 
            
            Ngày nhận phòng.  
        
            Định dạng: `yyyy-MM-dd`

    - checkOut `query` (String, required)
        
        !!! quote "" 
            
            Ngày trả phòng.  
        
            Định dạng: `yyyy-MM-dd`

    - paxInfos `query` (String[], required)
        
        !!! quote "" 
            
            Thông tin phòng và khách ở   
        
            Định dạng: `SoNguoiLon-TuoiTreEm1,TuoiTreEm2`
        
            Ví dụ:  
        
            - 2 người lớn và 2 trẻ em, 1 trẻ 4 tuổi, 1 trẻ 6 tuổi: `...&paxInfos=2-4,6&...  

            - 2 phòng, phòng 1 gồm 2 người lớn, phòng 2 gồm 2 người lớn và 2 trẻ em, 1 trẻ em 4 tuổi và 1 trẻ em 6 tuổi: `...&paxInfos=2&paxInfos=2-4,6&...

### Response 
#### Code 200
> OK

=== "Model"

    ???+ example "Model"
        - result (SearchAllRatesResult, optional),

            - tripId (string, optional),
                    
                !!! quote "" 
                        
                    Mã định danh kết quả search-all-rate, mỗi lần gọi search-all-rate sẽ tạo ra tripId mới, nó được sử dụng khi đi thao tác đặt phòng 

            - searchId (string, optional),
                    
                !!! quote "" 
                        
                    Mã tham chiếu đến search-best-rate, được lấy từ kết quả search-best-rate

            - propertyAllRate (PropertyAllRate, optional)
            
                !!! quote "" 

                    Thông tin trả về chi tiết của một khách sạn, thông tin phòng và thông tin của tất cả tùy chọn giá  
        
                - address (Address, optional)
                
                    !!! quote "" 
                        
                        Thông tin địa chỉ khách sạn

                    - city (string, optional),
                    
                    !!! quote "" 
                        
                        Thành phố

                    - countryCode (string, optional),
                    
                        !!! quote "" 
                        
                            Mã quốc gia

                    - countryName (string, optional),
                    
                        !!! quote "" 
                        
                            Tên quốc gia

                    - lineOne (string, optional),
                    
                        !!! quote "" 
                        
                            Địa chỉ dòng 1

                    - lineTow (string, optional),
                    
                        !!! quote "" 
                        
                            Địa chỉ dòng 2

                    - postalCode (string, optional),
                    
                        !!! quote "" 
                        
                            Mã bưu điện

                    - stateProvinceCode (string, optional),
                    
                        !!! quote "" 
                        
                            Mã tỉnh thành

                    - stateProvinceName (string, optional)
            
                        !!! quote "" 

                            Tên tỉnh thành

                - airportCode (string, optional),
                    
                    !!! quote "" 
                        
                        Mã sân bay 

                - amenities (Array[Amenity], optional),
                    
                    !!! quote "" 
                        
                        Mảng đối tượng chứa thông tin tiện nghi của khách sạn 

                    - id (string, optional),
                    
                    !!! quote "" 
                        
                        Mã tiện nghi khách sạn 

                    - name (string, optional),
                    
                        !!! quote "" 
                        
                            Tên của tiện nghi khách sạn

                    - ~~value (string, optional)~~
                    
                    - group (string, optional)
                        
                        !!! quote ""
                            
                            Thông tin tiện nghi của khách sạn được gom nhóm, với các nhóm sau 
                            
                            - `OTHER`: Tiện nghi khác

                            - `POPULAR_FACILITIES`: Tiện nghi phổ biến  

                            - `SERVICE`: Dịch vụ  

                            - `BUSINESS_SERVICE`: Dịch vụ doanh nghiệp  

                            - `RECREATION`: Cơ sở giải trí  

                            - `ENTERTAINMENT`: Giải trí đa phương tiện   

                            - `FITNESS_AND_SPA`: fitness và spa  

                            - `FOOD_AND_DRINK`: Khu vực ăn uống  

                            - `CONVENIENCES`: Tiện ích  

                            - `INTERNET`: Mạng intenet  

                            - `PARKING_AND_TRANSPORT`: Khu vực để xe và đưa đón  

                            - `PET`: Thú cưng  

                - ~~attributes (Array[Attribute], optional),~~
                
                - checkin (Checkin, optional),
                    
                    !!! quote "" 
                        
                        Khoảng thời gian nhận phòng, theo giờ địa phương của khách sạn 

                    - beginTime (string, optional),
                    
                        !!! quote "" 
                        
                            Thời gian bắt đầu được nhận phòng. Mặc định: 14:00

                    - endTime (string, optional)
                        
                        !!! quote "" 
    
                            Thời gian kết thúc được nhận phòng. Mặc định: 24:00 

                - checkout (Checkout, optional),

                    !!! quote "" 
                            
                        Thông tin thời gian trả phòng. Mặc định trước 12:00

                    - endTime (string, optional)

                        !!! quote "" 
                            
                            Thời gian trả phòng tối đa. Mặc định trước 12:00

                - currency (string, optional) = ['VND', 'USD'],
                    
                    !!! quote "" 
                        
                        Thông tin tiền tệ trả về 

                - descriptions (Array[Attribute], optional),
                    
                    !!! quote "" 
                        
                        Thông tin mô tả về khách sạn 

                    - id (string, optional),
                    
                        !!! quote "" 
                        
                            Mã định danh thuộc tính mô tả 

                    - name (string, optional),
                    
                        !!! quote "" 
                        
                            Tên thuộc tính 

                            - `description`: mô tả chung  
                        
                            - `amenities`: mô tả chung về tiện nghi của khách sạn  
                            
                            - `dining`: Mô tả về chỗ ăn uống của khách sạn  
                            
                            - `renovations`: Mô tả về quá trình cải tạo phòng hoặc khách sạn mới đây  
                            
                            - `national_ratings`: Nêu rõ nguồn xếp hạng sao của khách sạn  
                            
                            - `business_amenities`: Mô tả về tiện nghi dành cho doanh nghiệp tại chỗ nghỉ, Ví dụ: phòng hội nghị  
                            
                            - `rooms`: Mô tả về phòng  
                            
                            - `attractions`: Mô tả về điểm tham quan gần khách sạn  
                            
                            - `location`: Mô tả về vị trí của khách sạn  
                            
                            - `headline`: Mô tả tóm tắt  
                        
                    - value (string, optional)
                        
                        !!! quote "" 
                            
                            Thông tin mô tả

                - fees (Array[Attribute], optional),
                    
                    !!! quote "" 
                        
                        Thông tin mô tả về một số khoản phụ phí kèm theo 

                    - id (string, optional),
                    
                        !!! quote "" 
                        
                            Mã định danh thuộc tính phí 

                    - name (string, optional),
                    
                        !!! quote "" 
                        
                            Tên thuộc tính phí  
                        
                            - `mandatory`: Phí bắt buộc  
                        
                            - `optional`: Phí không bắt buộc  
                        
                    - value (string, optional)
                
                        !!! quote "" 
                            
                            Mô tả về khoản phí 

                - images (Array[HotelImage], optional),
                    
                    !!! quote "" 
                        
                        Hình ảnh của khách sạn

                    - caption (string, optional),
                    
                        !!! quote "" 
                        
                            Tiêu đề của hình ảnh 

                    - link (string, optional),
                    
                        !!! quote "" 
                        
                            Liên kết tới hình ảnh. Liên kết tuyệt đối 

                    - position (integer, optional)
            
                        !!! quote "" 

                            Vị trí sắp xếp hình ảnh 

                - inclusions (Array[Attribute], optional),
                    
                    !!! quote "" 
                        
                        Mảng đối tượng chứa thông tin mô tả về thuộc tính của khách sạn 

                    - id (string, optional),
                    
                        !!! quote "" 
                        
                            Mã định danh thuộc tính

                    - name (string, optional),
                    
                        !!! quote "" 
                        
                            Mô tả thuộc tính 

                    - ~~value (string, optional)~~
                    
                - language (string, optional) = ['vi', 'en'],
                    
                    !!! quote "" 
                        
                        Ngôn ngữ trả về 

                - latitude (number, optional),
                    
                    !!! quote "" 
                        
                        Vĩ độ của khách sạn 

                - longitude (number, optional),
                    
                    !!! quote "" 
                        
                        Kinh độ của khách sạn 

                - policies (Array[Attribute], optional),
                    
                    !!! quote "" 
                        
                        Thông tin về chính sách khách sạn mà khách cần lưu ý.

                    - id (string, optional),
                    
                        !!! quote "" 
                        
                            Mã định danh chính sách 

                    - name (string, optional),
                    
                        !!! quote "" 
                        
                            Tên thuộc chính sách  
                        
                            - `know_before_you_go`: Mô tả thông tin có thể hữu ích khi lập kế hoạch cho chuyến đi đến nơi này
                        
                    - value (string, optional)
                        
                        !!! quote "" 
                            
                            Mô tả về chính sách

                - propertyCategory (PropertyCategory, optional),
                    
                    !!! quote "" 
                        
                        Danh mục của khách sạn

                    - id (string, optional),
                    
                        !!! quote "" 
                        
                            Mã định danh danh mục khách sạn 

                    - name (string, optional)
            
                        !!! quote "" 

                            Tên danh mục khách sạn 

                - propertyId (string, optional),
                    
                    !!! quote "" 
                        
                        Mã định danh khách sạn 

                - propertyName (string, optional),
                    
                    !!! quote "" 
                        
                        Tên khách sạn 

                - ~~rank (integer, optional),~~
                
                - rating (Rating, optional),
                    
                    !!! quote "" 
                        
                        Đánh giá về khách sạn 

                    - ratingGuest (RatingGuest, optional)
            
                        !!! quote "" 

                            Đánh giá của khách 

                        - amenities (string, optional),
                    
                            !!! quote "" 
                        
                                Xếp hạng cho các tiện nghi do khách sạn cung cấp, được tính trung bình từ tất cả các đánh giá của khách. Trả về giá trị từ 1,0 đến 5,0.

                        - cleanliness (string, optional),
                    
                            !!! quote "" 
                        
                                Đánh giá mức độ sạch sẽ cho khách sạn, được tính trung bình từ tất cả các đánh giá của khách. Trả về giá trị từ 1,0 đến 5,0.

                        - comfort (string, optional),
                    
                            !!! quote "" 
                        
                                Đánh giá mức độ thoải mái của các phòng, được tính trung bình từ tất cả các đánh giá của khách. Trả về giá trị từ 1,0 đến 5,0.

                        - condition (string, optional),
                    
                            !!! quote "" 
                        
                                Xếp hạng cho tình trạng của chỗ nghỉ, được tính trung bình từ tất cả các đánh giá của khách. Trả về giá trị từ 1,0 đến 5,0.

                        - count (integer, optional),
                    
                            !!! quote "" 
                        
                                Tất cả xếp hạng đánh giá của khách giành cho khách sạn 

                        - location (string, optional),
                    
                            !!! quote "" 
                        
                                Xếp hạng về mức độ hấp dẫn của vị trí của khách sạn, được tính trung bình từ tất cả các đánh giá của khách. Trả về giá trị từ 1,0 đến 5,0.

                        - neighborhood (string, optional),
                    
                            !!! quote "" 
                        
                                Xếp hạng về mức độ hài lòng của khu vực lân cận của khách sạn, được tính trung bình từ tất cả các đánh giá của khách. Trả về giá trị từ 1,0 đến 5,0.

                        - overall (string, optional),
                    
                            !!! quote "" 
                        
                                Đánh giá chung cho khách sạn, được tính trung bình từ tất cả các đánh giá của khách. Trả về giá trị từ 1,0 đến 5,0.

                        - quality (string, optional),
                    
                            !!! quote "" 
                        
                                Xếp hạng chất lượng của các phòng, được tính trung bình từ tất cả các đánh giá của khách. Trả về giá trị từ 1,0 đến 5,0.

                        - recommendationPercent (string, optional),
                    
                            !!! quote "" 
                        
                                Phần trăm khách giới thiệu ở tại chỗ nghỉ này.

                        - ~~score (string, optional),~~
                        
                        - service (string, optional),
                    
                            !!! quote "" 
                        
                                Đánh giá về dịch vụ của nhân viên đối với chỗ nghỉ, được tính trung bình từ tất cả các đánh giá của khách. Trả về giá trị từ 1,0 đến 5,0.

                        - value (string, optional)
            
                            !!! quote "" 

                                Xếp hạng cho giá trị của bất động sản cung cấp cho chi phí lưu trú, được tính trung bình từ tất cả các đánh giá của khách. Trả về giá trị từ 1,0 đến 5,0.

                    - ratingProperty (RatingProperty, optional)
            
                        !!! quote "" 

                            Đánh giá hạng sao khách sạn

                        - rating (string, optional),
                    
                            !!! quote "" 
                        
                                Giá trị sếp hạng. Trả về giá trị từ 0,0 đến 5,0. Giá trị 0,0 hoặc giá trị trống cho biết không có xếp hạng nào.

                        - type (string, optional)

                            !!! quote ""
                        
                                Loại đánh giá 
                            
                                - `Star`: Xếp hạng sao của khách sạn

                - rooms (Array[PropertyRoom], optional),
                    
                    !!! quote "" 
                        
                        Mảng đối tượng chứa thông tin phòng

                    - descriptions (Array[Attribute], optional),
                    
                        !!! quote "" 
                        
                            Thông tin mô tả 

                        - id (string, optional),
                    
                            !!! quote "" 
                        
                                Mã định danh 

                        - name (string, optional),
                    
                            !!! quote "" 
                        
                                Tên mô tả  

                                - `overview`: Thông tin mô tả tổng quan về căn phòng 

                        - value (string, optional)
            
                            !!! quote "" 

                                Thông tin mô tả 

                    - id (string, optional),
                    
                        !!! quote "" 
                        
                            Mã định danh cho loại phòng 

                    - images (Array[RoomImage], optional),
                    
                        !!! quote "" 
                        
                            Mảng đối tượng chứa thông tin hình ảnh của loại phòng 

                        - caption (string, optional),
                    
                            !!! quote "" 
                        
                                Tiêu đề của hình ảnh 

                        - link (string, optional),
                    
                            !!! quote "" 
                        
                                Liên kết tới hình ảnh, là liên kết tuyệt đối 

                        - position (integer, optional)
                            
                            !!! quote "" 

                                Vị trí sắp xếp của hình ảnh 

                    - name (string, optional),
                    
                        !!! quote "" 
                        
                            Tên của loại phòng 

                    - ratePlans (Array[RatePlan], optional),
                    
                        !!! quote "" 
                        
                            Mảng đối tượng chứa thông tin về tùy chọn giá

                        - amenities (Array[Amenity], optional),
                    
                            !!! quote "" 
                        
                                Mảng đối tượng chứa thông tin tiện nghi của tùy chọn giá

                            - id (string, optional),
                    
                                !!! quote "" 
                        
                                    Mã định danh tiện nghi 

                            - name (string, optional),
                    
                                !!! quote "" 
                        
                                    Tên tiện nghi

                            - ~~value (string, optional)~~
                            
                            - ~~group (sting, optional)~~
                            
                        - basePrice (number, optional),
                    
                            !!! quote "" 
                        
                                Giá cơ bản 

                        - basePriceBeforePromo (number, optional),
                    
                            !!! quote "" 
                        
                                Giá cơ bản trước khuyến mãi

                        - bedGroups (Array[BedGroup], optional),
                    
                            !!! quote "" 
                        
                                Mảng đối tượng nhóm giường trong phòng

                            - configurations (Array[ConfigurationBedGroup], optional),
                    
                                !!! quote "" 
                        
                                    Thông tin cấu hình giường cho phòng

                                - quantity (integer, optional),
                    
                                    !!! quote "" 
                        
                                        Số lượng giường

                                - size (string, optional),
                    
                                    !!! quote "" 
                        
                                        Kích thước của giường 

                                - type (string, optional)
                                    
                                    !!! quote "" 
                                        
                                        Loại giường 

                            - description (string, optional),
                    
                                !!! quote "" 
                        
                                    Mô tả hiển thị giường cho phòng này

                            - id (string, optional)
            
                                !!! quote "" 
                                    
                                    Mã định danh nhóm giường 

                        - breakfastIncluded (boolean, optional),
                    
                            !!! quote "" 
                        
                                Tùy chọn giá có bao gồm bữa sáng hay không

                        - cancelFree (boolean, optional),
                    
                            !!! quote "" 
                        
                                Mô tả thông tin được phép hủy đặt phòng với tùy chọn giá này có tốn phí phạt hay không

                                - `true`: Hủy đặt phòng miễn phí 
                            
                                - `false`: Không đặt hủy đặt phòng miễn phí 
                            
                        - cancelFreeBeforeDate (string, optional),
                            
                            !!! quote "" 
                            
                                Ngày giới hạn cho phép hủy đặt phòng với tùy chọn giá này một cách miễn phí  

                        - cancelPenalties (Array[CancelPenalty], optional),

                            !!! quote "" 
                                
                                Mô tả các hình thức phạt khi hủy đặt phòng với tùy chọn giá này. [Xem mô tả thêm ở đây](/dev-guide/api-hotel/api-cancellation/#cac-hinh-thuc-phat)

                            - type (string, optional)
            
                                !!! quote "" 
                                    
                                    Loại hình phạt 

                                    - `NIGHTS`: Số đêm bị phạt 
                            
                                    - `AMOUNT`: Số tiền bị phạt 
                            
                                    - `PERCENT`: Số phần trăm bị phạt 
                                
                            - currency (string, optional) = ['VND', 'USD'],
                    
                                !!! quote "" 
                        
                                    Đơn vị tiền tệ đối với `type = AMOUNT` 

                            - amount (string, optional),
                    
                                !!! quote "" 
                        
                                    Số tiền của hình phạt  

                            - description (string, optional),
                    
                                !!! quote "" 
                        
                                    Mô tả về hình phạt 

                            - nights (string, optional),
                    
                                !!! quote "" 
                        
                                    Số đêm bị tính phí phạt 

                            - percent (string, optional),
                    
                                !!! quote "" 
                        
                                    Số phần trăm bị phạt  

                            - startDate (string, optional),
                    
                                !!! quote "" 
                        
                                    Ngày bắt đầu có hiệu lực của hình phạt 

                            - endDate (string, optional),
                    
                                !!! quote "" 
                        
                                    Ngày kết thúc của hình phạt

                        - fees (Map<String, Double>, optional),
                    
                            !!! quote "" 
                        
                                Thông tin các loại phí được phu bởi khách sạn Giá trị mối loại phí là tổng của loại đó. Phạm vi ảnh hưởng của mô tả này chỉ là thông tin thông báo cho khách hàng biết.

                                - `mandatory_fee`: Một khoản phí bắt buộc do khách sạn thu khi nhận phòng hoặc trả phòng.
                            
                                - `resort_fee`: Một khoản phí cho các tiện nghi và dịch vụ bổ sung và được khách sạn thu khi nhận phòng hoặc trả phòng.
                            
                                - `mandatory_tax`: Khoản thuế bắt buộc do chỗ nghỉ thu khi nhận phòng hoặc trả phòng.
                            
                        - paxPrice (Array[PaxPrice], optional),
                    
                            !!! quote "" 
                        
                                Mảng đối tượng chứa thông tin giá theo số lượng người ở trong một phòng

                            - nightPrices (Array[NightPrice], optional),
                    
                                !!! quote "" 
                        
                                    Mảng đối tượng chứa thông tin giá theo từng đêm 

                                - nightKey (string, optional),
                    
                                    !!! quote "" 
                        
                                        Khóa định danh của từng đêm

                                - nightPriceDetails (Array[NightPriceDetail], optional)
                                    
                                    !!! quote "" 

                                        Mảng đối tượng chứ thông tin giá chi tiết theo từng đêm 

                                    - name (string, optional),
                    
                                        !!! quote "" 
                        
                                            Tên loại giá 

                                            - `base_rate`: Giá cơ bản không bao gồm thuế phí 
                                        
                                            - `tax_and_service_fee`: Thuế và phí 
                                        
                                    - value (number, optional),
                    
                                        !!! quote "" 
                        
                                            Số tiền 

                                    - ~~valueByHotelCurrency (string, optional)~~
                                    
                            - paxInfo (PaxInfo, optional)
            
                                !!! quote "" 

                                    Mô tả thông tin người ở  

                                - adultQuantity (integer, optional),
                    
                                    !!! quote "" 
                        
                                        Số lượng người lớn 

                                - childAges (Array[integer], optional),
                    
                                    !!! quote "" 
                        
                                        Mảng chứa thông tin tuổi của trẻ em, số lượng phần từ mảng bằng với số lượng trẻ em

                                - childQuantity (integer, optional),
                    
                                    !!! quote "" 
                        
                                        Số lượng trẻ em 

                                - ~~infantQuantity (integer, optional)~~
                                
                        - promo (boolean, optional),
                    
                            !!! quote "" 
                        
                                Thông tin xác định có khuyến mãi hay không 

                                - `true`: Có khuyến mãi 
                            
                                - `false`: Không có khuyến mãi
                            
                        - promoDescription (string, optional),
                    
                            !!! quote "" 
                        
                                Mô tả thông tin khuyến mãi 

                        - ratePlanId (string, optional),
                    
                            !!! quote "" 
                        
                                Mã định danh tùy chọn giá 

                        - ratePlanName (string, optional),
                    
                            !!! quote "" 
                        
                                Tên của tùy chọn giá 

                        - refundable (boolean, optional),
                    
                            !!! quote "" 
                        
                                Thông tin xác định khi hủy phòng có được hoàn tiền hay không 

                                - `true`: Được hoàn tiền khi hủy 
                            
                                - `false`: Không được hoàn tiền khi hủy 
                            
                        - taxAndFees (number, optional),
                    
                            !!! quote "" 
                        
                                Thuế và phí của tùy chọn giá 

                        - totalPrice (number, optional),
                    
                            !!! quote "" 
                        
                                Giá tổng cộng đã bao gồm thuế phí 

                        - ~~totalPriceByHotelCurrency (number, optional),~~
                        
                        - totalRooms (integer, optional)
            
                            !!! quote "" 

                                Số lượng phòng còn trống 

                    - roomArea (RoomArea, optional)
            
                        !!! quote "" 

                            Thông tin về diện tích căn phòng 

                            - `squareFeet`: Diện tích của phòng được tính bằng feet vuông 
                        
                            - `squareMeters`: Diện tích của phòng được tính bằng mét vuông  
                        
                    - bedGroupStatics (Array[BedGroupStatic], optional)
                        
                        !!! quote "" 
                            
                            Mảng các đối tượng nhóm giường trong phòng

                        - id (String, optional)
            
                            !!! quote "" 

                                mã định danh nhóm giường 

                        - name (String, optional)
            
                            !!! quote "" 

                                Tên nhóm giường 

                        - ~~value (String, optional)~~
                        
                    - views (Array[View], optional)
            
                        !!! quote "" 

                            Thông tin mô tả hướng nhìn của phòng 

                        - id (String, optional)
                            
                            !!! quote "" 

                                mã định danh hướng nhìn

                        - name (String, optional)
            
                            !!! quote "" 

                                Mô tả hướng nhìn 

                        - ~~value (String, optional)~~ 
                        
                    - occupancyAllowed (OccupancyAllowed, optional)
            
                        !!! quote "" 

                            Thông tin về số người ở được phép 

                        - roomMaxAllowed (RoomMaxAllowed, optional)
            
                            !!! quote "" 

                                Sức chứa tối đa 

                            - adult (integer, optional)
            
                                !!! quote "" 

                                    Số người lớn

                            - children (integer, optional)
            
                                !!! quote "" 

                                    Số trẻ em 

                            - total (integer, optional)
            
                                !!! quote "" 

                                    Tổng số người

                        - ~~roomAgeCategories (Array[Attribute], optional)~~
                        
                    - amenities (Array[Amenity], optional)
            
                        !!! quote "" 

                            Mảng chứa đối tương thông tin tiện nghi của phòng 

                        - id (string, optional),
                    
                            !!! quote "" 
                        
                                Mã định danh tiện nghi phòng 

                        - name (string, optional),
                    
                            !!! quote "" 
                        
                                Tên tiện nghi phòng 

                        - ~~value (string, optional)~~
                        
                        - group (string, optional)
                            
                            !!! quote "" 
    
                                Thông tin tiện nghi của phòng được gom nhóm, với các nhóm sau  

                                - `OTHER`: Tiện nghi khác
                            
                                - `BEDROOM`: Tiện nghi phòng ngủ 
                                
                                - `BATHROOM`: Tiện nghi phòng tắm 
                                
                                - `ENTERTAINMENT`: Giải trí đa phương tiện trong phòng 
                                
                                - `FOOD_AND_DRINK`: Tiện nghi về đồ ăn thức uống trong phòng 
                                
                                - `ROOM_VIEW`: Hướng nhìn 
                                
                                - `INTERNET`: Mạng intenet
                                
                                - `SMOKING`: Hút thuốc 
                            
                - spokenLanguage (Array[Attribute], optional),
                    
                    !!! quote "" 
                        
                        Các ngôn ngữ giao tiếp với nhân viên khách sạn.

                    - id (string, optional),
                    
                        !!! quote "" 
                        
                            Mã định danh ngôn ngữ 

                    - name (string, optional),
                    
                        !!! quote "" 
                        
                            Tên ngôn ngữ 

                    - ~~value (string, optional)~~
                    
                - statistics (Array[Attribute], optional),
                    
                    !!! quote "" 
                        
                        Thống kê về tài sản, chẳng hạn như số tầng

                    - id (string, optional),
                    
                        !!! quote "" 
                        
                            Mã định danh thống kê 

                    - name (string, optional),
                    
                        !!! quote "" 
                        
                            Mô tả thống kê bao gồm tên và giá trị thống kê  
            
                            ```json
                            {
                                "id": "52",
                                "name": "Tổng số phòng: - 335",
                                "value": "335"
                            }
                            ```

                    - value (string, optional)
                        
                        !!! quote "" 

                            Giá trị của thống kê

                - supplier (string, optional) = [EXPEDIA, AXISROOM, BEDLINKER],
                    
                    !!! quote "" 
                        
                        Nguồn khách sạn 

                - tags (Array[string], optional),
                    
                    !!! quote "" 
                        
                        Thẻ được gắn cho khách sạn, để xác định một số yêu cầu đặc biệt 

                - themes (Array[Attribute], optional)
            
                    !!! quote "" 

                        Mảng đối tượng chứa thông tin về chủ đề của khách sạn 

                    - id (string, optional),
                    
                        !!! quote "" 
                        
                            Mã định chủ đề  

                    - name (string, optional),
                    
                        !!! quote "" 
                        
                            Tên chủ đề 

                    - ~~value (string, optional)~~

                - masterPropertyId (Long, optional)

                    !!! quote ""

                        Mã định danh khách sạn chính.
                
                    
        - duration (integer, optional),
        - errors (Array[Error], optional),
        - infos (Array[Info], optional),
        - success (boolean, optional),
        - textMessage (string, optional)

=== "Example"
    ```json 
    {
        "result": {
            "tripId": "QtmwRXkB5hnyw2pfga4b",
            "searchId": "eyJzZWFyY2hJZCI6IiIsImNoZWNrSW4iOiIyMDIxLTA3LTIzIiwiY2hlY2tPdXQiOiIyMDIxLTA3LTI0IiwicGF4SW5mb3MiOlt7ImFkdWx0UXVhbnRpdHkiOjIsImNoaWxkUXVhbnRpdHkiOjAsImluZmFudFF1YW50aXR5IjowLCJjaGlsZEFnZXMiOltdfV0sImxhbmd1YWdlIjoidmkiLCJjdXJyZW5jeSI6IlZORCIsInN1cHBsaWVyIjoiRVhQRURJQSIsInNlYXJjaENvZGUiOiIxNzgyNjIiLCJzZWFyY2hUeXBlIjoiTVVMVElfQ0lUWV9WSUNJTklUWSJ9",
            "propertyAllRate": {
            "propertyId": "481659",
            "propertyName": "Khách sạn Continental Sài Gòn",
            "supplier": "EXPEDIA",
            "language": "vi",
            "currency": "VND",
            "rating": {
                "ratingProperty": {
                "rating": "4.0",
                "type": "Star"
                },
                "ratingGuest": {
                "count": 995,
                "score": "4.133333333333333",
                "recommendationPercent": "80.2",
                "overall": "4.1",
                "cleanliness": "4.1",
                "service": "4.1",
                "comfort": "4.0",
                "condition": "3.8",
                "location": "4.7",
                "neighborhood": "4.7",
                "quality": "",
                "value": "3.8",
                "amenities": "3.9"
                }
            },
            "address": {
                "lineOne": "132 - 134 Đồng Khởi, Q.1",
                "lineTow": "",
                "stateProvinceCode": "",
                "stateProvinceName": "",
                "postalCode": "70000",
                "city": "TP.Hồ Chí Minh",
                "countryCode": "VN",
                "countryName": ""
            },
            "latitude": 10.776629,
            "longitude": 106.702459,
            "masterPropertyId": 1,
            "propertyCategory": {
                "id": "1",
                "name": "Khách sạn"
            },
            "checkin": {
                "beginTime": "02:00 PM",
                "endTime": "12:00 AM"
            },
            "checkout": {
                "endTime": "12:00"
            },
            "rank": 11042,
            "fees": [],
            "inclusions": [
                {
                "id": "1073745021",
                "name": "Để phòng trống giữa các lượt khách 24 giờ",
                "value": "24 giờ"
                },
                {
                "id": "1073745053",
                "name": "Nơi lưu trú xác nhận đang áp dụng biện pháp an toàn cho khách",
                "value": ""
                },
                {
                "id": "1073745047",
                "name": "Có kiểm tra nhiệt độ cho khách",
                "value": ""
                },
                {
                "id": "1073745004",
                "name": "Có áp dụng biện pháp giãn cách xã hội",
                "value": ""
                },
                {
                "id": "1073745045",
                "name": "Thường xuyên kiểm tra nhiệt độ nhân viên",
                "value": ""
                },
                {
                "id": "1073744992",
                "name": "Nơi lưu trú được vệ sinh bằng dung dịch khử trùng",
                "value": ""
                },
                {
                "id": "1073745002",
                "name": "Có cung cấp nước rửa tay miễn phí cho khách",
                "value": ""
                },
                {
                "id": "1073745013",
                "name": "Nơi lưu trú xác nhận đang áp dụng biện pháp vệ sinh tăng cường",
                "value": ""
                },
                {
                "id": "1073744994",
                "name": "Nhân viên có mang thiết bị bảo hộ cá nhân",
                "value": ""
                },
                {
                "id": "1073745049",
                "name": "Giặt tấm trải giường và khăn ở nhiệt độ tối thiểu 60°C",
                "value": ""
                },
                {
                "id": "2545",
                "name": "Không có nôi/cũi (giường cho trẻ sơ sinh)",
                "value": ""
                },
                {
                "id": "2544",
                "name": "Không có giường gấp/giường phụ",
                "value": ""
                },
                {
                "id": "1073745051",
                "name": "Những bề mặt thường có nhiều tiếp xúc được vệ sinh bằng dung dịch khử trùng",
                "value": ""
                },
                {
                "id": "1073745062",
                "name": "Nơi lưu trú áp dụng tiêu chuẩn vệ sinh Intertek Cristal (Chuyên viên bên thứ 3 - Toàn cầu)",
                "value": ""
                },
                {
                "id": "2808",
                "name": "Không được mang vật nuôi hỗ trợ người khuyết tật",
                "value": ""
                },
                {
                "id": "2050",
                "name": "Không được phép mang vật nuôi",
                "value": ""
                }
            ],
            "policies": [
                {
                "id": "1",
                "name": "know_before_you_go",
                "value": "<ul>  <li>Chỉ khách đã đăng ký được lưu trú tại phòng. </li><li>Khách không được phép mang vật nuôi, bao gồm cả vật nuôi hỗ trợ người khuyết tật, vào nơi lưu trú này. </li><li>Nơi lưu trú cho biết đang áp dụng các biện pháp vệ sinh tăng cường và an toàn cho khách.</li><li>Vệ sinh nơi lưu trú bằng dung dịch khử trùng, những bề mặt thường có nhiều tiếp xúc được vệ sinh bằng dung dịch khử trùng giữa các lần lưu trú và giặt tấm trải giường và khăn ở nhiệt độ tối thiểu 60°C.</li><li>Giãn cách xã hội, nhân viên mang thiết bị bảo hộ cá nhân, kiểm tra nhiệt độ cho nhân viên định kỳ, kiểm tra nhiệt độ cho khách và cung cấp nước rửa tay cho khách.</li><li>Tất cả phòng đều được để trống tối thiểu 24 giờ giữa mỗi lượt khách.</li><li>Nơi lưu trú xác nhận đang áp dụng biện pháp vệ sinh và khử trùng theo quy định Intertek Cristal (Chuyên viên bên thứ 3 - Toàn cầu).</li>\n </ul>"
                }
            ],
            "descriptions": [
                {
                "id": "1",
                "name": "amenities",
                "value": "Hãy để mình được chăm sóc đặc biệt với dịch vụ trị liệu toàn thân trong khuôn viên hay thư giãn cùng những tiện nghi, dịch vụ như câu lạc bộ sức khỏe. Khách sạn này còn có truy cập Internet không dây miễn phí, dịch vụ tư vấn/hỗ trợ khách và cửa hàng quà tặng hoặc quầy thông tin."
                },
                {
                "id": "2",
                "name": "dining",
                "value": "Dùng bữa tại Continental Palace Restau, một trong 2 nhà hàng của khách sạn hoặc nghỉ lại trong phòng và tận hưởng dịch vụ phòng 24 giờ. Thức ăn nhẹ cũng có ở quán cà phê. Đập tan cơn khát với đồ uống yêu thích tại quầy bar/khu lounge. Khách có thể dùng bữa sáng buffet miễn phí hàng ngày từ 06:30 đến 09:00."
                },
                {
                "id": "5",
                "name": "business_amenities",
                "value": "Có nhiều dịch vụ, tiện ích dành cho khách, bao gồm trung tâm dịch vụ văn phòng, báo miễn phí ở sảnh và dịch vụ giặt ủi/giặt khô. Khách có thể được phục vụ dịch vụ đón khách tại nhà ga với khoản phụ phí nhỏ."
                },
                {
                "id": "6",
                "name": "rooms",
                "value": "Hãy nghỉ ngơi thoải mái như đang ở nhà mình tại một trong 80 phòng được trang bị máy điều hòa cùng minibar và TV LCD. Quý vị sẽ luôn có thể giữ liên lạc bằng truy cập Internet không dây miễn phí ngay tại phòng. Phòng tắm riêng với vòi sen/bồn tắm kết hợp có đồ dùng nhà tắm miễn phí và áo choàng tắm. Tiện nghi phòng bao gồm két bảo mật và bàn; bên cạnh đó dịch vụ dọn phòng cũng phục vụ hàng ngày."
                },
                {
                "id": "7",
                "name": "attractions",
                "value": "Khoảng cách được làm tròn đến 0,1 km (hoặc dặm). <br /> <p>Đồng Khởi - 0,1 km <br /> Quảng trường Ủy ban Nhân dân TP.HCM - 0,1 km <br /> Parkson Plaza - 0,2 km <br /> Nhà hát Lớn - 0,2 km <br /> Phố đi bộ Nguyễn Huệ - 0,2 km <br /> Trung tâm Thương mại Vincom - 0,2 km <br /> Ủy ban Nhân dân TP.HCM - 0,2 km <br /> Trung tâm Thương mại Lucky Plaza - 0,3 km <br /> Thương xá Tax - 0,4 km <br /> Bưu điện Trung tâm Sài Gòn - 0,5 km <br /> Quảng trường Nhà thờ Đức Bà - 0,5 km <br /> Trung tâm Thương mại Taka Plaza - 0,5 km <br /> Nhà thờ Đức Bà Sài Gòn - 0,5 km <br /> Bảo tàng Thành phố Hồ Chí Minh - 0,6 km <br /> Khu Lãnh sự - 0,6 km <br /> </p><p>Khách có thể đến Khách sạn Continental Sài Gòn qua Sân bay Quốc tế Tân Sơn Nhất - Quận Tân Bình (SGN), cách khoảng 7,1 km </p>"
                },
                {
                "id": "8",
                "name": "location",
                "value": "Khách sạn Continental Sài Gòn ở trung tâm Thành phố Hồ Chí Minh, chỉ cách Nhà hát Lớn và Trung tâm Thương mại Vincom vài bước.  Khách sạn 4 sao này cách Sài Gòn Square 0,5 mi (0,7 km) và Chợ Bến Thành 0,6 mi (0,9 km)."
                },
                {
                "id": "9",
                "name": "headline",
                "value": "Gần Sài Gòn Square"
                }
            ],
            "themes": [
                {
                "id": "2328",
                "name": "Nơi lưu trú phù hợp với khách đi công tác",
                "value": ""
                },
                {
                "id": "2333",
                "name": "Nơi lưu trú phù hợp cho gia đình",
                "value": ""
                }
            ],
            "statistics": [
                {
                "id": "55",
                "name": "Số lượng tòa nhà:  - 1",
                "value": "1"
                },
                {
                "id": "2515",
                "name": "Năm xây dựng:  - 1880",
                "value": "1880"
                },
                {
                "id": "52",
                "name": "Tổng số phòng:  - 80",
                "value": "80"
                },
                {
                "id": "54",
                "name": "Số tầng: 3",
                "value": "3"
                }
            ],
            "amenities": [
                {
                "id": "2065",
                "name": "Trung tâm hành chính, văn phòng",
                "value": "",
                "group": "CONVENIENCES"
                },
                {
                "id": "2063",
                "name": "Quầy tiếp tân 24 giờ",
                "value": "",
                "group": "POPULAR_FACILITIES"
                },
                {
                "id": "2537",
                "name": "Số lượng nhà hàng:  - 2",
                "value": "",
                "group": "FOOD_AND_DRINK"
                },
                {
                "id": "3",
                "name": "Bar/lounge",
                "value": "",
                "group": "POPULAR_FACILITIES"
                },
                {
                "id": "3637",
                "name": "Một phòng họp",
                "value": "",
                "group": "BUSINESS_SERVICE"
                },
                {
                "id": "4003",
                "name": "Trông giữ/bảo quản hành lý",
                "value": "",
                "group": "SERVICES"
                },
                {
                "id": "2001",
                "name": "Bữa sáng miễn phí",
                "value": "",
                "group": "POPULAR_FACILITIES"
                },
                {
                "id": "369",
                "name": "Trang thiết bị giặt ủi",
                "value": "",
                "group": "CONVENIENCES"
                },
                {
                "id": "8",
                "name": "Thang máy",
                "value": "",
                "group": "CONVENIENCES"
                },
                {
                "id": "4514",
                "name": "Sân thượng/sân hiên",
                "value": "",
                "group": "CONVENIENCES"
                },
                {
                "id": "43",
                "name": "Dịch vụ concierge hỗ trợ khách",
                "value": "",
                "group": "SERVICES"
                },
                {
                "id": "2016",
                "name": "Két an toàn tại quầy tiếp tân",
                "value": "",
                "group": "POPULAR_FACILITIES"
                },
                {
                "id": "2137",
                "name": "Khách sạn không khói thuốc",
                "value": "",
                "group": "POPULAR_FACILITIES"
                },
                {
                "id": "3500",
                "name": "Bar chuyên các món ăn nhẹ/deli",
                "value": "",
                "group": "FOOD_AND_DRINK"
                },
                {
                "id": "2008",
                "name": "Câu lạc bộ sức khỏe",
                "value": "",
                "group": "FITNESS_AND_SPA"
                },
                {
                "id": "2129",
                "name": "Phòng trị liệu spa",
                "value": "",
                "group": "FITNESS_AND_SPA"
                },
                {
                "id": "378",
                "name": "Vườn",
                "value": "",
                "group": "CONVENIENCES"
                },
                {
                "id": "2004",
                "name": "Quán cà phê",
                "value": "",
                "group": "POPULAR_FACILITIES"
                },
                {
                "id": "2047",
                "name": "Báo miễn phí tại sảnh",
                "value": "",
                "group": "CONVENIENCES"
                },
                {
                "id": "2167",
                "name": "Dịch vụ cưới",
                "value": "",
                "group": "SERVICES"
                },
                {
                "id": "2387",
                "name": "Dịch vụ hỗ trợ tour/vé du lịch",
                "value": "",
                "group": "RECREATION"
                },
                {
                "id": "44",
                "name": "Cửa hàng quà tặng/quầy báo",
                "value": "",
                "group": "CONVENIENCES"
                },
                {
                "id": "2070",
                "name": "Dịch vụ giặt khô/giặt ủi",
                "value": "",
                "group": "SERVICES"
                },
                {
                "id": "45",
                "name": "Khu mua sắm trong khuôn viên",
                "value": "",
                "group": "CONVENIENCES"
                },
                {
                "id": "4010",
                "name": "Đón từ ga tàu (phụ phí)",
                "value": "",
                "group": "PARKING_AND_TRANSPORT"
                },
                {
                "id": "1073744110",
                "name": "Phòng khiêu vũ",
                "value": "",
                "group": "ENTERTAINMENT"
                },
                {
                "id": "2390",
                "name": "Wifi miễn phí",
                "value": "",
                "group": "POPULAR_FACILITIES"
                }
            ],
            "images": [
                {
                "caption": "Ảnh nổi bật",
                "position": 1,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/cbe48cdd_z.jpg"
                },
                {
                "caption": "Tiền sảnh",
                "position": 2,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/580dff7d_z.jpg"
                },
                {
                "caption": "Phòng",
                "position": 3,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/394e4ca3_z.jpg"
                },
                {
                "caption": "Phòng",
                "position": 4,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/b6e21a19_z.jpg"
                },
                {
                "caption": "Phòng",
                "position": 5,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/03f49af2_z.jpg"
                },
                {
                "caption": "Phòng",
                "position": 6,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/7563f797_z.jpg"
                },
                {
                "caption": "Phòng",
                "position": 7,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/d7bc598e_z.jpg"
                },
                {
                "caption": "Phòng",
                "position": 8,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/698c8de8_z.jpg"
                },
                {
                "caption": "Phòng",
                "position": 9,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/eb9050ee_z.jpg"
                },
                {
                "caption": "Phòng",
                "position": 10,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/e9786e7a_z.jpg"
                },
                {
                "caption": "Phòng",
                "position": 11,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/69a5669a_z.jpg"
                },
                {
                "caption": "Phòng",
                "position": 12,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/4539c566_z.jpg"
                },
                {
                "caption": "Phòng",
                "position": 13,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/c7d3697b_z.jpg"
                },
                {
                "caption": "Phòng",
                "position": 14,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/8dcfe39b_z.jpg"
                },
                {
                "caption": "Phòng",
                "position": 15,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/cf01e333_z.jpg"
                },
                {
                "caption": "Phòng",
                "position": 16,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/2bd2576e_z.jpg"
                },
                {
                "caption": "Phòng",
                "position": 17,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/9b74d7d1_z.jpg"
                },
                {
                "caption": "Phòng",
                "position": 18,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/95edabdd_z.jpg"
                },
                {
                "caption": "Phòng",
                "position": 19,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/981d451d_z.jpg"
                },
                {
                "caption": "Phòng",
                "position": 20,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/e09b3e04_z.jpg"
                },
                {
                "caption": "Phòng",
                "position": 21,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/3e84b5ea_z.jpg"
                },
                {
                "caption": "Phòng",
                "position": 22,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/ca41955a_z.jpg"
                },
                {
                "caption": "Phòng",
                "position": 23,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/b981dc7e_z.jpg"
                },
                {
                "caption": "Phòng",
                "position": 24,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/0a875a50_z.jpg"
                },
                {
                "caption": "Phòng",
                "position": 25,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/bf27b217_z.jpg"
                },
                {
                "caption": "Khu phòng khách",
                "position": 26,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/cf00f0ba_z.jpg"
                },
                {
                "caption": "Ban công",
                "position": 27,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/5b71c73f_z.jpg"
                },
                {
                "caption": "Ban công",
                "position": 28,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/97d39dd7_z.jpg"
                },
                {
                "caption": "Tiện nghi tại phòng",
                "position": 29,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/fcf3ac20_z.jpg"
                },
                {
                "caption": "Tiện nghi tại phòng",
                "position": 30,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/c00dc523_z.jpg"
                },
                {
                "caption": "Quang cảnh từ phòng",
                "position": 31,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/a90b6f48_z.jpg"
                },
                {
                "caption": "Quang cảnh từ phòng",
                "position": 32,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/6bea4654_z.jpg"
                },
                {
                "caption": "Quang cảnh từ phòng",
                "position": 33,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/e5a9e6ab_z.jpg"
                },
                {
                "caption": "Quang cảnh từ phòng",
                "position": 34,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/37a2958e_z.jpg"
                },
                {
                "caption": "Quang cảnh từ phòng",
                "position": 35,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/1da56c1a_z.jpg"
                },
                {
                "caption": "Phòng tắm",
                "position": 36,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/ee07c9cf_z.jpg"
                },
                {
                "caption": "Phòng tắm",
                "position": 37,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/891630e3_z.jpg"
                },
                {
                "caption": "Phòng tắm",
                "position": 38,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/69f7e479_z.jpg"
                },
                {
                "caption": "Bồn tắm vòi sen trong phòng tắm",
                "position": 39,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/e2792550_z.jpg"
                },
                {
                "caption": "Tiện nghi phòng tắm",
                "position": 40,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/ae3f3563_z.jpg"
                },
                {
                "caption": "Tiện nghi phòng tắm",
                "position": 41,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/ad72ed9e_z.jpg"
                },
                {
                "caption": "Tiện nghi phòng tắm",
                "position": 42,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/cdc96496_z.jpg"
                },
                {
                "caption": "Tiện nghi phòng tắm",
                "position": 43,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/fcb69d05_z.jpg"
                },
                {
                "caption": "Tiện nghi phòng tắm",
                "position": 44,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/3c87904a_z.jpg"
                },
                {
                "caption": "Khu thể hình",
                "position": 45,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/024eb2e2_z.jpg"
                },
                {
                "caption": "Spa",
                "position": 46,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/2f407e97_z.jpg"
                },
                {
                "caption": "Khu phục vụ bữa sáng",
                "position": 47,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/f38528f1_z.jpg"
                },
                {
                "caption": "Nhà hàng",
                "position": 48,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/fc1911aa_z.jpg"
                },
                {
                "caption": "Bar",
                "position": 49,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/32906018_z.jpg"
                },
                {
                "caption": "Phòng khiêu vũ",
                "position": 50,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/b3d3586b_z.jpg"
                },
                {
                "caption": "Khu phòng họp",
                "position": 51,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/6c965fcf_z.jpg"
                },
                {
                "caption": "Mặt tiền nơi lưu trú - Ban đêm",
                "position": 52,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/73dd6a91_z.jpg"
                },
                {
                "caption": "Khu ẩm thực ngoài trời",
                "position": 53,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/1a37bb97_z.jpg"
                },
                {
                "caption": "Hiên",
                "position": 54,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/7d9fe885_z.jpg"
                },
                {
                "caption": "Hiên",
                "position": 55,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/6143da6b_z.jpg"
                },
                {
                "caption": "Cảnh từ trên cao",
                "position": 56,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/7d1ba1fb_z.jpg"
                },
                {
                "caption": "Quang cảnh từ khách sạn",
                "position": 57,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/6f5fb460_z.jpg"
                },
                {
                "caption": "Nhãn vệ sinh",
                "position": 58,
                "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/2f2889dd_z.jpg"
                }
            ],
            "rooms": [
                {
                "id": "201866846",
                "name": "Phòng Superior",
                "descriptions": [
                    {
                    "id": "1",
                    "name": "overview",
                    "value": "<p><strong>1 giường cỡ queen hoặc 2 giường đơn</strong></p><p>35 mét vuông</p><br/><p><b>Internet</b> - Wifi miễn phí <br /> <p><b>Giải trí</b> - TV LCD 46 inch với các kênh truyền hình cáp</p><p><b>Ăn uống</b> - Dụng cụ pha cà phê/trà, minibar, dịch vụ phòng 24 giờ và nước đóng chai miễn phí</p> <p><b>Giấc ngủ</b> - Dịch vụ dọn phòng buổi tối</p> <p><b>Phòng tắm</b> - Phòng tắm riêng với vòi sen/bồn tắm kết hợp, áo choàng tắm và dép đi trong nhà</p><p><b>Tiện nghi</b> - Két an toàn, báo miễn phí các ngày trong tuần và bàn</p><p><b>Tiện nghi</b> - Máy điều hòa nhiệt độ và dịch vụ dọn phòng hàng ngày</p><p><b>Thông tin cần biết</b> - Không có bộ trải giường</p> <p>Không hút thuốc</p>"
                    }
                ],
                "images": [
                    {
                    "caption": "Phòng",
                    "position": 1,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/698c8de8_z.jpg"
                    },
                    {
                    "caption": "Phòng",
                    "position": 2,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/4539c566_z.jpg"
                    },
                    {
                    "caption": "Phòng",
                    "position": 3,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/8dcfe39b_z.jpg"
                    },
                    {
                    "caption": "Phòng tắm",
                    "position": 4,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/ee07c9cf_z.jpg"
                    },
                    {
                    "caption": "Tiện nghi phòng tắm",
                    "position": 5,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/fcb69d05_z.jpg"
                    }
                ],
                "roomArea": {
                    "squareMeters": 35,
                    "squareFeet": 377
                },
                "ratePlans": [
                    {
                    "ratePlanId": "209445837",
                    "ratePlanName": "",
                    "totalRooms": 5,
                    "breakfastIncluded": true,
                    "refundable": true,
                    "cancelFree": true,
                    "basePrice": 1043680.0,
                    "promo": true,
                    "basePriceBeforePromo": 1490972.0,
                    "amenities": [
                        {
                        "id": "2205",
                        "name": "Bữa sáng buffet",
                        "value": "",
                        "group": ""
                        },
                        {
                        "id": "1073742786",
                        "name": "Bữa sáng miễn phí",
                        "value": "",
                        "group": ""
                        },
                        {
                        "id": "2109",
                        "name": "Đậu xe miễn phí",
                        "value": "",
                        "group": ""
                        },
                        {
                        "id": "2192",
                        "name": "Wifi miễn phí",
                        "value": "",
                        "group": ""
                        }
                    ],
                    "bedGroups": [
                        {
                        "id": "37341",
                        "description": "2 giường đơn",
                        "configurations": [
                            {
                            "size": "Twin",
                            "type": "TwinBed",
                            "quantity": 2
                            }
                        ]
                        },
                        {
                        "id": "37310",
                        "description": "1 giường cỡ queen",
                        "configurations": [
                            {
                            "size": "Queen",
                            "type": "QueenBed",
                            "quantity": 1
                            }
                        ]
                        }
                    ],
                    "cancelPenalties": [
                        {
                        "startDate": "2021-07-09T18:00:00.000+07:00",
                        "endDate": "2021-07-23T18:00:00.000+07:00",
                        "type": "PERCENT",
                        "currency": "VND",
                        "percent": "100%",
                        "nights": "",
                        "amount": "",
                        "description": ""
                        }
                    ],
                    "paxPrice": [
                        {
                        "paxInfo": {
                            "adultQuantity": 2,
                            "childQuantity": 0,
                            "infantQuantity": 0,
                            "childAges": []
                        },
                        "nightPrices": [
                            {
                            "nightKey": "0",
                            "nightPriceDetails": [
                                {
                                "name": "base_rate",
                                "value": 1043680.0,
                                "valueByHotelCurrency": "1043680.0 VND"
                                },
                                {
                                "name": "tax_and_service_fee",
                                "value": 161770.0,
                                "valueByHotelCurrency": "161770.0 VND"
                                }
                            ]
                            }
                        ]
                        }
                    ],
                    "totalPrice": 1205450.0,
                    "totalPriceByHotelCurrency": 1205450.0,
                    "taxAndFees": 161770.0,
                    "fees": {},
                    "promoDescription": "Tiết kiệm 30%",
                    "cancelFreeBeforeDate": "2021-07-09T00:00:00+07:00",
                    "meals": []
                    }
                ],
                "bedGroupStatics": [
                    {
                    "id": "37341",
                    "name": "2 giường đơn",
                    "value": ""
                    },
                    {
                    "id": "37310",
                    "name": "1 giường cỡ queen",
                    "value": ""
                    }
                ],
                "views": [],
                "occupancyAllowed": {
                    "roomMaxAllowed": {
                    "total": 2,
                    "children": 1,
                    "adult": 2
                    },
                    "roomAgeCategories": [
                    {
                        "id": "",
                        "name": "ChildAgeA",
                        "value": "3"
                    },
                    {
                        "id": "",
                        "name": "Infant",
                        "value": "0"
                    },
                    {
                        "id": "",
                        "name": "Adult",
                        "value": "10"
                    }
                    ]
                },
                "amenities": [
                    {
                    "id": "2162",
                    "name": "Dép đi trong nhà",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "2183",
                    "name": "Buồng tắm vòi sen/bồn tắm kết hợp",
                    "value": "",
                    "group": "BATHROOM"
                    },
                    {
                    "id": "141",
                    "name": "Phòng tắm riêng",
                    "value": "",
                    "group": "BATHROOM"
                    },
                    {
                    "id": "142",
                    "name": "Áo choàng tắm",
                    "value": "",
                    "group": "BATHROOM"
                    },
                    {
                    "id": "143",
                    "name": "Đồ dùng nhà tắm miễn phí",
                    "value": "",
                    "group": "BATHROOM"
                    },
                    {
                    "id": "1",
                    "name": "Máy điều hòa",
                    "value": "",
                    "group": "BEDROOM"
                    },
                    {
                    "id": "146",
                    "name": "Két an toàn tại phòng",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "1073743929",
                    "name": "Không có bộ trải giường",
                    "value": "",
                    "group": "BEDROOM"
                    },
                    {
                    "id": "2015",
                    "name": "Dịch vụ phòng (24 giờ)",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "2575",
                    "name": "TV LCD",
                    "value": "",
                    "group": "ENTERTAINMENT"
                    },
                    {
                    "id": "2057",
                    "name": "Nước đóng chai miễn phí",
                    "value": "",
                    "group": "FOOD_AND_DRINK"
                    },
                    {
                    "id": "2398",
                    "name": "Dịch vụ truyền hình cáp",
                    "value": "",
                    "group": "ENTERTAINMENT"
                    },
                    {
                    "id": "132",
                    "name": "Dụng cụ pha cà phê/trà",
                    "value": "",
                    "group": "FOOD_AND_DRINK"
                    },
                    {
                    "id": "133",
                    "name": "Dọn phòng hàng ngày",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "2403",
                    "name": "Wifi miễn phí",
                    "value": "",
                    "group": "INTERNET"
                    },
                    {
                    "id": "2402",
                    "name": "HDTV",
                    "value": "",
                    "group": "ENTERTAINMENT"
                    },
                    {
                    "id": "2026",
                    "name": "Bàn",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "2180",
                    "name": "Máy sấy tóc (theo yêu cầu)",
                    "value": "",
                    "group": "BATHROOM"
                    },
                    {
                    "id": "6176",
                    "name": "Không hút thuốc",
                    "value": "",
                    "group": "SMOKING"
                    },
                    {
                    "id": "26",
                    "name": "TV",
                    "value": "",
                    "group": "ENTERTAINMENT"
                    },
                    {
                    "id": "1073745067",
                    "name": "Không có bộ trải giường",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "2056",
                    "name": "Dịch vụ dọn phòng buổi tối",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "2031",
                    "name": "Báo các ngày trong tuần miễn phí",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "131",
                    "name": "Minibar",
                    "value": "",
                    "group": "FOOD_AND_DRINK"
                    }
                ]
                },
                {
                "id": "201866844",
                "name": "Phòng Deluxe, Quang cảnh vườn",
                "descriptions": [
                    {
                    "id": "1",
                    "name": "overview",
                    "value": "<p><strong>1 giường cỡ queen hoặc 2 giường đơn</strong></p><p>Phòng 38 mét vuông với quang cảnh vườn và sân trong</p><br/><p><b>Internet</b> - Wifi miễn phí <br /> <p><b>Giải trí</b> - TV LCD 46 inch với các kênh truyền hình vệ tinh</p><p><b>Ăn uống</b> - Dụng cụ pha cà phê/trà, minibar, dịch vụ phòng 24 giờ và nước đóng chai miễn phí</p> <p><b>Giấc ngủ</b> - Giường đệm bông và dịch vụ dọn phòng buổi tối</p> <p><b>Phòng tắm</b> - Phòng tắm riêng với vòi sen/bồn tắm kết hợp, áo choàng tắm và dép đi trong nhà</p><p><b>Tiện nghi</b> - Két an toàn, báo miễn phí các ngày trong tuần và bàn</p><p><b>Tiện nghi</b> - Máy điều hòa nhiệt độ và dịch vụ dọn phòng hàng ngày</p><p><b>Thông tin cần biết</b> - Không có bộ trải giường</p> <p>Không hút thuốc</p>"
                    }
                ],
                "images": [
                    {
                    "caption": "Phòng",
                    "position": 1,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/c7d3697b_z.jpg"
                    },
                    {
                    "caption": "Phòng",
                    "position": 2,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/b981dc7e_z.jpg"
                    },
                    {
                    "caption": "Tiện nghi tại phòng",
                    "position": 3,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/fcf3ac20_z.jpg"
                    },
                    {
                    "caption": "Tiện nghi tại phòng",
                    "position": 4,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/c00dc523_z.jpg"
                    },
                    {
                    "caption": "Quang cảnh từ phòng",
                    "position": 5,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/1da56c1a_z.jpg"
                    },
                    {
                    "caption": "Phòng tắm",
                    "position": 6,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/ee07c9cf_z.jpg"
                    },
                    {
                    "caption": "Tiện nghi phòng tắm",
                    "position": 7,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/cdc96496_z.jpg"
                    }
                ],
                "roomArea": {
                    "squareMeters": 38,
                    "squareFeet": 409
                },
                "ratePlans": [
                    {
                    "ratePlanId": "232235391",
                    "ratePlanName": "",
                    "totalRooms": 10,
                    "breakfastIncluded": true,
                    "refundable": true,
                    "cancelFree": true,
                    "basePrice": 1468144.0,
                    "promo": true,
                    "basePriceBeforePromo": 2097349.0,
                    "amenities": [
                        {
                        "id": "1073742786",
                        "name": "Bữa sáng miễn phí",
                        "value": "",
                        "group": ""
                        },
                        {
                        "id": "2192",
                        "name": "Wifi miễn phí",
                        "value": "",
                        "group": ""
                        }
                    ],
                    "bedGroups": [
                        {
                        "id": "37341",
                        "description": "2 giường đơn",
                        "configurations": [
                            {
                            "size": "Twin",
                            "type": "TwinBed",
                            "quantity": 2
                            }
                        ]
                        },
                        {
                        "id": "37310",
                        "description": "1 giường cỡ queen",
                        "configurations": [
                            {
                            "size": "Queen",
                            "type": "QueenBed",
                            "quantity": 1
                            }
                        ]
                        }
                    ],
                    "cancelPenalties": [
                        {
                        "startDate": "2021-07-22T18:00:00.000+07:00",
                        "endDate": "2021-07-23T18:00:00.000+07:00",
                        "type": "PERCENT",
                        "currency": "VND",
                        "percent": "100%",
                        "nights": "",
                        "amount": "",
                        "description": ""
                        }
                    ],
                    "paxPrice": [
                        {
                        "paxInfo": {
                            "adultQuantity": 2,
                            "childQuantity": 0,
                            "infantQuantity": 0,
                            "childAges": []
                        },
                        "nightPrices": [
                            {
                            "nightKey": "0",
                            "nightPriceDetails": [
                                {
                                "name": "base_rate",
                                "value": 1468144.0,
                                "valueByHotelCurrency": "1468144.0 VND"
                                },
                                {
                                "name": "tax_and_service_fee",
                                "value": 227563.0,
                                "valueByHotelCurrency": "227563.0 VND"
                                }
                            ]
                            }
                        ]
                        }
                    ],
                    "totalPrice": 1695707.0,
                    "totalPriceByHotelCurrency": 1695707.0,
                    "taxAndFees": 227563.0,
                    "fees": {},
                    "promoDescription": "Tiết kiệm 30%",
                    "cancelFreeBeforeDate": "2021-07-22T00:00:00+07:00",
                    "meals": []
                    },
                    {
                    "ratePlanId": "210168428",
                    "ratePlanName": "",
                    "totalRooms": 10,
                    "breakfastIncluded": true,
                    "refundable": false,
                    "cancelFree": false,
                    "basePrice": 1468144.0,
                    "promo": true,
                    "basePriceBeforePromo": 2097349.0,
                    "amenities": [
                        {
                        "id": "2205",
                        "name": "Bữa sáng buffet",
                        "value": "",
                        "group": ""
                        },
                        {
                        "id": "1073742786",
                        "name": "Bữa sáng miễn phí",
                        "value": "",
                        "group": ""
                        },
                        {
                        "id": "2109",
                        "name": "Đậu xe miễn phí",
                        "value": "",
                        "group": ""
                        },
                        {
                        "id": "2192",
                        "name": "Wifi miễn phí",
                        "value": "",
                        "group": ""
                        }
                    ],
                    "bedGroups": [
                        {
                        "id": "37341",
                        "description": "2 giường đơn",
                        "configurations": [
                            {
                            "size": "Twin",
                            "type": "TwinBed",
                            "quantity": 2
                            }
                        ]
                        },
                        {
                        "id": "37310",
                        "description": "1 giường cỡ queen",
                        "configurations": [
                            {
                            "size": "Queen",
                            "type": "QueenBed",
                            "quantity": 1
                            }
                        ]
                        }
                    ],
                    "cancelPenalties": [],
                    "paxPrice": [
                        {
                        "paxInfo": {
                            "adultQuantity": 2,
                            "childQuantity": 0,
                            "infantQuantity": 0,
                            "childAges": []
                        },
                        "nightPrices": [
                            {
                            "nightKey": "0",
                            "nightPriceDetails": [
                                {
                                "name": "base_rate",
                                "value": 1468144.0,
                                "valueByHotelCurrency": "1468144.0 VND"
                                },
                                {
                                "name": "tax_and_service_fee",
                                "value": 227563.0,
                                "valueByHotelCurrency": "227563.0 VND"
                                }
                            ]
                            }
                        ]
                        }
                    ],
                    "totalPrice": 1695707.0,
                    "totalPriceByHotelCurrency": 1695707.0,
                    "taxAndFees": 227563.0,
                    "fees": {},
                    "promoDescription": "Tiết kiệm 30%",
                    "cancelFreeBeforeDate": "",
                    "meals": []
                    },
                    {
                    "ratePlanId": "209445835",
                    "ratePlanName": "",
                    "totalRooms": 10,
                    "breakfastIncluded": true,
                    "refundable": true,
                    "cancelFree": true,
                    "basePrice": 1468144.0,
                    "promo": true,
                    "basePriceBeforePromo": 2097349.0,
                    "amenities": [
                        {
                        "id": "2205",
                        "name": "Bữa sáng buffet",
                        "value": "",
                        "group": ""
                        },
                        {
                        "id": "1073742786",
                        "name": "Bữa sáng miễn phí",
                        "value": "",
                        "group": ""
                        },
                        {
                        "id": "2109",
                        "name": "Đậu xe miễn phí",
                        "value": "",
                        "group": ""
                        },
                        {
                        "id": "2192",
                        "name": "Wifi miễn phí",
                        "value": "",
                        "group": ""
                        }
                    ],
                    "bedGroups": [
                        {
                        "id": "37341",
                        "description": "2 giường đơn",
                        "configurations": [
                            {
                            "size": "Twin",
                            "type": "TwinBed",
                            "quantity": 2
                            }
                        ]
                        },
                        {
                        "id": "37310",
                        "description": "1 giường cỡ queen",
                        "configurations": [
                            {
                            "size": "Queen",
                            "type": "QueenBed",
                            "quantity": 1
                            }
                        ]
                        }
                    ],
                    "cancelPenalties": [
                        {
                        "startDate": "2021-07-09T18:00:00.000+07:00",
                        "endDate": "2021-07-23T18:00:00.000+07:00",
                        "type": "PERCENT",
                        "currency": "VND",
                        "percent": "100%",
                        "nights": "",
                        "amount": "",
                        "description": ""
                        }
                    ],
                    "paxPrice": [
                        {
                        "paxInfo": {
                            "adultQuantity": 2,
                            "childQuantity": 0,
                            "infantQuantity": 0,
                            "childAges": []
                        },
                        "nightPrices": [
                            {
                            "nightKey": "0",
                            "nightPriceDetails": [
                                {
                                "name": "base_rate",
                                "value": 1468144.0,
                                "valueByHotelCurrency": "1468144.0 VND"
                                },
                                {
                                "name": "tax_and_service_fee",
                                "value": 227563.0,
                                "valueByHotelCurrency": "227563.0 VND"
                                }
                            ]
                            }
                        ]
                        }
                    ],
                    "totalPrice": 1695707.0,
                    "totalPriceByHotelCurrency": 1695707.0,
                    "taxAndFees": 227563.0,
                    "fees": {},
                    "promoDescription": "Tiết kiệm 30%",
                    "cancelFreeBeforeDate": "2021-07-09T00:00:00+07:00",
                    "meals": []
                    }
                ],
                "bedGroupStatics": [
                    {
                    "id": "37341",
                    "name": "2 giường đơn",
                    "value": ""
                    },
                    {
                    "id": "37310",
                    "name": "1 giường cỡ queen",
                    "value": ""
                    }
                ],
                "views": [
                    {
                    "id": "4185",
                    "name": "Quang cảnh vườn",
                    "value": ""
                    },
                    {
                    "id": "4146",
                    "name": "Quang cảnh sân",
                    "value": ""
                    }
                ],
                "occupancyAllowed": {
                    "roomMaxAllowed": {
                    "total": 2,
                    "children": 1,
                    "adult": 2
                    },
                    "roomAgeCategories": [
                    {
                        "id": "",
                        "name": "ChildAgeA",
                        "value": "3"
                    },
                    {
                        "id": "",
                        "name": "Infant",
                        "value": "0"
                    },
                    {
                        "id": "",
                        "name": "Adult",
                        "value": "10"
                    }
                    ]
                },
                "amenities": [
                    {
                    "id": "2026",
                    "name": "Bàn",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "2180",
                    "name": "Máy sấy tóc (theo yêu cầu)",
                    "value": "",
                    "group": "BATHROOM"
                    },
                    {
                    "id": "2162",
                    "name": "Dép đi trong nhà",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "2183",
                    "name": "Buồng tắm vòi sen/bồn tắm kết hợp",
                    "value": "",
                    "group": "BATHROOM"
                    },
                    {
                    "id": "141",
                    "name": "Phòng tắm riêng",
                    "value": "",
                    "group": "BATHROOM"
                    },
                    {
                    "id": "142",
                    "name": "Áo choàng tắm",
                    "value": "",
                    "group": "BATHROOM"
                    },
                    {
                    "id": "1073743929",
                    "name": "Không có bộ trải giường",
                    "value": "",
                    "group": "BEDROOM"
                    },
                    {
                    "id": "2015",
                    "name": "Dịch vụ phòng (24 giờ)",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "2575",
                    "name": "TV LCD",
                    "value": "",
                    "group": "ENTERTAINMENT"
                    },
                    {
                    "id": "2057",
                    "name": "Nước đóng chai miễn phí",
                    "value": "",
                    "group": "FOOD_AND_DRINK"
                    },
                    {
                    "id": "143",
                    "name": "Đồ dùng nhà tắm miễn phí",
                    "value": "",
                    "group": "BATHROOM"
                    },
                    {
                    "id": "1",
                    "name": "Máy điều hòa",
                    "value": "",
                    "group": "BEDROOM"
                    },
                    {
                    "id": "146",
                    "name": "Két an toàn tại phòng",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "2031",
                    "name": "Báo các ngày trong tuần miễn phí",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "131",
                    "name": "Minibar",
                    "value": "",
                    "group": "FOOD_AND_DRINK"
                    },
                    {
                    "id": "132",
                    "name": "Dụng cụ pha cà phê/trà",
                    "value": "",
                    "group": "FOOD_AND_DRINK"
                    },
                    {
                    "id": "133",
                    "name": "Dọn phòng hàng ngày",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "2403",
                    "name": "Wifi miễn phí",
                    "value": "",
                    "group": "INTERNET"
                    },
                    {
                    "id": "2402",
                    "name": "HDTV",
                    "value": "",
                    "group": "ENTERTAINMENT"
                    },
                    {
                    "id": "6176",
                    "name": "Không hút thuốc",
                    "value": "",
                    "group": "SMOKING"
                    },
                    {
                    "id": "26",
                    "name": "TV",
                    "value": "",
                    "group": "ENTERTAINMENT"
                    },
                    {
                    "id": "1073745067",
                    "name": "Không có bộ trải giường",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "2056",
                    "name": "Dịch vụ dọn phòng buổi tối",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "2396",
                    "name": "Dịch vụ truyền hình vệ tinh",
                    "value": "",
                    "group": "ENTERTAINMENT"
                    },
                    {
                    "id": "2571",
                    "name": "Nệm có lớp đệm bông",
                    "value": "",
                    "group": "BEDROOM"
                    }
                ]
                },
                {
                "id": "437391",
                "name": "Opera View Room",
                "descriptions": [
                    {
                    "id": "1",
                    "name": "overview",
                    "value": "<p><strong>1 giường cỡ queen hoặc 2 giường đơn</strong></p><p>Phòng 40 mét vuông, hiên với quang cảnh thành phố</p><br/><p><b>Internet</b> - Wifi miễn phí <br /> <p><b>Giải trí</b> - TV LCD 46 inch với các kênh truyền hình cáp</p><p><b>Ăn uống</b> - Dụng cụ pha cà phê/trà, minibar, dịch vụ phòng 24 giờ và nước đóng chai miễn phí</p> <p><b>Giấc ngủ</b> - Giường đệm bông</p> <p><b>Phòng tắm</b> - Phòng tắm riêng với vòi sen/bồn tắm kết hợp, áo choàng tắm và dép đi trong nhà</p><p><b>Tiện nghi</b> - Két an toàn, báo miễn phí các ngày trong tuần và bàn</p><p><b>Tiện nghi</b> - Máy điều hòa nhiệt độ và dịch vụ dọn phòng hàng ngày</p><p><b>Thông tin cần biết</b> - Không có bộ trải giường</p> <p>Hút thuốc và không hút thuốc</p>"
                    }
                ],
                "images": [
                    {
                    "caption": "Phòng",
                    "position": 1,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/03f49af2_z.jpg"
                    },
                    {
                    "caption": "Phòng",
                    "position": 2,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/7563f797_z.jpg"
                    },
                    {
                    "caption": "Phòng",
                    "position": 3,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/c7d3697b_z.jpg"
                    },
                    {
                    "caption": "Phòng",
                    "position": 4,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/9b74d7d1_z.jpg"
                    },
                    {
                    "caption": "Khu phòng khách",
                    "position": 5,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/cf00f0ba_z.jpg"
                    },
                    {
                    "caption": "Ban công",
                    "position": 6,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/97d39dd7_z.jpg"
                    },
                    {
                    "caption": "Quang cảnh từ phòng",
                    "position": 7,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/e5a9e6ab_z.jpg"
                    },
                    {
                    "caption": "Phòng tắm",
                    "position": 8,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/891630e3_z.jpg"
                    },
                    {
                    "caption": "Tiện nghi phòng tắm",
                    "position": 9,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/ad72ed9e_z.jpg"
                    }
                ],
                "roomArea": {
                    "squareMeters": 40,
                    "squareFeet": 431
                },
                "ratePlans": [
                    {
                    "ratePlanId": "209445859",
                    "ratePlanName": "",
                    "totalRooms": 10,
                    "breakfastIncluded": true,
                    "refundable": true,
                    "cancelFree": true,
                    "basePrice": 1649915.0,
                    "promo": true,
                    "basePriceBeforePromo": 2357021.0,
                    "amenities": [
                        {
                        "id": "2205",
                        "name": "Bữa sáng buffet",
                        "value": "",
                        "group": ""
                        },
                        {
                        "id": "1073742786",
                        "name": "Bữa sáng miễn phí",
                        "value": "",
                        "group": ""
                        },
                        {
                        "id": "2109",
                        "name": "Đậu xe miễn phí",
                        "value": "",
                        "group": ""
                        },
                        {
                        "id": "2192",
                        "name": "Wifi miễn phí",
                        "value": "",
                        "group": ""
                        }
                    ],
                    "bedGroups": [
                        {
                        "id": "37341",
                        "description": "2 giường đơn",
                        "configurations": [
                            {
                            "size": "Twin",
                            "type": "TwinBed",
                            "quantity": 2
                            }
                        ]
                        },
                        {
                        "id": "37310",
                        "description": "1 giường cỡ queen",
                        "configurations": [
                            {
                            "size": "Queen",
                            "type": "QueenBed",
                            "quantity": 1
                            }
                        ]
                        }
                    ],
                    "cancelPenalties": [
                        {
                        "startDate": "2021-07-20T18:00:00.000+07:00",
                        "endDate": "2021-07-23T18:00:00.000+07:00",
                        "type": "NIGHTS",
                        "currency": "VND",
                        "percent": "",
                        "nights": "1.0",
                        "amount": "",
                        "description": ""
                        }
                    ],
                    "paxPrice": [
                        {
                        "paxInfo": {
                            "adultQuantity": 2,
                            "childQuantity": 0,
                            "infantQuantity": 0,
                            "childAges": []
                        },
                        "nightPrices": [
                            {
                            "nightKey": "0",
                            "nightPriceDetails": [
                                {
                                "name": "base_rate",
                                "value": 1649915.0,
                                "valueByHotelCurrency": "1649915.0 VND"
                                },
                                {
                                "name": "tax_and_service_fee",
                                "value": 255737.0,
                                "valueByHotelCurrency": "255737.0 VND"
                                }
                            ]
                            }
                        ]
                        }
                    ],
                    "totalPrice": 1905652.0,
                    "totalPriceByHotelCurrency": 1905652.0,
                    "taxAndFees": 255737.0,
                    "fees": {},
                    "promoDescription": "Tiết kiệm 30%",
                    "cancelFreeBeforeDate": "2021-07-20T00:00:00+07:00",
                    "meals": []
                    }
                ],
                "bedGroupStatics": [
                    {
                    "id": "37341",
                    "name": "2 giường đơn",
                    "value": ""
                    },
                    {
                    "id": "37310",
                    "name": "1 giường cỡ queen",
                    "value": ""
                    }
                ],
                "views": [
                    {
                    "id": "4134",
                    "name": "Quang cảnh thành phố",
                    "value": ""
                    }
                ],
                "occupancyAllowed": {
                    "roomMaxAllowed": {
                    "total": 3,
                    "children": 2,
                    "adult": 3
                    },
                    "roomAgeCategories": [
                    {
                        "id": "",
                        "name": "ChildAgeA",
                        "value": "3"
                    },
                    {
                        "id": "",
                        "name": "Infant",
                        "value": "0"
                    },
                    {
                        "id": "",
                        "name": "Adult",
                        "value": "10"
                    }
                    ]
                },
                "amenities": [
                    {
                    "id": "2180",
                    "name": "Máy sấy tóc (theo yêu cầu)",
                    "value": "",
                    "group": "BATHROOM"
                    },
                    {
                    "id": "2162",
                    "name": "Dép đi trong nhà",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "2183",
                    "name": "Buồng tắm vòi sen/bồn tắm kết hợp",
                    "value": "",
                    "group": "BATHROOM"
                    },
                    {
                    "id": "141",
                    "name": "Phòng tắm riêng",
                    "value": "",
                    "group": "BATHROOM"
                    },
                    {
                    "id": "142",
                    "name": "Áo choàng tắm",
                    "value": "",
                    "group": "BATHROOM"
                    },
                    {
                    "id": "143",
                    "name": "Đồ dùng nhà tắm miễn phí",
                    "value": "",
                    "group": "BATHROOM"
                    },
                    {
                    "id": "2015",
                    "name": "Dịch vụ phòng (24 giờ)",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "2575",
                    "name": "TV LCD",
                    "value": "",
                    "group": "ENTERTAINMENT"
                    },
                    {
                    "id": "2057",
                    "name": "Nước đóng chai miễn phí",
                    "value": "",
                    "group": "FOOD_AND_DRINK"
                    },
                    {
                    "id": "2398",
                    "name": "Dịch vụ truyền hình cáp",
                    "value": "",
                    "group": "ENTERTAINMENT"
                    },
                    {
                    "id": "1",
                    "name": "Máy điều hòa",
                    "value": "",
                    "group": "BEDROOM"
                    },
                    {
                    "id": "146",
                    "name": "Két an toàn tại phòng",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "1073743929",
                    "name": "Không có bộ trải giường",
                    "value": "",
                    "group": "BEDROOM"
                    },
                    {
                    "id": "131",
                    "name": "Minibar",
                    "value": "",
                    "group": "FOOD_AND_DRINK"
                    },
                    {
                    "id": "132",
                    "name": "Dụng cụ pha cà phê/trà",
                    "value": "",
                    "group": "FOOD_AND_DRINK"
                    },
                    {
                    "id": "133",
                    "name": "Dọn phòng hàng ngày",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "2403",
                    "name": "Wifi miễn phí",
                    "value": "",
                    "group": "INTERNET"
                    },
                    {
                    "id": "2402",
                    "name": "HDTV",
                    "value": "",
                    "group": "ENTERTAINMENT"
                    },
                    {
                    "id": "2026",
                    "name": "Bàn",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "26",
                    "name": "TV",
                    "value": "",
                    "group": "ENTERTAINMENT"
                    },
                    {
                    "id": "1073745067",
                    "name": "Không có bộ trải giường",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "6213",
                    "name": "Hút thuốc và không hút thuốc",
                    "value": "",
                    "group": "SMOKING"
                    },
                    {
                    "id": "2032",
                    "name": "Sân trong",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "2571",
                    "name": "Nệm có lớp đệm bông",
                    "value": "",
                    "group": "BEDROOM"
                    },
                    {
                    "id": "2031",
                    "name": "Báo các ngày trong tuần miễn phí",
                    "value": "",
                    "group": "OTHER"
                    }
                ]
                },
                {
                "id": "349133",
                "name": "Phòng Deluxe, Quang cảnh thành phố",
                "descriptions": [
                    {
                    "id": "1",
                    "name": "overview",
                    "value": "<p><strong>1 giường đôi hoặc 2 giường đơn</strong></p><p>Phòng 45 mét vuông với quang cảnh thành phố</p><br/><p><b>Bố trí</b> - Phòng khách và khu tiếp khách tách biệt</p> <p><b>Internet</b> - Wifi miễn phí <br /> <p><b>Giải trí</b> - TV LCD 46 inch với các kênh truyền hình cáp</p><p><b>Ăn uống</b> - Dụng cụ pha cà phê/trà, minibar, dịch vụ phòng 24 giờ và nước đóng chai miễn phí</p> <p><b>Phòng tắm</b> - Phòng tắm riêng với vòi sen/bồn tắm kết hợp, áo choàng tắm và dép đi trong nhà</p><p><b>Tiện nghi</b> - Két an toàn, báo miễn phí các ngày trong tuần và bàn</p><p><b>Tiện nghi</b> - Máy điều hòa nhiệt độ và dịch vụ dọn phòng hàng ngày</p><p><b>Thông tin cần biết</b> - Không có bộ trải giường</p> <p>Hút thuốc và không hút thuốc</p>"
                    }
                ],
                "images": [
                    {
                    "caption": "Phòng",
                    "position": 1,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/c7d3697b_z.jpg"
                    },
                    {
                    "caption": "Phòng",
                    "position": 2,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/cf01e333_z.jpg"
                    },
                    {
                    "caption": "Phòng",
                    "position": 3,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/2bd2576e_z.jpg"
                    },
                    {
                    "caption": "Quang cảnh từ phòng",
                    "position": 4,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/6bea4654_z.jpg"
                    },
                    {
                    "caption": "Phòng tắm",
                    "position": 5,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/ee07c9cf_z.jpg"
                    },
                    {
                    "caption": "Tiện nghi phòng tắm",
                    "position": 6,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/ae3f3563_z.jpg"
                    }
                ],
                "roomArea": {
                    "squareMeters": 45,
                    "squareFeet": 484
                },
                "ratePlans": [
                    {
                    "ratePlanId": "209445850",
                    "ratePlanName": "",
                    "totalRooms": 10,
                    "breakfastIncluded": true,
                    "refundable": true,
                    "cancelFree": true,
                    "basePrice": 1649915.0,
                    "promo": true,
                    "basePriceBeforePromo": 2357021.0,
                    "amenities": [
                        {
                        "id": "2205",
                        "name": "Bữa sáng buffet",
                        "value": "",
                        "group": ""
                        },
                        {
                        "id": "1073742786",
                        "name": "Bữa sáng miễn phí",
                        "value": "",
                        "group": ""
                        },
                        {
                        "id": "2109",
                        "name": "Đậu xe miễn phí",
                        "value": "",
                        "group": ""
                        },
                        {
                        "id": "2192",
                        "name": "Wifi miễn phí",
                        "value": "",
                        "group": ""
                        }
                    ],
                    "bedGroups": [
                        {
                        "id": "37341",
                        "description": "2 giường đơn",
                        "configurations": [
                            {
                            "size": "Twin",
                            "type": "TwinBed",
                            "quantity": 2
                            }
                        ]
                        },
                        {
                        "id": "37316",
                        "description": "1 giường đôi",
                        "configurations": [
                            {
                            "size": "Full",
                            "type": "FullBed",
                            "quantity": 1
                            }
                        ]
                        }
                    ],
                    "cancelPenalties": [
                        {
                        "startDate": "2021-07-09T18:00:00.000+07:00",
                        "endDate": "2021-07-23T18:00:00.000+07:00",
                        "type": "PERCENT",
                        "currency": "VND",
                        "percent": "100%",
                        "nights": "",
                        "amount": "",
                        "description": ""
                        }
                    ],
                    "paxPrice": [
                        {
                        "paxInfo": {
                            "adultQuantity": 2,
                            "childQuantity": 0,
                            "infantQuantity": 0,
                            "childAges": []
                        },
                        "nightPrices": [
                            {
                            "nightKey": "0",
                            "nightPriceDetails": [
                                {
                                "name": "base_rate",
                                "value": 1649915.0,
                                "valueByHotelCurrency": "1649915.0 VND"
                                },
                                {
                                "name": "tax_and_service_fee",
                                "value": 255737.0,
                                "valueByHotelCurrency": "255737.0 VND"
                                }
                            ]
                            }
                        ]
                        }
                    ],
                    "totalPrice": 1905652.0,
                    "totalPriceByHotelCurrency": 1905652.0,
                    "taxAndFees": 255737.0,
                    "fees": {},
                    "promoDescription": "Tiết kiệm 30%",
                    "cancelFreeBeforeDate": "2021-07-09T00:00:00+07:00",
                    "meals": []
                    },
                    {
                    "ratePlanId": "232235390",
                    "ratePlanName": "",
                    "totalRooms": 10,
                    "breakfastIncluded": true,
                    "refundable": true,
                    "cancelFree": true,
                    "basePrice": 1649915.0,
                    "promo": true,
                    "basePriceBeforePromo": 2357021.0,
                    "amenities": [
                        {
                        "id": "1073742551",
                        "name": "Đồ uống miễn phí chào đón khách",
                        "value": "",
                        "group": ""
                        },
                        {
                        "id": "1073742786",
                        "name": "Bữa sáng miễn phí",
                        "value": "",
                        "group": ""
                        },
                        {
                        "id": "2192",
                        "name": "Wifi miễn phí",
                        "value": "",
                        "group": ""
                        }
                    ],
                    "bedGroups": [
                        {
                        "id": "37341",
                        "description": "2 giường đơn",
                        "configurations": [
                            {
                            "size": "Twin",
                            "type": "TwinBed",
                            "quantity": 2
                            }
                        ]
                        },
                        {
                        "id": "37316",
                        "description": "1 giường đôi",
                        "configurations": [
                            {
                            "size": "Full",
                            "type": "FullBed",
                            "quantity": 1
                            }
                        ]
                        }
                    ],
                    "cancelPenalties": [
                        {
                        "startDate": "2021-07-22T18:00:00.000+07:00",
                        "endDate": "2021-07-23T18:00:00.000+07:00",
                        "type": "PERCENT",
                        "currency": "VND",
                        "percent": "100%",
                        "nights": "",
                        "amount": "",
                        "description": ""
                        }
                    ],
                    "paxPrice": [
                        {
                        "paxInfo": {
                            "adultQuantity": 2,
                            "childQuantity": 0,
                            "infantQuantity": 0,
                            "childAges": []
                        },
                        "nightPrices": [
                            {
                            "nightKey": "0",
                            "nightPriceDetails": [
                                {
                                "name": "base_rate",
                                "value": 1649915.0,
                                "valueByHotelCurrency": "1649915.0 VND"
                                },
                                {
                                "name": "tax_and_service_fee",
                                "value": 255737.0,
                                "valueByHotelCurrency": "255737.0 VND"
                                }
                            ]
                            }
                        ]
                        }
                    ],
                    "totalPrice": 1905652.0,
                    "totalPriceByHotelCurrency": 1905652.0,
                    "taxAndFees": 255737.0,
                    "fees": {},
                    "promoDescription": "Tiết kiệm 30%",
                    "cancelFreeBeforeDate": "2021-07-22T00:00:00+07:00",
                    "meals": []
                    }
                ],
                "bedGroupStatics": [
                    {
                    "id": "37341",
                    "name": "2 giường đơn",
                    "value": ""
                    },
                    {
                    "id": "37316",
                    "name": "1 giường đôi",
                    "value": ""
                    }
                ],
                "views": [
                    {
                    "id": "4134",
                    "name": "Quang cảnh thành phố",
                    "value": ""
                    }
                ],
                "occupancyAllowed": {
                    "roomMaxAllowed": {
                    "total": 3,
                    "children": 2,
                    "adult": 3
                    },
                    "roomAgeCategories": [
                    {
                        "id": "",
                        "name": "ChildAgeA",
                        "value": "3"
                    },
                    {
                        "id": "",
                        "name": "Infant",
                        "value": "0"
                    },
                    {
                        "id": "",
                        "name": "Adult",
                        "value": "10"
                    }
                    ]
                },
                "amenities": [
                    {
                    "id": "2183",
                    "name": "Buồng tắm vòi sen/bồn tắm kết hợp",
                    "value": "",
                    "group": "BATHROOM"
                    },
                    {
                    "id": "141",
                    "name": "Phòng tắm riêng",
                    "value": "",
                    "group": "BATHROOM"
                    },
                    {
                    "id": "142",
                    "name": "Áo choàng tắm",
                    "value": "",
                    "group": "BATHROOM"
                    },
                    {
                    "id": "143",
                    "name": "Đồ dùng nhà tắm miễn phí",
                    "value": "",
                    "group": "BATHROOM"
                    },
                    {
                    "id": "1",
                    "name": "Máy điều hòa",
                    "value": "",
                    "group": "BEDROOM"
                    },
                    {
                    "id": "146",
                    "name": "Két an toàn tại phòng",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "1073743929",
                    "name": "Không có bộ trải giường",
                    "value": "",
                    "group": "BEDROOM"
                    },
                    {
                    "id": "2015",
                    "name": "Dịch vụ phòng (24 giờ)",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "2037",
                    "name": "Khu tiếp khách riêng",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "2575",
                    "name": "TV LCD",
                    "value": "",
                    "group": "ENTERTAINMENT"
                    },
                    {
                    "id": "2057",
                    "name": "Nước đóng chai miễn phí",
                    "value": "",
                    "group": "FOOD_AND_DRINK"
                    },
                    {
                    "id": "2398",
                    "name": "Dịch vụ truyền hình cáp",
                    "value": "",
                    "group": "ENTERTAINMENT"
                    },
                    {
                    "id": "133",
                    "name": "Dọn phòng hàng ngày",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "2403",
                    "name": "Wifi miễn phí",
                    "value": "",
                    "group": "INTERNET"
                    },
                    {
                    "id": "2402",
                    "name": "HDTV",
                    "value": "",
                    "group": "ENTERTAINMENT"
                    },
                    {
                    "id": "2026",
                    "name": "Bàn",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "2180",
                    "name": "Máy sấy tóc (theo yêu cầu)",
                    "value": "",
                    "group": "BATHROOM"
                    },
                    {
                    "id": "2162",
                    "name": "Dép đi trong nhà",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "26",
                    "name": "TV",
                    "value": "",
                    "group": "ENTERTAINMENT"
                    },
                    {
                    "id": "1073745067",
                    "name": "Không có bộ trải giường",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "6213",
                    "name": "Hút thuốc và không hút thuốc",
                    "value": "",
                    "group": "SMOKING"
                    },
                    {
                    "id": "2031",
                    "name": "Báo các ngày trong tuần miễn phí",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "131",
                    "name": "Minibar",
                    "value": "",
                    "group": "FOOD_AND_DRINK"
                    },
                    {
                    "id": "132",
                    "name": "Dụng cụ pha cà phê/trà",
                    "value": "",
                    "group": "FOOD_AND_DRINK"
                    }
                ]
                },
                {
                "id": "349134",
                "name": "Opera View Suite",
                "descriptions": [
                    {
                    "id": "1",
                    "name": "overview",
                    "value": "<p><strong>1 giường cỡ queen hoặc 2 giường đơn</strong></p><p>Phòng 55 mét vuông, ban công với quang cảnh thành phố</p><br/><p><b>Bố trí</b> - Phòng khách và khu tiếp khách tách biệt</p> <p><b>Internet</b> - Wifi miễn phí <br /> <p><b>Giải trí</b> - TV LCD với các kênh truyền hình vệ tinh</p><p><b>Ăn uống</b> - Dụng cụ pha cà phê/trà, minibar, dịch vụ phòng 24 giờ và nước đóng chai miễn phí</p> <p><b>Giấc ngủ</b> - Giường đệm bông</p> <p><b>Phòng tắm</b> - Phòng tắm riêng với vòi sen/bồn tắm kết hợp, áo choàng tắm và dép đi trong nhà</p><p><b>Tiện nghi</b> - Điện thoại, két an toàn và báo miễn phí các ngày trong tuần</p><p><b>Tiện nghi</b> - Hệ thống điều hòa nhiệt độ và dịch vụ dọn phòng hàng ngày</p><p><b>Thông tin cần biết</b> - Không có bộ trải giường</p> <p>Hút thuốc và không hút thuốc</p>"
                    }
                ],
                "images": [
                    {
                    "caption": "Phòng",
                    "position": 1,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/b6e21a19_z.jpg"
                    },
                    {
                    "caption": "Phòng",
                    "position": 2,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/394e4ca3_z.jpg"
                    },
                    {
                    "caption": "Phòng",
                    "position": 3,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/d7bc598e_z.jpg"
                    },
                    {
                    "caption": "Phòng",
                    "position": 4,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/c7d3697b_z.jpg"
                    },
                    {
                    "caption": "Ban công",
                    "position": 5,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/5b71c73f_z.jpg"
                    },
                    {
                    "caption": "Quang cảnh từ phòng",
                    "position": 6,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/a90b6f48_z.jpg"
                    },
                    {
                    "caption": "Phòng tắm",
                    "position": 7,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/891630e3_z.jpg"
                    }
                ],
                "roomArea": {
                    "squareMeters": 55,
                    "squareFeet": 592
                },
                "ratePlans": [
                    {
                    "ratePlanId": "209445865",
                    "ratePlanName": "",
                    "totalRooms": 5,
                    "breakfastIncluded": true,
                    "refundable": true,
                    "cancelFree": true,
                    "basePrice": 2167261.0,
                    "promo": true,
                    "basePriceBeforePromo": 3096087.0,
                    "amenities": [
                        {
                        "id": "2205",
                        "name": "Bữa sáng buffet",
                        "value": "",
                        "group": ""
                        },
                        {
                        "id": "1073742786",
                        "name": "Bữa sáng miễn phí",
                        "value": "",
                        "group": ""
                        },
                        {
                        "id": "2109",
                        "name": "Đậu xe miễn phí",
                        "value": "",
                        "group": ""
                        },
                        {
                        "id": "2192",
                        "name": "Wifi miễn phí",
                        "value": "",
                        "group": ""
                        }
                    ],
                    "bedGroups": [
                        {
                        "id": "37341",
                        "description": "2 giường đơn",
                        "configurations": [
                            {
                            "size": "Twin",
                            "type": "TwinBed",
                            "quantity": 2
                            }
                        ]
                        },
                        {
                        "id": "37310",
                        "description": "1 giường cỡ queen",
                        "configurations": [
                            {
                            "size": "Queen",
                            "type": "QueenBed",
                            "quantity": 1
                            }
                        ]
                        }
                    ],
                    "cancelPenalties": [
                        {
                        "startDate": "2021-07-20T18:00:00.000+07:00",
                        "endDate": "2021-07-23T18:00:00.000+07:00",
                        "type": "NIGHTS",
                        "currency": "VND",
                        "percent": "",
                        "nights": "1.0",
                        "amount": "",
                        "description": ""
                        }
                    ],
                    "paxPrice": [
                        {
                        "paxInfo": {
                            "adultQuantity": 2,
                            "childQuantity": 0,
                            "infantQuantity": 0,
                            "childAges": []
                        },
                        "nightPrices": [
                            {
                            "nightKey": "0",
                            "nightPriceDetails": [
                                {
                                "name": "base_rate",
                                "value": 2167261.0,
                                "valueByHotelCurrency": "2167261.0 VND"
                                },
                                {
                                "name": "tax_and_service_fee",
                                "value": 335925.0,
                                "valueByHotelCurrency": "335925.0 VND"
                                }
                            ]
                            }
                        ]
                        }
                    ],
                    "totalPrice": 2503186.0,
                    "totalPriceByHotelCurrency": 2503186.0,
                    "taxAndFees": 335925.0,
                    "fees": {},
                    "promoDescription": "Tiết kiệm 30%",
                    "cancelFreeBeforeDate": "2021-07-20T00:00:00+07:00",
                    "meals": []
                    }
                ],
                "bedGroupStatics": [
                    {
                    "id": "37341",
                    "name": "2 giường đơn",
                    "value": ""
                    },
                    {
                    "id": "37310",
                    "name": "1 giường cỡ queen",
                    "value": ""
                    }
                ],
                "views": [
                    {
                    "id": "4134",
                    "name": "Quang cảnh thành phố",
                    "value": ""
                    }
                ],
                "occupancyAllowed": {
                    "roomMaxAllowed": {
                    "total": 3,
                    "children": 2,
                    "adult": 3
                    },
                    "roomAgeCategories": [
                    {
                        "id": "",
                        "name": "ChildAgeA",
                        "value": "3"
                    },
                    {
                        "id": "",
                        "name": "Infant",
                        "value": "0"
                    },
                    {
                        "id": "",
                        "name": "Adult",
                        "value": "10"
                    }
                    ]
                },
                "amenities": [
                    {
                    "id": "318",
                    "name": "Ban công",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "2180",
                    "name": "Máy sấy tóc (theo yêu cầu)",
                    "value": "",
                    "group": "BATHROOM"
                    },
                    {
                    "id": "2162",
                    "name": "Dép đi trong nhà",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "2183",
                    "name": "Buồng tắm vòi sen/bồn tắm kết hợp",
                    "value": "",
                    "group": "BATHROOM"
                    },
                    {
                    "id": "141",
                    "name": "Phòng tắm riêng",
                    "value": "",
                    "group": "BATHROOM"
                    },
                    {
                    "id": "142",
                    "name": "Áo choàng tắm",
                    "value": "",
                    "group": "BATHROOM"
                    },
                    {
                    "id": "143",
                    "name": "Đồ dùng nhà tắm miễn phí",
                    "value": "",
                    "group": "BATHROOM"
                    },
                    {
                    "id": "1",
                    "name": "Máy điều hòa",
                    "value": "",
                    "group": "BEDROOM"
                    },
                    {
                    "id": "146",
                    "name": "Két an toàn tại phòng",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "1073743929",
                    "name": "Không có bộ trải giường",
                    "value": "",
                    "group": "BEDROOM"
                    },
                    {
                    "id": "2015",
                    "name": "Dịch vụ phòng (24 giờ)",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "2037",
                    "name": "Khu tiếp khách riêng",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "2575",
                    "name": "TV LCD",
                    "value": "",
                    "group": "ENTERTAINMENT"
                    },
                    {
                    "id": "2057",
                    "name": "Nước đóng chai miễn phí",
                    "value": "",
                    "group": "FOOD_AND_DRINK"
                    },
                    {
                    "id": "131",
                    "name": "Minibar",
                    "value": "",
                    "group": "FOOD_AND_DRINK"
                    },
                    {
                    "id": "132",
                    "name": "Dụng cụ pha cà phê/trà",
                    "value": "",
                    "group": "FOOD_AND_DRINK"
                    },
                    {
                    "id": "133",
                    "name": "Dọn phòng hàng ngày",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "2403",
                    "name": "Wifi miễn phí",
                    "value": "",
                    "group": "INTERNET"
                    },
                    {
                    "id": "2402",
                    "name": "HDTV",
                    "value": "",
                    "group": "ENTERTAINMENT"
                    },
                    {
                    "id": "136",
                    "name": "Điện thoại",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "2026",
                    "name": "Bàn",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "26",
                    "name": "TV",
                    "value": "",
                    "group": "ENTERTAINMENT"
                    },
                    {
                    "id": "1073745067",
                    "name": "Không có bộ trải giường",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "6213",
                    "name": "Hút thuốc và không hút thuốc",
                    "value": "",
                    "group": "SMOKING"
                    },
                    {
                    "id": "2396",
                    "name": "Dịch vụ truyền hình vệ tinh",
                    "value": "",
                    "group": "ENTERTAINMENT"
                    },
                    {
                    "id": "2571",
                    "name": "Nệm có lớp đệm bông",
                    "value": "",
                    "group": "BEDROOM"
                    },
                    {
                    "id": "2031",
                    "name": "Báo các ngày trong tuần miễn phí",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "2030",
                    "name": "Hệ thống điều hòa tại phòng (máy điều hòa)",
                    "value": "",
                    "group": "BEDROOM"
                    }
                ]
                },
                {
                "id": "201866848",
                "name": "Phòng (Heritage )",
                "descriptions": [
                    {
                    "id": "1",
                    "name": "overview",
                    "value": "<p><strong>1 giường cỡ queen hoặc 2 giường đơn</strong></p><p>Phòng 45 mét vuông với quang cảnh thành phố</p><br/><p><b>Bố trí</b> - phòng ngủ, phòng khách riêng và khu tiếp khách tách biệt</p> <p><b>Internet</b> - Wifi miễn phí <br /> <p><b>Giải trí</b> - TV LCD 46 inch với các kênh truyền hình cáp</p><p><b>Ăn uống</b> - Dụng cụ pha cà phê/trà, minibar, dịch vụ phòng 24 giờ và nước đóng chai miễn phí</p> <p><b>Phòng tắm</b> - Phòng tắm riêng với vòi sen/bồn tắm kết hợp, áo choàng tắm và dép đi trong nhà</p><p><b>Tiện nghi</b> - Két an toàn, báo miễn phí các ngày trong tuần và bàn</p><p><b>Tiện nghi</b> - Máy điều hòa nhiệt độ và dịch vụ dọn phòng hàng ngày</p><p><b>Thông tin cần biết</b> - Không có bộ trải giường</p> <p>Không hút thuốc</p>"
                    }
                ],
                "images": [
                    {
                    "caption": "Phòng",
                    "position": 1,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/eb9050ee_z.jpg"
                    },
                    {
                    "caption": "Phòng",
                    "position": 2,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/e9786e7a_z.jpg"
                    },
                    {
                    "caption": "Phòng",
                    "position": 3,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/69a5669a_z.jpg"
                    },
                    {
                    "caption": "Phòng",
                    "position": 4,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/95edabdd_z.jpg"
                    },
                    {
                    "caption": "Phòng",
                    "position": 5,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/981d451d_z.jpg"
                    },
                    {
                    "caption": "Phòng",
                    "position": 6,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/e09b3e04_z.jpg"
                    },
                    {
                    "caption": "Phòng",
                    "position": 7,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/3e84b5ea_z.jpg"
                    },
                    {
                    "caption": "Phòng",
                    "position": 8,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/ca41955a_z.jpg"
                    },
                    {
                    "caption": "Quang cảnh từ phòng",
                    "position": 9,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/37a2958e_z.jpg"
                    },
                    {
                    "caption": "Phòng tắm",
                    "position": 10,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/69f7e479_z.jpg"
                    },
                    {
                    "caption": "Bồn tắm vòi sen trong phòng tắm",
                    "position": 11,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/e2792550_z.jpg"
                    },
                    {
                    "caption": "Tiện nghi phòng tắm",
                    "position": 12,
                    "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/3c87904a_z.jpg"
                    }
                ],
                "roomArea": {
                    "squareMeters": 45,
                    "squareFeet": 484
                },
                "ratePlans": [
                    {
                    "ratePlanId": "209445872",
                    "ratePlanName": "",
                    "totalRooms": 5,
                    "breakfastIncluded": true,
                    "refundable": true,
                    "cancelFree": true,
                    "basePrice": 2307084.0,
                    "promo": true,
                    "basePriceBeforePromo": 3295835.0,
                    "amenities": [
                        {
                        "id": "2205",
                        "name": "Bữa sáng buffet",
                        "value": "",
                        "group": ""
                        },
                        {
                        "id": "1073742786",
                        "name": "Bữa sáng miễn phí",
                        "value": "",
                        "group": ""
                        },
                        {
                        "id": "2109",
                        "name": "Đậu xe miễn phí",
                        "value": "",
                        "group": ""
                        },
                        {
                        "id": "2192",
                        "name": "Wifi miễn phí",
                        "value": "",
                        "group": ""
                        }
                    ],
                    "bedGroups": [
                        {
                        "id": "37341",
                        "description": "2 giường đơn",
                        "configurations": [
                            {
                            "size": "Twin",
                            "type": "TwinBed",
                            "quantity": 2
                            }
                        ]
                        },
                        {
                        "id": "37310",
                        "description": "1 giường cỡ queen",
                        "configurations": [
                            {
                            "size": "Queen",
                            "type": "QueenBed",
                            "quantity": 1
                            }
                        ]
                        }
                    ],
                    "cancelPenalties": [
                        {
                        "startDate": "2021-07-20T18:00:00.000+07:00",
                        "endDate": "2021-07-23T18:00:00.000+07:00",
                        "type": "NIGHTS",
                        "currency": "VND",
                        "percent": "",
                        "nights": "1.0",
                        "amount": "",
                        "description": ""
                        }
                    ],
                    "paxPrice": [
                        {
                        "paxInfo": {
                            "adultQuantity": 2,
                            "childQuantity": 0,
                            "infantQuantity": 0,
                            "childAges": []
                        },
                        "nightPrices": [
                            {
                            "nightKey": "0",
                            "nightPriceDetails": [
                                {
                                "name": "base_rate",
                                "value": 2307084.0,
                                "valueByHotelCurrency": "2307084.0 VND"
                                },
                                {
                                "name": "tax_and_service_fee",
                                "value": 357598.0,
                                "valueByHotelCurrency": "357598.0 VND"
                                }
                            ]
                            }
                        ]
                        }
                    ],
                    "totalPrice": 2664682.0,
                    "totalPriceByHotelCurrency": 2664682.0,
                    "taxAndFees": 357598.0,
                    "fees": {},
                    "promoDescription": "Tiết kiệm 30%",
                    "cancelFreeBeforeDate": "2021-07-20T00:00:00+07:00",
                    "meals": []
                    }
                ],
                "bedGroupStatics": [
                    {
                    "id": "37341",
                    "name": "2 giường đơn",
                    "value": ""
                    },
                    {
                    "id": "37310",
                    "name": "1 giường cỡ queen",
                    "value": ""
                    }
                ],
                "views": [
                    {
                    "id": "4134",
                    "name": "Quang cảnh thành phố",
                    "value": ""
                    }
                ],
                "occupancyAllowed": {
                    "roomMaxAllowed": {
                    "total": 2,
                    "children": 1,
                    "adult": 2
                    },
                    "roomAgeCategories": [
                    {
                        "id": "",
                        "name": "ChildAgeA",
                        "value": "3"
                    },
                    {
                        "id": "",
                        "name": "Infant",
                        "value": "0"
                    },
                    {
                        "id": "",
                        "name": "Adult",
                        "value": "10"
                    }
                    ]
                },
                "amenities": [
                    {
                    "id": "2183",
                    "name": "Buồng tắm vòi sen/bồn tắm kết hợp",
                    "value": "",
                    "group": "BATHROOM"
                    },
                    {
                    "id": "141",
                    "name": "Phòng tắm riêng",
                    "value": "",
                    "group": "BATHROOM"
                    },
                    {
                    "id": "142",
                    "name": "Áo choàng tắm",
                    "value": "",
                    "group": "BATHROOM"
                    },
                    {
                    "id": "143",
                    "name": "Đồ dùng nhà tắm miễn phí",
                    "value": "",
                    "group": "BATHROOM"
                    },
                    {
                    "id": "1",
                    "name": "Máy điều hòa",
                    "value": "",
                    "group": "BEDROOM"
                    },
                    {
                    "id": "146",
                    "name": "Két an toàn tại phòng",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "2575",
                    "name": "TV LCD",
                    "value": "",
                    "group": "ENTERTAINMENT"
                    },
                    {
                    "id": "2057",
                    "name": "Nước đóng chai miễn phí",
                    "value": "",
                    "group": "FOOD_AND_DRINK"
                    },
                    {
                    "id": "2398",
                    "name": "Dịch vụ truyền hình cáp",
                    "value": "",
                    "group": "ENTERTAINMENT"
                    },
                    {
                    "id": "4954",
                    "name": "Phòng ngủ riêng",
                    "value": "",
                    "group": "BEDROOM"
                    },
                    {
                    "id": "1073743929",
                    "name": "Không có bộ trải giường",
                    "value": "",
                    "group": "BEDROOM"
                    },
                    {
                    "id": "2015",
                    "name": "Dịch vụ phòng (24 giờ)",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "2037",
                    "name": "Khu tiếp khách riêng",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "133",
                    "name": "Dọn phòng hàng ngày",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "2403",
                    "name": "Wifi miễn phí",
                    "value": "",
                    "group": "INTERNET"
                    },
                    {
                    "id": "2402",
                    "name": "HDTV",
                    "value": "",
                    "group": "ENTERTAINMENT"
                    },
                    {
                    "id": "2026",
                    "name": "Bàn",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "2180",
                    "name": "Máy sấy tóc (theo yêu cầu)",
                    "value": "",
                    "group": "BATHROOM"
                    },
                    {
                    "id": "2162",
                    "name": "Dép đi trong nhà",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "6176",
                    "name": "Không hút thuốc",
                    "value": "",
                    "group": "SMOKING"
                    },
                    {
                    "id": "26",
                    "name": "TV",
                    "value": "",
                    "group": "ENTERTAINMENT"
                    },
                    {
                    "id": "1073745067",
                    "name": "Không có bộ trải giường",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "2031",
                    "name": "Báo các ngày trong tuần miễn phí",
                    "value": "",
                    "group": "OTHER"
                    },
                    {
                    "id": "131",
                    "name": "Minibar",
                    "value": "",
                    "group": "FOOD_AND_DRINK"
                    },
                    {
                    "id": "132",
                    "name": "Dụng cụ pha cà phê/trà",
                    "value": "",
                    "group": "FOOD_AND_DRINK"
                    }
                ]
                }
            ],
            "attributes": [],
            "spokenLanguage": [],
            "airportCode": "",
            "tags": []
            }
        },
        "duration": 0,
        "textMessage": null,
        "errors": null,
        "infos": null,
        "success": true
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

## 5. API Lấy danh sách khách sạn 

!!! info "GET: /api/v3/hotel/get-master-properties"
    Lấy danh sách thông tin cơ bản của khách sạn.

### Parameters
=== "Parameters"
    ???+ example "Parameters"
        - id `query` (String, optional)

            !!! quote "" 
            
                Mã định danh khách sạn 

        - language `query` (String, Required)

            !!! quote "" 
            
                Ngôn ngữ 

                - `vi` : Tiếng Việt 
                
                - `en`: Tiếng Anh 

        - lastModifiedDate `query` (String, optional)

            !!! quote "" 
            
                Ngày cập nhật  

        - pageNumber `query` (String, Optional)
            
            !!! quote "" 
                
                Trang số

        - pageSize `query` (String, Optional)
            
            !!! quote "" 
                
                Số phần tử trên trang

=== "Example"
    - Tìm kiếm theo ngày cập nhật 
    ```
    ?language=vi&lastModifiedDate=2021-09-10&pageNumber=0&pageSize=50
    ```

    - Tìm kiếm theo id 
    ```
    ?id=123&language=vi
    ```

### Response
#### Code 200
=== "Model" 
    ???+ example "Model"
        - result (FilterOptionsResult, optional)

            !!! quote ""
        
                Thông tin kết quả trả về 
        
            - masterProperties (Array[MasterProperty], optional),
            
                !!! quote "" 
                    
                    Danh sách thông tin khách sạn

                - id (Long, optional),
            
                    !!! quote "" 

                        Mã định danh  

                - propertyName (string, optional),
            
                    !!! quote "" 

                        Tên khách sạn 

                - address (Address, optional)
                
                    !!! quote "" 
                        
                        Thông tin địa chỉ khách sạn

                    - city (string, optional),
                    
                    !!! quote "" 
                        
                        Thành phố

                    - countryCode (string, optional),
                    
                        !!! quote "" 
                        
                            Mã quốc gia

                    - countryName (string, optional),
                    
                        !!! quote "" 
                        
                            Tên quốc gia

                    - lineOne (string, optional),
                    
                        !!! quote "" 
                        
                            Địa chỉ dòng 1

                    - lineTow (string, optional),
                    
                        !!! quote "" 
                        
                            Địa chỉ dòng 2

                    - postalCode (string, optional),
                    
                        !!! quote "" 
                        
                            Mã bưu điện

                    - stateProvinceCode (string, optional),
                    
                        !!! quote "" 
                        
                            Mã tỉnh thành

                    - stateProvinceName (string, optional)
            
                        !!! quote "" 

                            Tên tỉnh thành

                - propertyLocation (PropertyLocation, optional) = ['vi', 'en'],
                    
                    !!! quote "" 
                        
                        Vị trí toạ độ  

                    - longitude (string, optional),
                
                        !!! quote "" 
                            
                            Kinh độ 

                    - latitude (string, optional),
                
                        !!! quote "" 
                            
                            Vĩ độ 

                - activated (boolean, required),
                    
                    !!! quote "" 
        
                        Trạng thái `true`: hoạt động / `false`: không hoạt động  

                - legacyIds (Array[Long], optional),
                    
                    !!! quote "" 
        
                        Danh sách mã định danh cũ  

        - duration (integer, optional),
        - errors (Array[Error], optional),
        - infos (Array[Info], optional),
        - success (boolean, optional),
        - textMessage (string, optional)
=== "Example"
    ```json 
    {
        "result":
        {
            "masterProperties":
            [
                {
                    "id": 26,
                    "propertyName": "Khách sạn Mường Thanh Luxury Nhật Lệ",
                    "propertyAddress":
                    {
                        "lineOne": "121, Trương Pháp, Hải Thành, Thành phố Đồng Hới",
                        "lineTow": "",
                        "stateProvinceCode": "",
                        "stateProvinceName": "",
                        "postalCode": "47000",
                        "city": "Quang Binh",
                        "countryCode": "VN",
                        "countryName": "Vietnam"
                    },
                    "propertyLocation":
                    {
                        "longitude": "106.627343",
                        "latitude": "17.4866314"
                    },
                    "activated": true,
                    "legacyIds": null
                },
                {
                    "id": 25,
                    "propertyName": "Van Mieu I Hotel",
                    "propertyAddress":
                    {
                        "lineOne": "54B Quốc Tử Giám, Văn Miếu, Đống Đa",
                        "lineTow": "",
                        "stateProvinceCode": "",
                        "stateProvinceName": "",
                        "postalCode": "100000",
                        "city": "Hanoi",
                        "countryCode": "VN",
                        "countryName": "Vietnam"
                    },
                    "propertyLocation":
                    {
                        "longitude": "105.8371357",
                        "latitude": "21.0266163"
                    },
                    "activated": true,
                    "legacyIds": null
                },
                {
                    "id": 491,
                    "propertyName": "Poulo Condor Boutique Resort & Spa",
                    "propertyAddress":
                    {
                        "lineOne": "Bãi Vông, Cỏ Ống, TT. Côn Đảo, Huyện Côn Đảo, Tỉnh Bà Rịa Vũng Tàu\t\t\t\t\t\t",
                        "lineTow": "",
                        "stateProvinceCode": "",
                        "stateProvinceName": "",
                        "postalCode": "78000",
                        "city": "Ba Ria - Vung Tau",
                        "countryCode": "VN",
                        "countryName": "Vietnam"
                    },
                    "propertyLocation":
                    {
                        "longitude": "106.6357014",
                        "latitude": "8.7141538"
                    },
                    "activated": true,
                    "legacyIds": null
                }
            ],
            "pageResult":
            {
                "pageSize": 3,
                "pageNumber": 0,
                "totalPage": 206,
                "totalItems": 617
            }
        },
        "duration": 0,
        "textMessage": null,
        "errors": null,
        "infos": null,
        "success": true
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