# Document API Login

---

## 1. API Đăng nhập

!!! info "POST: /api/partner/login"
    Khởi tạo phiên làm việc mới cho người dùng B2B2C

    !!! note "Chú ý"
        Yêu cầu bảo mật: Mã hóa dữ liệu và kèm theo chữ ký điện tử

### Request Body 

=== "Model"
    ???+ example "Model"

        - key (string, required),

            !!! quote ""

                Key giải mã dữ liệu (đã được mã hóa). Cách thành lập tham khảo mục: [Mã hóa dữ liệu truyền và xác thực chữ ký điện tử](/dev-guide/#3-ma-hoa-du-lieu-truyen-va-xac-thuc-chu-ky-ien-tu)

        - data (string, required),

            !!! quote ""

                Dữ liệu kèm theo chữ ký điện tử (đã được mã hóa). Cách giải mã tham khảo mục: [Mã hóa dữ liệu truyền và xác thực chữ ký điện tử](/dev-guide/#3-ma-hoa-du-lieu-truyen-va-xac-thuc-chu-ky-ien-tu)

                *Signature data schema:*

                ``` 
                <access_code>|<user_id>
                ```    

                *Original data schema:*
                ```
                <access_code>|<user_id>|<signature>
                ```

                - access_code (String, required)

                    !!! quote ""

                        Access code do Gotadi cung cấp cho Đối tác.

                - user_id (String, required)

                    !!! quote ""

                        Mã định danh người dùng trên hệ thống của Đối tác.


=== "Example"
    ```json
    {
        "data": "string",
        "key": "string"
    }
    ```

### Response 
#### Code 200
> OK

=== "Model"
    ???+ example "Model"

        - key (String, required)

            !!! quote ""

                Key giải mã dữ liệu (đã được mã hóa). Cách giải mã tham khảo mục: [Mã hóa dữ liệu truyền và xác thực chữ ký điện tử](/dev-guide/#3-ma-hoa-du-lieu-truyen-va-xac-thuc-chu-ky-ien-tu)

        - data (String, required)

            !!! quote ""

                Dữ liệu kèm theo chữ ký điện tử (đã được mã hóa). Cách giải mã tham khảo mục: [Mã hóa dữ liệu truyền và xác thực chữ ký điện tử](/dev-guide/#3-ma-hoa-du-lieu-truyen-va-xac-thuc-chu-ky-ien-tu)

                *Signature data schema:*

                ``` 
                <access_code>|<error_code>
                ```    

                *Original data schema:*
                ```
                <jwt_token>|<error_code>|<signature>
                ```

                - access_code (String, required)

                    !!! quote ""

                        Access code do Gotadi cung cấp cho Đối tác.

                - error_code (String, required)

                    !!! quote ""

                        [Mã lỗi](/dev-guide/#7-ma-loi)

                - jwt_token (String, required)

                    !!! quote ""

                        token dùng để gọi api của gotadi
                        
=== "Example"
    ```json
    {
        "data": "string",
        "key": "string"
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


## 2. API Tạo Tài Khoản SubAgency

!!! info "POST: /api/partner/create-sub-agency"
    Tạo tài khoản mới cho người dùng B2B2C nếu tài khoản khi gọi API login trả về  Error_Code = 10

### Request Body 

=== "Model"
    ???+ example "Model"

        - userId (string, required),

            !!! quote ""

                Mã định danh người dùng trên hệ thống của Đối tác.

        - address (string, required),

            !!! quote ""

                Địa chỉ khách hàng

        - email (string, required),

            !!! quote ""

                Email khách hàng

        - city (string, required),

            !!! quote ""

                Thành phố
        
        - cityCode (string, required),

            !!! quote ""

                Mã thành phố

        - country (string, required),

            !!! quote ""

                Quốc gia

        - countryCode (string, required),

            !!! quote ""

                Mã quốc gia

        - firstName (string, required),

            !!! quote ""

                Tên khách hàng

        - lastName (string, required),

            !!! quote ""

                Họ khách hàng

        - phoneNumber (string, required),

            !!! quote ""

                Số điện thoại khách hàng

=== "Example"
    ```json
    {
        "userId": "string",
        "address": "string",
        "email": "string",
        "city": "Vĩnh Long",
        "cityCode": "vn_16d7_",
        "country": "Vietnam",
        "countryCode": "vn",
        "firstName": "string",
        "lastName": "string",
        "phoneNumber": "string"
    }
    ```

### Response 
#### Code 200
> OK

=== "Model"
    ???+ example "Model"

        - duration (Integer, Optional),
        - errors (Array[Error], Optional),
        - infos (Array[Info], Optional),
        - success (Boolean, Optional),
        - textMessage (String, Optional)
                        
=== "Example"
    ```json
    {
        "duration": 46854,
        "errors": null,
        "success": true,
        "textMessage": null,
        "infos": null
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

## 3. API lấy thông tin SubAgency

!!! info "POST: /api/partner/sub-agency"
    lấy thông tin subagency theo userId

### Parameter

=== "Paramter"
    ???+ example "Parameters"

        - userId `query` (String, Required)

            !!! quote ""

                Mã định danh của người dùng

=== "Example"
    ?userId=`b286b297-a22e-41c6-a776-49a6891c57b3`

### Response 
#### Code 200
> OK

=== "Model"
    ???+ example "Model"
        - result
            
            -  SubAgencyInfoDTO:

                - userId (string, required),

                    !!! quote ""

                        Mã định danh người dùng trên hệ thống của Đối tác.

                - address (string, required),

                    !!! quote ""

                        Địa chỉ khách hàng

                - email (string, required),

                    !!! quote ""

                        Email khách hàng

                - city (string, required),

                    !!! quote ""

                        Thành phố
                
                - cityCode (string, required),

                    !!! quote ""

                        Mã thành phố

                - country (string, required),

                    !!! quote ""

                        Quốc gia

                - countryCode (string, required),

                    !!! quote ""

                        Mã quốc gia

                - firstName (string, required),

                    !!! quote ""

                        Tên khách hàng

                - lastName (string, required),

                    !!! quote ""

                        Họ khách hàng

                - phoneNumber (string, required),

                    !!! quote ""

                        Số điện thoại khách hàng

                - agencyNumber (string, required) 

                    !!! quote ""

                        Mã agency bên hệ thống gotadi

        - duration (Integer, Optional),
        - errors (Array[Error], Optional),
        - infos (Array[Info], Optional),
        - success (Boolean, Optional),
        - textMessage (String, Optional)
                        
=== "Example"
    ```json
        {
            "result": {
                "userId": "b286b297-a22e-41c6-a776-49a6891c57b3",
                "address": "Hà Nội",
                "email": "namkh20008@fpt.com.vn",
                "city": "Hà Nội",
                "cityCode": "vn_163b_",
                "country": "Vietnam",
                "countryCode": "vn",
                "firstName": "Nam",
                "lastName": "Kim",
                "phoneNumber": "0836202008",
                "agencyNumber": "GOB2B2BHN0000027278"
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

## 4. API lấy thông tin thành phố / quốc gia

!!! info "GET: /api/_search/lookups
    Lấy thông tin thành phố / quốc gia

### Request Body 

=== "Parameter"
    ???+ example "Parameter"

        - domain_name (string, required),

            !!! quote ""

                Miền đối tượng

                - destination

        - object_name (string, required),

            !!! quote ""

                Tên đối tượng

        - lookupType (string, required),

            !!! quote ""

                Khu vực tìm kiếm


=== "Example"
    ```
    ?domain_name=destination&object_name=region&lookupType=vn&page=0&size=1000
    ```

### Response 
#### Code 200
> OK

=== "Model"
    ???+ example "Model"

        - id (Integer),
        - domainName (String),
        - objectName (String),
        - lookupType (String),
        - lookupValue (String)
        - description (String)
        - sortOrder (Integer)
        - lang (String)
        - lookupCode (String)
                        
=== "Example"
    ```json
    [
        {
            "id":13691,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16d9_",
            "description":"An Giang",
            "sortOrder":1791,
            "lang":"destination.region.vn_16d9_",
            "lookupCode":"AG"
        },
        {
            "id":13692,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16e6_",
            "description":"Bắc Giang",
            "sortOrder":1792,
            "lang":"destination.region.vn_16e6_",
            "lookupCode":"BG"
        },
        {
            "id":13693,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16e4_",
            "description":"Bắc Kạn",
            "sortOrder":1793,
            "lang":"destination.region.vn_16e4_",
            "lookupCode":"BK"
        },
        {
            "id":13694,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16dc_",
            "description":"Bạc Liêu",
            "sortOrder":1794,
            "lang":"destination.region.vn_16dc_",
            "lookupCode":"BL"
        },
        {
            "id":13695,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_15c6_",
            "description":"Bắc Ninh",
            "sortOrder":1795,
            "lang":"destination.region.vn_15c6_",
            "lookupCode":"BN"
        },
        {
            "id":13696,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_1640_",
            "description":"Bà Rịa - Vũng Tàu",
            "sortOrder":1796,
            "lang":"destination.region.vn_1640_",
            "lookupCode":"BR"
        },
        {
            "id":13697,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16d6_",
            "description":"Bến Tre",
            "sortOrder":1797,
            "lang":"destination.region.vn_16d6_",
            "lookupCode":"BT"
        },
        {
            "id":13698,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16f2_",
            "description":"Bình Định",
            "sortOrder":1798,
            "lang":"destination.region.vn_16f2_",
            "lookupCode":"BI"
        },
        {
            "id":13699,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_1584_",
            "description":"Bình Dương",
            "sortOrder":1799,
            "lang":"destination.region.vn_1584_",
            "lookupCode":"BD"
        },
        {
            "id":13700,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16d0_",
            "description":"Bình Phước",
            "sortOrder":1800,
            "lang":"destination.region.vn_16d0_",
            "lookupCode":"BP"
        },
        {
            "id":13701,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_1580_",
            "description":"Bình Thuận",
            "sortOrder":1801,
            "lang":"destination.region.vn_1580_",
            "lookupCode":"BH"
        },
        {
            "id":13702,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16dd_",
            "description":"Cà Mau",
            "sortOrder":1802,
            "lang":"destination.region.vn_16dd_",
            "lookupCode":"CM"
        },
        {
            "id":13703,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_163d_",
            "description":"Cần Thơ",
            "sortOrder":1803,
            "lang":"destination.region.vn_163d_",
            "lookupCode":"CT"
        },
        {
            "id":13704,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16e2_",
            "description":"Cao Bằng",
            "sortOrder":1804,
            "lang":"destination.region.vn_16e2_",
            "lookupCode":"CB"
        },
        {
            "id":13705,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16ce_",
            "description":"Đắk Lắk",
            "sortOrder":1805,
            "lang":"destination.region.vn_16ce_",
            "lookupCode":"DL"
        },
        {
            "id":13706,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16cf_",
            "description":"Đắk Nông",
            "sortOrder":1806,
            "lang":"destination.region.vn_16cf_",
            "lookupCode":"DK"
        },
        {
            "id":13707,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_163f_",
            "description":"Đà Nẵng",
            "sortOrder":1807,
            "lang":"destination.region.vn_163f_",
            "lookupCode":"DN"
        },
        {
            "id":13708,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16e9_",
            "description":"Điện Biên",
            "sortOrder":1808,
            "lang":"destination.region.vn_16e9_",
            "lookupCode":"DB"
        },
        {
            "id":13709,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16d2_",
            "description":"Đồng Nai",
            "sortOrder":1809,
            "lang":"destination.region.vn_16d2_",
            "lookupCode":"DI"
        },
        {
            "id":13710,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16d8_",
            "description":"Đồng Tháp",
            "sortOrder":1810,
            "lang":"destination.region.vn_16d8_",
            "lookupCode":"DT"
        },
        {
            "id":13711,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16ef_",
            "description":"Gia Lai",
            "sortOrder":1811,
            "lang":"destination.region.vn_16ef_",
            "lookupCode":"GL"
        },
        {
            "id":13712,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16e1_",
            "description":"Hà Giang",
            "sortOrder":1812,
            "lang":"destination.region.vn_16e1_",
            "lookupCode":"HA"
        },
        {
            "id":13713,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16ea_",
            "description":"Hải Dương",
            "sortOrder":1813,
            "lang":"destination.region.vn_16ea_",
            "lookupCode":"HD"
        },
        {
            "id":13714,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_1647_",
            "description":"Hải Phòng",
            "sortOrder":1814,
            "lang":"destination.region.vn_1647_",
            "lookupCode":"HP"
        },
        {
            "id":13715,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16cb_",
            "description":"Hà Nam",
            "sortOrder":1815,
            "lang":"destination.region.vn_16cb_",
            "lookupCode":"HM"
        },
        {
            "id":13716,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_163b_",
            "description":"Hà Nội",
            "sortOrder":1816,
            "lang":"destination.region.vn_163b_",
            "lookupCode":"HN"
        },
        {
            "id":13717,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16df_",
            "description":"Hà Tĩnh",
            "sortOrder":1817,
            "lang":"destination.region.vn_16df_",
            "lookupCode":"HT"
        },
        {
            "id":13718,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16da_",
            "description":"Hậu Giang",
            "sortOrder":1818,
            "lang":"destination.region.vn_16da_",
            "lookupCode":"HG"
        },
        {
            "id":13719,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16e0_",
            "description":"Hòa Bình",
            "sortOrder":1819,
            "lang":"destination.region.vn_16e0_",
            "lookupCode":"HB"
        },
        {
            "id":13720,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_163c_",
            "description":"HCM",
            "sortOrder":1820,
            "lang":"destination.region.vn_163c_",
            "lookupCode":"SG"
        },
        {
            "id":13721,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16c9_",
            "description":"Hưng Yên",
            "sortOrder":1821,
            "lang":"destination.region.vn_16c9_",
            "lookupCode":"HY"
        },
        {
            "id":13722,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_1585_",
            "description":"Khánh Hòa",
            "sortOrder":1822,
            "lang":"destination.region.vn_1585_",
            "lookupCode":"KH"
        },
        {
            "id":13723,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_1581_",
            "description":"Kiên Giang",
            "sortOrder":1823,
            "lang":"destination.region.vn_1581_",
            "lookupCode":"KG"
        },
        {
            "id":13724,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16f0_",
            "description":"Kon Tum",
            "sortOrder":1824,
            "lang":"destination.region.vn_16f0_",
            "lookupCode":"KT"
        },
        {
            "id":13725,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16ec_",
            "description":"Lai Châu",
            "sortOrder":1825,
            "lang":"destination.region.vn_16ec_",
            "lookupCode":"LH"
        },
        {
            "id":13726,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_164a_",
            "description":"Lâm Đồng",
            "sortOrder":1826,
            "lang":"destination.region.vn_164a_",
            "lookupCode":"LD"
        },
        {
            "id":13727,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16e5_",
            "description":"Lạng Sơn",
            "sortOrder":1827,
            "lang":"destination.region.vn_16e5_",
            "lookupCode":"LS"
        },
        {
            "id":13728,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_1646_",
            "description":"Lào Cai",
            "sortOrder":1828,
            "lang":"destination.region.vn_1646_",
            "lookupCode":"LC"
        },
        {
            "id":13729,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16d3_",
            "description":"Long An",
            "sortOrder":1829,
            "lang":"destination.region.vn_16d3_",
            "lookupCode":"LA"
        },
        {
            "id":13730,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16cc_",
            "description":"Nam Định",
            "sortOrder":1830,
            "lang":"destination.region.vn_16cc_",
            "lookupCode":"ND"
        },
        {
            "id":13731,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16de_",
            "description":"Nghệ An",
            "sortOrder":1831,
            "lang":"destination.region.vn_16de_",
            "lookupCode":"NA"
        },
        {
            "id":13732,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_1648_",
            "description":"Ninh Bình",
            "sortOrder":1832,
            "lang":"destination.region.vn_1648_",
            "lookupCode":"NB"
        },
        {
            "id":13733,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16f1_",
            "description":"Ninh Thuận",
            "sortOrder":1833,
            "lang":"destination.region.vn_16f1_",
            "lookupCode":"NT"
        },
        {
            "id":13734,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_15ef_",
            "description":"Phú Quốc",
            "sortOrder":1834,
            "lang":"destination.region.vn_15ef_",
            "lookupCode":"PQ"
        },
        {
            "id":13735,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16e8_",
            "description":"Phú Thọ",
            "sortOrder":1835,
            "lang":"destination.region.vn_16e8_",
            "lookupCode":"PT"
        },
        {
            "id":13736,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_1649_",
            "description":"Phú Yên",
            "sortOrder":1836,
            "lang":"destination.region.vn_1649_",
            "lookupCode":"PY"
        },
        {
            "id":13737,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16f6_",
            "description":"Quảng Bình",
            "sortOrder":1837,
            "lang":"destination.region.vn_16f6_",
            "lookupCode":"QB"
        },
        {
            "id":13738,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16f4_",
            "description":"Quảng Nam",
            "sortOrder":1838,
            "lang":"destination.region.vn_16f4_",
            "lookupCode":"QN"
        },
        {
            "id":13739,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16f3_",
            "description":"Quảng Ngãi",
            "sortOrder":1839,
            "lang":"destination.region.vn_16f3_",
            "lookupCode":"QG"
        },
        {
            "id":13740,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_157f_",
            "description":"Quảng Ninh",
            "sortOrder":1840,
            "lang":"destination.region.vn_157f_",
            "lookupCode":"QH"
        },
        {
            "id":13741,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16f5_",
            "description":"Quảng Trị",
            "sortOrder":1841,
            "lang":"destination.region.vn_16f5_",
            "lookupCode":"QT"
        },
        {
            "id":13742,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16db_",
            "description":"Sóc Trăng",
            "sortOrder":1842,
            "lang":"destination.region.vn_16db_",
            "lookupCode":"ST"
        },
        {
            "id":13743,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16ed_",
            "description":"Sơn La",
            "sortOrder":1843,
            "lang":"destination.region.vn_16ed_",
            "lookupCode":"SL"
        },
        {
            "id":13744,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16d1_",
            "description":"Tây Ninh",
            "sortOrder":1844,
            "lang":"destination.region.vn_16d1_",
            "lookupCode":"TN"
        },
        {
            "id":13745,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16ca_",
            "description":"Thái Bình",
            "sortOrder":1845,
            "lang":"destination.region.vn_16ca_",
            "lookupCode":"TB"
        },
        {
            "id":13746,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16e3_",
            "description":"Thái Nguyên",
            "sortOrder":1846,
            "lang":"destination.region.vn_16e3_",
            "lookupCode":"TE"
        },
        {
            "id":13747,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16d4_",
            "description":"Thanh Hóa",
            "sortOrder":1847,
            "lang":"destination.region.vn_16d4_",
            "lookupCode":"TH"
        },
        {
            "id":13748,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_163e_",
            "description":"Thừa Thiên Huế",
            "sortOrder":1848,
            "lang":"destination.region.vn_163e_",
            "lookupCode":"TT"
        },
        {
            "id":13749,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16d5_",
            "description":"Tiền Giang",
            "sortOrder":1849,
            "lang":"destination.region.vn_16d5_",
            "lookupCode":"TG"
        },
        {
            "id":13750,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16cd_",
            "description":"Trà Vinh",
            "sortOrder":1850,
            "lang":"destination.region.vn_16cd_",
            "lookupCode":"TV"
        },
        {
            "id":13751,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16e7_",
            "description":"Tuyên Quang",
            "sortOrder":1851,
            "lang":"destination.region.vn_16e7_",
            "lookupCode":"TQ"
        },
        {
            "id":13752,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16d7_",
            "description":"Vĩnh Long",
            "sortOrder":1852,
            "lang":"destination.region.vn_16d7_",
            "lookupCode":"VL"
        },
        {
            "id":13753,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16eb_",
            "description":"Vĩnh Phúc",
            "sortOrder":1853,
            "lang":"destination.region.vn_16eb_",
            "lookupCode":"VP"
        },
        {
            "id":13754,
            "domainName":"destination",
            "objectName":"region",
            "lookupType":"vn",
            "lookupValue":"vn_16ee_",
            "description":"Yên Bái",
            "sortOrder":1854,
            "lang":"destination.region.vn_16ee_",
            "lookupCode":"YB"
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