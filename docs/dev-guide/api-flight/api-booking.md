# Document Flight API Booking

---

## 1.API kiểm tra tình trạng vé

!!! info "POST: /api/air-tickets/revalidate"

    Kiểm tra tình trạng vé còn hữu dụng trước khi đi booking

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

        - valid (Boolean, Required) 

            !!! quote ""

            Thông tin vé còn hữu dụng hay không

                        
        - duration (Integer, Optional),
        - errors (Array[Error], Optional),
        - infos (Array[Info], Optional),
        - success (Boolean, Optional),
        - textMessage (String, Optional)

=== "Example"
    ```json

    {
        "duration" : 858,
        "errors" : null,
        "infos" : null,
        "itinerary" : null,
        "success" : true,
        "textMessage" : null,
        "valid" : true
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

## 2.API khởi tạo thông tin booking

!!! info "POST: /api/air-tickets/draft-booking"

    Kiểm tra tình trạng vé còn hữu dụng trước khi đi booking

### Request Body

=== "Model"
    ???+ example "Request Body"

        - itineraryInfos (Array[ItineraryInfo], Required)

            !!! quote ""

                Thông tin hành trình chiều đi + chiều về (nếu có)

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
            "itineraryInfos": [
                {
                    "fareSourceCode": "dom07b2da7b-3232-4294-9278-b35fb6307714",
                    "groupId": "27b091a7-62b8-4ce2-b45b-eda3340d7673",
                    "searchId": "ATD::210720::dc96e1a9-c39e-4f48-974e-e0be6abb45c7"
                },
                {
                    "fareSourceCode": "domb771ff7f-57b5-4bd5-9443-e43b79f61aaa",
                    "groupId": "8ceaa3c5-bbcf-451a-95ae-cd0a81e60993",
                    "searchId": "ATD::210720::dc96e1a9-c39e-4f48-974e-e0be6abb45c7-R"
                }
            ]
        }

    ```

### Response

#### Code 200

> OK

=== "Model"
    ???+ example "Model"
        `Chỉ định danh những trường/field cần thiết`

        - bookingCode (BookingCode, Required) 

            !!! quote ""

                Thông tin mã định danh Booking

            - bookingCode (String, Required)

                !!! quote ""

                    Mã định danh booking

            - bookingNumber (String, Required)

                !!! quote ""

                    Mã dùng tham chiếu đến booking. Mã này là duy nhất.

        - bookingType (String, Required)

            !!! quote ""
                
                Thông tin thể hiện loại booking: Trong nước hay quốc tế

                - `DOME`: Trong nước
                - `INTE`: Quốc tế
            
        - departDraftItineraryInfo (DraftItineraryInfo, Required)

            !!! quote ""

                Thông tin hành trình chiều đi
            
            - bookingDirection (String, Required) 

                !!! quote ""

                    Thông tin chiều đi 

                    - `DEPARTURE`: chiều đi
                    - `RETURN`: chiều về
                    - `TRIP`: dùng cho vé quốc tế (chiều đi + chiều về)
            
            - fareSourceCode(String, Required)

                !!! quote ""

                    Thông tin mã định danh hành trình
            
            - groupId (String, Required)    

                !!! quote ""

                    Mã định danh hành trình trong danh sách hành trình trả về theo kết quả tìm kiếm
                
            - itinTotalFare (ItinTotalFare, Required)

                !!! quote ""

                    Thông tin các loại giá của hành trình

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
                
                - totalTax (FareInfo, Required)

                    !!! quote ""

                        Tương tự như baseFare

                        Thông tin tổng phí dịch vụ
                
                - totalFare (FareInfo, Required)

                    !!! quote ""

                        Tương tự như baseFare

                        Thông tin tổng cộng giá vé
        
        - returnDraftItineraryInfo (DraftItineraryInfo, Optional)

            !!! quote ""

                Tương tự như thông tin chi tiết hành trình chiều đi

                Thông tin hành trình chiều về

        - duration (Integer, Optional),
        - errors (Array[Error], Optional),
        - infos (Array[Info], Optional),
        - success (Boolean, Optional),
        - textMessage (String, Optional)

=== "Example"
    ```json

        {
            "bookingCode": {
                "bookingCode": "BOD::210720::b87fd70e-4a9b-4532-9cb6-7d8142822ac3",
                "bookingNumber": "ADCO2107201223803"
            },
            "bookingType": "DOME",
            "departDraftItineraryInfo": {
                "bookingDirection": "DEPARTURE",
                "fareSourceCode": "dom07b2da7b-3232-4294-9278-b35fb6307714",
                "groupId": "27b091a7-62b8-4ce2-b45b-eda3340d7673",
                "itinTotalFare": {
                "baseFare": {
                    "amount": 399000,
                    "currencyCode": null,
                    "decimalPlaces": 2
                },
                "comboMarkup": null,
                "equivFare": {
                    "amount": 0,
                    "currencyCode": null,
                    "decimalPlaces": 2
                },
                "serviceTax": {
                    "amount": 512000,
                    "currencyCode": null,
                    "decimalPlaces": 2
                },
                "totalFare": {
                    "amount": 911000,
                    "currencyCode": null,
                    "decimalPlaces": 2
                },
                "totalPaxFee": null,
                "totalTax": {
                    "amount": 0,
                    "currencyCode": null,
                    "decimalPlaces": 2
                }
                },
                "searchId": "ATD::210720::dc96e1a9-c39e-4f48-974e-e0be6abb45c7"
            },
            "duration": 3498,
            "errors": null,
            "infos": null,
            "isPerBookingType": true,
            "isRoundTripType": true,
            "isSuccess": true,
            "markupType": "PER_BOOKING",
            "returnDraftItineraryInfo": {
                "bookingDirection": "RETURN",
                "fareSourceCode": "domb771ff7f-57b5-4bd5-9443-e43b79f61aaa",
                "groupId": "8ceaa3c5-bbcf-451a-95ae-cd0a81e60993",
                "itinTotalFare": {
                "baseFare": {
                    "amount": 1319000,
                    "currencyCode": null,
                    "decimalPlaces": 2
                },
                "comboMarkup": null,
                "equivFare": null,
                "serviceTax": {
                    "amount": 350900,
                    "currencyCode": null,
                    "decimalPlaces": 2
                },
                "totalFare": {
                    "amount": 1669900,
                    "currencyCode": null,
                    "decimalPlaces": 2
                },
                "totalPaxFee": null,
                "totalTax": {
                    "amount": 0,
                    "currencyCode": null,
                    "decimalPlaces": 2
                }
                },
                "searchId": "ATD::210720::dc96e1a9-c39e-4f48-974e-e0be6abb45c7-R"
            },
            "roundType": "RoundTrip",
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

## 3.API lấy chi tiết thông tin booking

!!! info "GET: /api/product/booking-detail"

    Lấy thông tin chi tiết của booking

### Parameter

=== "Parameters"
    ???+ example "Parameter"

        - bookingNumber (String, Required)

            !!! quote ""

                Mã tham chiếu đến booking

=== "Example"

    ?bookingNumber=`ADCO2107201223969`

### Response

#### Code 200

> OK

=== "Model"
    ???+ example "Model"
        `Chỉ định danh những trường/field cần thiết`

        - id (String, Optional),

            !!! quote ""

                Mã định danh chi tiết booking 

        - agencyCode (String, Optional),

            !!! quote "" 

                Mã đại lý. Mã dùng tham chiếu đến tác giả của booking

        - agentCode (String, Optional),

            !!! quote "" 

                Mã nhân viên đại lý. Mã dùng tham chiếu đến tác giả của booking

        - bookingCode (String, Optional),

            !!! quote "" 

                Mã dùng mô tả các thông tin cơ bản của booking
                
        - bookingDate (String, Optional),

            !!! quote "" 

                Ngày tạo booking 

        - bookingInfo (BookingInfo, Optional),

            !!! quote "" 

                Thông tin booking 

            - additionalFee (Number, Optional),

                !!! quote ""
        
                    Các khoản phí khác 

            - agencyCode (String, Optional),

                !!! quote "" 

                    Mã đại lý. Mã dùng tham chiếu đến tác giả của booking

            - ~~agencyMarkupInfos (Array[BookingAgencyMarkupInfo], Optional),~~

            - ~~agencyMarkupValue (Number, Optional),~~

            - agentCode (String, Optional),

                !!! quote "" 

                    Mã nhân viên đại lý. Mã dùng tham chiếu đến tác giả của booking

            - agentId (Integer, Optional),

                !!! quote "" 

                    Id nhân viên đại lý

            - agentName (String, Optional),

                !!! quote "" 

                    Tên nhân viên đại lý 

            - allowHold (Boolean, Optional),

                !!! quote "" 

                    Cho phép giữ vé máy bay hay không 

                    `true`: cho phép giữ vé

                    `false`: Không cho phép giữ vé 

            - baseFare (Number, Optional),

                !!! quote ""
        
                    Giá phòng chưa bao gồm thuế phí 

            - bookBy (String, Optional),

                !!! quote ""
        
                    Người đặt booking 

            - bookByCode (String, Optional),

                !!! quote ""
        
                    Mã người đặt 

            - bookingCode (String, Optional),

                !!! quote "" 

                    Mã dùng mô tả các thông tin cơ bản của booking

            - bookingDate (String, Optional),

                !!! quote "" 

                    Ngày tạo booking 

            - ~~bookingIssuedType (String, Optional) = ['INSTANT_BOOKING', 'CONFIRM_OFFLINE'],~~

            - bookingNote (String, Optional),

                !!! quote "" 

                    Ghi chú của booking 

            - bookingNumber (String, Optional),

                !!! quote "" 

                    Mã dùng tham chiếu đến booking. Mã này là duy nhất.

            - bookingType (String, Optional) = ['DOME', 'INTE'],

                !!! quote "" 

                    Xác định điểm đến là trong nước hay quốc tế 

                    - `DOME`: Trong nước 

                    - `INTE`: Quốc tế 

            - branchCode (String, Optional),

                !!! quote "" 

                    Mã chi nhánh 

            - cancellationBy (String, Optional),

                !!! quote "" 

                    Hủy vé bởi ...

            - cancellationDate (String, Optional),

                !!! quote "" 

                    Ngày hủy vé

            - cancellationFee (Number, Optional),

                !!! quote "" 

                    Phí hủy đặt phòng 

            - cancellationNotes (String, Optional),

                !!! quote "" 

                    Ghi chú hủy 

            - channelType (String, Optional) = ['ONLINE', 'OFFLINE'],

                !!! quote "" 

                    Loại kênh đặt phòng

            - contactInfos (Array[BookingContactInfo], Optional),

                !!! quote "" 

                    Mảng đối tượng chứ thông tin người liên hệ 

                - bookingNumber (String, Optional),

                    !!! quote ""

                        Mã tham chiếu đến booking

                - contactLevel (String, Optional) = ['PRIMARY', 'SECONDARY', 'OTHER'],

                    !!! quote ""

                        Cấp của người liên hệ 

                - contactType (String, Optional) = ['CUSTOMER', 'AGENCY'],
                
                    !!! quote ""

                        Loại của người liên hệ 

                - email (String, Optional),

                    !!! quote ""

                        Địa chỉ email 

                - firstName (String, Optional),

                    !!! quote ""

                        Tên đêm và tên người liên hệ 
                        
                - phoneCode1 (String, Optional),

                    !!! quote ""

                        Mã quốc gia 

                - phoneNumber1 (String, Optional),

                    !!! quote ""

                        Số điện thoại 1

                - surName (String, Optional)

                    !!! quote ""

                        Họ người liên hệ 

            - customerCode (String, Optional),

                !!! quote "" 

                    Mã khách hàng 

            - customerEmail (String, Optional),

                !!! quote "" 

                    Email của khách hàng 

            - customerFirstName (String, Optional),

                !!! quote "" 

                    Họ của khách hàng 

            - customerId (Integer, Optional),

                !!! quote "" 

                    Id của khách hàng 

            - customerLastName (String, Optional),

                !!! quote "" 

                    Tên của khách hàng 

            - customerPhoneNumber1 (String, Optional),

                !!! quote "" 

                    Số điện thoại 1 của khách hàng 

            - customerPhoneNumber2 (String, Optional),

                !!! quote "" 

                    Số điện thoại 2 của khách hàng 

            - ~~deleted (Boolean, Optional),~~

            - departureDate (String, Optional),

                !!! quote "" 

                    Ngày khởi hành

            - discountAmount (Number, Optional),

                !!! quote "" 

                    Số tiền được giảm 
            
            - discountDate (String, Optional),

                !!! quote "" 

                    Ngày sử dụng mã giảm giá 
            
            - discountRedeemCode (String, Optional),

                !!! quote "" 

                    Mã liên kết đổi thưởng 
            
            - discountRedeemId (String, Optional),

                !!! quote "" 

                    Id định danh liên kết đổi thường 
            
            - discountVoucherCode (String, Optional),

                !!! quote "" 

                    Mã voucher 
            
            - discountVoucherName (String, Optional),

                !!! quote "" 

                    Tên voucher
            
            - ~~displayPriceInfo (BookingPriceInfo, Optional),~~
            
            - equivFare (Number, Optional),

                !!! quote ""

                    Phí xuất vé

            - etickets (String, Optional),

                !!! quote "" 

                    Mã liên kết với nhà cung cấp, được sử dụng để nhận vé máy bay

            - fromCity (String, Optional),

                !!! quote ""

                    Tên thành phố khởi hành

            - fromLocationCode (String, Optional),

                !!! quote ""

                    Mã định danh sân bay khởi hành

            - fromLocationName (String, Optional),

                !!! quote ""

                    Tên sân bay khởi hành

            - id (integer, Optional),

                !!! quote "" 

                    Id của booking 

            - ~~internalBookingNote (String, Optional),~~

            - issuedByCode (String, Optional),

                !!! quote "" 

                    Xuất vé bởi ...

            - issuedDate (String, Optional),

                !!! quote "" 

                    Ngày xuất phòng 

            - issuedStatus (String, Optional) = ['PENDING', 'TICKET_ON_PROCESS', 'SUCCEEDED', 'FAILED'],

                !!! quote "" 

                    Trạng thái xuất vé 

                    - `PENDING`: Đợi xuất vé 

                    - `TICKET_ON_PROCESS`: Xuất vé đang được xử lý 

                    - `SUCCEEDED`: Xuất vé thành công 

                    - `FAILED`: Xuất vé thất bại 

            - ~~markupValue (Number, Optional),~~

            - ~~onlyPayLater (Boolean, Optional),~~

            - orgCode (String, Optional),

                !!! quote "" 

                    Mã tổ chức 

            - ~~ownerBooking (Boolean, Optional),~~

            - passengerNameRecords (String, Optional),

                !!! quote "" 

                    Mã liên kết với nhà cung cấp, được sử dụng để nhận vé máy bay

            - paymentBy (String, Optional),

                !!! quote "" 

                    Thanh toán bởi ...

            - paymentByCode (String, Optional),

                !!! quote "" 

                    Mã người thanh toán 

            - paymentDate (String, Optional),

                !!! quote "" 

                    Thời gian thanh toán 

            - paymentFee (Number, Optional),

                !!! quote "" 

                    Phí thanh toán 

            - paymentRefNumber (String, Optional),

                !!! quote "" 

                    Mã tham chiếu thanh toán 

            - paymentStatus (String, Optional) = ['SUCCEEDED', 'FAILED', 'REFUNDED', 'PENDING'],

                !!! quote "" 

                    Trạng thái thanh toán 

                    - `PENDING`: Chờ thanh toán 

                    - `SUCCEEDED`: Thanh toán thành công 

                    - `FAILED`: Thanh toán thất bại 

                    - `REFUNDED`: Hoàn tiền 

            - paymentTotalAmount (Number, Optional),

                !!! quote "" 

                    Tổng số tiền thanh toán 

            - paymentType (String, Optional) = ['BALANCE', 'CREDIT', 'ATM_DEBIT', 'AIRPAY', 'VNPAYQR', 'VIETTELPAY', 'MOMO', 'ZALO', 'PAYOO', 'CASH', 'TRANSFER', 'PARTNER', 'OTHER'],

                !!! quote "" 

                    Hình thức thanh toán 

            - ~~promotionID (Array[String], Optional),~~
            
            - ~~reasonCodePaymentFailed (String, Optional),~~
            
            - refundBy (String, Optional),

                !!! quote "" 

                    Người hoàn trả 

            - refundByCode (String, Optional),

                !!! quote "" 

                    Mã của người thực hiện hoàn trả  
            
            - refundable (Boolean, Optional),

                !!! quote "" 

                    Ngày hoàn trả 
            
            - returnDate (String, Optional),

                !!! quote "" 

                    Ngày trả phòng 
            
            - roundType (String, Optional) = ['RoundTrip],
            
            - saleChannel (String, Optional) = ['B2B', 'B2C', 'B2B2C', 'B2C_WEB', 'B2C_WEB_APP', 'B2C_MOBILE'],

                !!! quote "" 

                    Kênh phân phối 
            
            - serviceTax (Number, Optional),

                !!! quote "" 

                    Thuế và phí

            - ~~showPayLaterOption (Boolean, Optional),~~

            - ~~showPayNowOption (Boolean, Optional),~~

            - status (String, Optional) = ['PENDING', 'BOOKING_ON_PROCESS', 'BOOKED', 'FAILED', 'CANCELLED', 'EXPIRED'],

                !!! quote "" 

                    Trạng thái của booking 

                    - `PENDING`: Chờ xác nhận booking 

                    - `BOOKING_ON_PROCESS`: Booking đang được xử lý 

                    - `BOOKED`: Booking đã được xác nhận 

                    - `FAILED`: Booking thất bại 

                    - `EXPIRED`: Booking hết hạn 

                    - `CANCELLED`: Booking đã bị hủy 

            - ~~supplierBookingStatus (String, Optional),~~

            - supplierType (String, Optional) = ['AIR', 'HOTEL', 'TOURS', 'TRAIN', 'SHIP', 'OTHER'],

                !!! quote "" 

                    Loại nhà cung cấp 

            - taxAddress1 (String, Optional),

                !!! quote "" 

                    Địa chỉ xuất hóa đơn dòng 1

            - taxAddress2 (String, Optional),

                !!! quote "" 

                    Địa chỉ xuất hóa đơn dòng 2

            - taxCompanyName (String, Optional),

                !!! quote "" 

                    Tên công ty xuất hóa đơn 

            - taxNumber (String, Optional),

                !!! quote "" 

                    Mã số thuế cần xuất hóa đơn 

            - taxPersonalInfoContact (String, Optional),

                !!! quote "" 

                    Người nhận hóa đơn 

            - taxReceiptRequest (Boolean, Optional),

                !!! quote "" 

                    Yêu cầu xuất hóa đơn hay không 

            - timeToLive (String, Optional),

                !!! quote "" 

                    Thời gian chờ thanh toán, sau thời gian này trạng thái của booking sẽ chuyển sang `EXPIRED`

            - toCity (String, Optional),

                !!! quote "" 

                    Tên tỉnh, thành phố điểm đến

            - toLocationCode (String, Optional),

                !!! quote "" 

                    Mã định danh điểm đến

            - toLocationName (String, Optional),

                !!! quote "" 

                    Tên sân bay điểm đến
                    
            - totalFare (Number, Optional),

                !!! quote "" 

                    Tổng giá phòng 

            - totalSsrValue (Number, Optional),

                !!! quote ""

                    Tổng giá hành lý / dịch vụ thêm

            - totalTax (Number, Optional),

                !!! quote "" 

                    Tổng số tiền thuế phí 

            - transactionInfos (Array[BookingTransactionInfo], Optional),

                !!! quote "" 

                    Mảng đối tượng chứa thông tin giao dịch 

                - id (integer, Optional),

                    !!! quote "" 

                        Id định danh giao dịch 

                - ~~agencyMarkupValue (Number, Optional),~~

                - allowHold (Boolean, Optional),

                    !!! quote "" 

                        Cho phép giữ vé hay không 

                - bookingCode (String, Optional),

                    !!! quote "" 

                        Mã dùng mô tả các thông tin cơ bản của booking

                - bookingDate (String, Optional),

                    !!! quote "" 

                        Ngày tạo booking 

                - bookingDirection (String, Optional) = ['DEPARTURE', 'RETURN'],

                - bookingNumber (String, Optional),

                    !!! quote "" 

                        Mã dùng tham chiếu đến booking.

                - bookingRefNo (String, Optional),

                    !!! quote "" 

                        Mã liên kết với nhà cung cấp 

                - channelType (String, Optional) = ['ONLINE', 'OFFLINE'],

                    !!! quote "" 

                        Loại kênh bán 

                - checkIn (String, Optional),

                    !!! quote "" 

                        Ngày giờ bay

                - checkOut (String, Optional),

                    !!! quote "" 

                        Ngày giờ đến

                - destinationLocationCode (String, Optional),

                    !!! quote "" 

                        Mã định danh sân bây
                
                - detail (String, Optional),

                    !!! quote "" 

                        Tên khách sạn 

                - etickets (String, Optional),

                    !!! quote "" 

                        Mã liên kết với nhà cung cấp, được sử dụng để nhận vé
                
                - issuedDate (String, Optional),

                    !!! quote "" 

                        Ngày xuất vé 

                - issuedStatus (String, Optional) = ['PENDING', 'TICKET_ON_PROCESS', 'SUCCEEDED', 'FAILED'],

                    !!! quote "" 

                        Trạng thái xuất vé 

                        - `PENDING`: Đợi xuất vé 

                        - `TICKET_ON_PROCESS`: Xuất vé đang được xử lý 

                        - `SUCCEEDED`: Xuất vé thành công 

                        - `FAILED`: Xuất vé thất bại 

                - ~~markupCode (String, Optional),~~

                - ~~markupFormula (String, Optional),~~

                - ~~markupKey (String, Optional),~~

                - ~~markupValue (Number, Optional),~~

                - noAdult (integer, Optional),

                    !!! quote "" 

                        Số người lớn 

                - noChild (integer, Optional),

                    !!! quote "" 

                        Số trể em 

                - onlyPayLater (Boolean, Optional),

                    !!! quote "" 

                        Cho phép trả sau hay không 

                - passengerNameRecord (String, Optional),

                    !!! quote "" 

                        Mã liên kết với nhà cung cấp, được sử dụng để nhận vé 

                - paymentAmount (Number, Optional),

                    !!! quote "" 

                        Số tiền thanh toán 

                - productSeqNumber (String, Optional),

                    !!! quote ""

                        Mã sản phẩm 

                - refundable (Boolean, Optional),

                    !!! quote "" 

                        Có hoàn tiền khi hủy vé hay không 

                - saleChannel (String, Optional) = ['B2B', 'B2C', 'B2B2C', 'B2C_WEB', 'B2C_WEB_APP', 'B2C_MOBILE'],

                    !!! quote "" 

                        Kênh phân phối 

                - serviceTax (Number, Optional),

                    !!! quote "" 

                        Thuế và phí

                - status (String, Optional) = ['PENDING', 'BOOKING_ON_PROCESS', 'BOOKED', 'FAILED', 'CANCELLED', 'EXPIRED'],

                    !!! quote "" 

                        Trạng thái của booking 

                        - `PENDING`: Chờ xác nhận booking 

                        - `BOOKING_ON_PROCESS`: Booking đang được xử lý 

                        - `BOOKED`: Booking đã được xác nhận 

                        - `FAILED`: Booking thất bại 

                        - `EXPIRED`: Booking hết hạn 

                        - `CANCELLED`: Booking đã bị hủy 

                - supplierCode (String, Optional),

                    !!! quote "" 

                        Mã nhà cung cấp 

                - supplierName (String, Optional),

                    !!! quote "" 

                        Tên nhà cung cấp 

                - supplierType (String, Optional) = ['AIR', 'HOTEL', 'TOURS', 'TRAIN', 'SHIP', 'OTHER']

                    !!! quote "" 

                        Loại sản phẩm 

                - totalFare (Number, Optional),
                
                    !!! quote ""

                        Tổng giá vé 

                - totalTax (Number, Optional)

                    !!! quote ""

                        Tổng thuế và phí 
                
                - baseFare (Number, Optional),

                    !!! quote "" 

                        Giá vé không bao gồm thuế phí 

            - travelerInfos (Array[BookingTravelerInfo], Optional),

                !!! quote ""

                    Mảng đối tượng chứa thông tin hành khách.

                - bookingNumber (String),

                    !!! quote ""

                        Mã tham chiếu đến booking 

                - firstName (String),

                    !!! quote ""

                        Tên đêm và tên hành khách

                - surName (String)

                    !!! quote ""

                        Họ của hành khách

        - bookingNumber (String, Optional),

            !!! quote "" 

                Mã dùng tham chiếu đến booking. Mã này là duy nhất.

        - bookingType (String, Optional),

            !!! quote "" 

                Xác định điểm đến là trong nước hay quốc tế 

                - `DOME`: Trong nước 

                - `INTE`: Quốc tế 

        - branchCode (String, Optional),

            !!! quote "" 

                Mã chi nhánh 

        - cacheType (String, Optional) = ['COMBO'],

        - ~~channelType (String, Optional) = ['ONLINE', 'OFFLINE'],~~

            !!! quote "" 

                Loại kênh đặt vé máy bay

        - ~~customerCode (String, Optional),~~

            !!! quote "" 

                Mã khách hàng 

        - groupPricedItineraries (Array[GroupPricedItinerary], Optional),

            !!! quote ""

                Thông tin danh sách hành trình trả về theo kết quả tìm kiếm

                Tương tự như lấy thông tin tìm kiếm vé máy bay

        - ~~hotelAvailability (HotelAvailability, Optional),~~

        - ~~hotelProduct (HotelProduct, Optional)~~,

        - ~~hotelProductPayload (HotelProductPayload, Optional)~~,

        - ~~isPerBookingType (Boolean, Optional),~~

        - ~~markupType (String, Optional),~~

        - ~~offlineBooking (OfflineBooking, Optional),~~

        - orgCode (String, Optional),

            !!! quote "" 

                Mã tổ chức 

        - saleChannel (String, Optional) = ['B2B', 'B2C', 'B2B2C', 'B2C_WEB', 'B2C_WEB_APP', 'B2C_MOBILE'],

            !!! quote "" 

                Kênh phân phối 

        - supplierType (String, Optional)  = ['AIR', 'HOTEL', 'TOURS', 'TRAIN', 'SHIP', 'OTHER'],

            !!! quote "" 

                Loại nhà cung cấp 

        - ~~travelerInfo (TravelerInfo, Optional),~~
        - ~~updatedDate (String, Optional)~~

=== "Example"
    ```json

        {
            "id": "BOD::210720::157f1341-5a66-4b0e-a6fb-a2d39b99dfdf",
            "updatedDate": "2021-07-20T07:11:49.524Z",
            "cacheType": "COMBO",
            "orgCode": "A::1",
            "agencyCode": "A::1",
            "branchCode": null,
            "saleChannel": "B2C_WEB",
            "channelType": "ONLINE",
            "supplierType": "AIR",
            "bookingCode": "BOD::210720::157f1341-5a66-4b0e-a6fb-a2d39b99dfdf",
            "bookingType": "DOME",
            "agentCode": null,
            "customerCode": "C::A::1|-1",
            "bookingNumber": "ADCO2107201223969",
            "bookingDate": "2021-07-20T07:11:49.52Z",
            "markupType": "PER_BOOKING",
            "bookingInfo": {
                "id": 1223969,
                "orgCode": "A::1",
                "agencyCode": "A::1",
                "saleChannel": "B2C_WEB",
                "channelType": "ONLINE",
                "supplierType": "AIR",
                "bookingCode": "BOD::210720::157f1341-5a66-4b0e-a6fb-a2d39b99dfdf",
                "bookingType": "DOME",
                "agentCode": null,
                "agentId": null,
                "agentName": null,
                "branchCode": null,
                "customerCode": "C::A::1|-1",
                "customerId": -1,
                "bookingNumber": "ADCO2107201223969",
                "roundType": "RoundTrip",
                "fromLocationCode": "HAN",
                "fromLocationName": "Sân bay Nội Bài",
                "fromCity": "Hà Nội",
                "toLocationCode": "SGN",
                "toLocationName": "Sân bay Tân Sơn Nhất",
                "toCity": "Hồ Chí Minh",
                "status": "PENDING",
                "bookingDate": "2021-07-20T07:11:49.52Z",
                "departureDate": "2021-08-16T05:10:00Z",
                "returnDate": "2021-08-24T05:25:00Z",
                "baseFare": 2638000,
                "equivFare": 0,
                "serviceTax": 701800,
                "vat": null,
                "totalFare": 3339800,
                "totalTax": 701800,
                "agencyMarkupValue": 0,
                "markupValue": 0,
                "totalSsrValue": 0,
                "totalCombo": null,
                "paymentTotalAmount": 0,
                "paymentFee": 0,
                "paymentType": "OTHER",
                "paymentStatus": "PENDING",
                "paymentDate": null,
                "paymentRefNumber": null,
                "issuedStatus": "PENDING",
                "issuedDate": null,
                "customerFirstName": null,
                "customerLastName": null,
                "customerPhoneNumber1": null,
                "customerPhoneNumber2": null,
                "customerEmail": null,
                "taxReceiptRequest": null,
                "taxCompanyName": null,
                "taxAddress1": null,
                "taxAddress2": null,
                "taxNumber": null,
                "paymentBy": null,
                "paymentByCode": null,
                "issuedByCode": null,
                "refundBy": null,
                "refundByCode": null,
                "bookBy": "GUEST",
                "bookByCode": "C::A::1|-1",
                "displayPriceInfo": {
                "bookingNumber": "ADCO2107201223969",
                "baseFare": 2638000,
                "equivFare": 0,
                "serviceTax": 701800,
                "totalFare": 3339800,
                "totalTax": 701800,
                "agencyMarkupValue": 0,
                "markupValue": 0,
                "totalSsrValue": 0,
                "cancellationFee": 0,
                "paymentFee": 0,
                "discountAmount": 0,
                "additionalFee": 0,
                "additionalTaxPerTraveler": 0,
                "vat": null
                },
                "transactionInfos": [
                {
                    "id": 1224043,
                    "saleChannel": "B2C_WEB",
                    "channelType": "ONLINE",
                    "supplierType": "AIR",
                    "bookingCode": "ADCO2107201223969::HAN-SGN::domd879a3f6-f3cb-40d6-8e95-52dd0a7d47a5",
                    "bookingNumber": "ADCO2107201223969",
                    "status": "PENDING",
                    "bookingDate": "2021-07-20T07:11:49.52Z",
                    "supplierCode": "VJ",
                    "supplierName": "Vietjet Air",
                    "bookingRefNo": null,
                    "passengerNameRecord": null,
                    "timeToLive": null,
                    "signature": null,
                    "detail": "HAN-SGN :: VJ 135",
                    "originLocationCode": "HAN",
                    "destinationLocationCode": "SGN",
                    "carrierNo": "135",
                    "checkIn": "2021-08-16T07:20:00Z",
                    "checkOut": "2021-08-16T05:10:00Z",
                    "baseFare": 1319000,
                    "equivFare": 0,
                    "serviceTax": 350900,
                    "totalFare": 1669900,
                    "totalTax": 350900,
                    "agencyMarkupValue": 0,
                    "markupValue": null,
                    "totalSsrValue": 0,
                    "markupKey": "F2C|A::1|A|DOME|BAS|VIETJET|ECONOMY|-1",
                    "markupCode": null,
                    "markupFormula": null,
                    "paymentAmount": null,
                    "issuedStatus": "PENDING",
                    "issuedDate": null,
                    "etickets": null,
                    "listETickets": null,
                    "productSeqNumber": "ibe4754299335928434",
                    "productClass": "ECONOMY",
                    "bookingDirection": "DEPARTURE",
                    "noAdult": 1,
                    "noChild": 0,
                    "noInfant": 0,
                    "b2cBasePrice": 0,
                    "b2cTaxAndFees": 0,
                    "adjustNet": 0,
                    "adjustContract": 0,
                    "b2cTotalPrice": 0,
                    "supplierBookingStatus": "PENDING",
                    "supplierPaymentStatus": null,
                    "onlyPayLater": false,
                    "allowHold": true,
                    "refundable": false
                },
                {
                    "id": 1224044,
                    "saleChannel": "B2C_WEB",
                    "channelType": "ONLINE",
                    "supplierType": "AIR",
                    "bookingCode": "ADCO2107201223969::SGN-HAN::dom389dca01-c0fd-466b-8a98-daaa4d5a06d4",
                    "bookingNumber": "ADCO2107201223969",
                    "status": "PENDING",
                    "bookingDate": "2021-07-20T07:11:49.52Z",
                    "supplierCode": "VJ",
                    "supplierName": "Vietjet Air",
                    "bookingRefNo": null,
                    "passengerNameRecord": null,
                    "timeToLive": null,
                    "signature": null,
                    "detail": "SGN-HAN :: VJ 176",
                    "originLocationCode": "SGN",
                    "destinationLocationCode": "HAN",
                    "carrierNo": "176",
                    "checkIn": "2021-08-24T07:35:00Z",
                    "checkOut": "2021-08-24T05:25:00Z",
                    "baseFare": 1319000,
                    "equivFare": 0,
                    "serviceTax": 350900,
                    "totalFare": 1669900,
                    "totalTax": 350900,
                    "agencyMarkupValue": 0,
                    "markupValue": null,
                    "totalSsrValue": 0,
                    "markupKey": "F2C|A::1|A|DOME|BAS|VIETJET|ECONOMY|-1",
                    "markupCode": null,
                    "markupFormula": null,
                    "paymentAmount": null,
                    "issuedStatus": "PENDING",
                    "issuedDate": null,
                    "etickets": null,
                    "listETickets": null,
                    "productSeqNumber": "ibe4754299329767108",
                    "productClass": "ECONOMY",
                    "bookingDirection": "RETURN",
                    "noAdult": 1,
                    "noChild": 0,
                    "noInfant": 0,
                    "b2cBasePrice": 0,
                    "b2cTaxAndFees": 0,
                    "adjustNet": 0,
                    "adjustContract": 0,
                    "b2cTotalPrice": 0,
                    "supplierBookingStatus": "PENDING",
                    "supplierPaymentStatus": null,
                    "onlyPayLater": false,
                    "allowHold": true,
                    "refundable": false
                }
                ],
                "agencyMarkupInfos": [
                {
                    "agencyCode": "A::1",
                    "baseFare": 2638000,
                    "equivFare": 0,
                    "serviceTax": 701800,
                    "totalFare": 3339800,
                    "totalTax": 701800,
                    "markupValue": 0,
                    "agencyMarkupValue": 0
                }
                ],
                "contactInfos": [],
                "travelerInfos": [],
                "timeToLive": null,
                "supplierBookingStatus": "PENDING",
                "passengerNameRecords": "",
                "etickets": "",
                "cancellationFee": 0,
                "cancellationNotes": null,
                "cancellationBy": null,
                "cancellationDate": null,
                "discountAmount": 0,
                "discountVoucherCode": null,
                "discountVoucherName": null,
                "discountRedeemId": null,
                "discountRedeemCode": null,
                "discountDate": null,
                "additionalFee": null,
                "taxPersonalInfoContact": null,
                "bookingNote": null,
                "internalBookingNote": null,
                "promotionID": null,
                "reasonCodePaymentFailed": null,
                "bookingFinalStatus": null,
                "bookingIssuedType": null,
                "deleted": null,
                "onlyPayLater": false,
                "allowHold": true,
                "refundable": false,
                "ownerBooking": false,
                "showPayLaterOption": true,
                "showPayNowOption": true
            },
            "groupPricedItineraries": [
                {
                "groupId": "061f0408-ddb8-4462-ada0-d7aacac4154f",
                "airline": "VJ",
                "airlineName": "VietJet Air",
                "airSupplier": "VJ",
                "fightNo": "135",
                "flightType": "DOMESTIC",
                "roundType": "ROUNDTRIP",
                "originLocationCode": "HAN",
                "originLocationName": "Sân bay Nội Bài",
                "originCity": "Hà Nội",
                "originCountryCode": null,
                "originCountry": null,
                "destinationLocationCode": "SGN",
                "destinationLocationName": "Sân bay Tân Sơn Nhất",
                "destinationCity": "Hồ Chí Minh",
                "destinationCountryCode": null,
                "destinationCountry": null,
                "requiredFields": null,
                "aircraft": "Airbus A321",
                "vnaArea": null,
                "arrivalDateTime": "2021-08-16T07:20:00Z",
                "returnDateTime": null,
                "departureDateTime": "2021-08-16T05:10:00Z",
                "totalPricedItinerary": 1,
                "pricedItineraries": [
                    {
                    "sequenceNumber": "ibe4754299335928434",
                    "directionInd": "DEPARTURE",
                    "ticketType": "ETICKET",
                    "validatingAirlineCode": "VJ",
                    "validatingAirlineName": "VietJet Air",
                    "fightNo": "135",
                    "airItineraryPricingInfo": {
                        "fareSourceCode": "domd879a3f6-f3cb-40d6-8e95-52dd0a7d47a5",
                        "fareType": "PUBLIC",
                        "divideInPartyIndicator": false,
                        "fareInfoReferences": null,
                        "itinTotalFare": {
                        "baseFare": {
                            "amount": 1319000,
                            "currencyCode": null,
                            "decimalPlaces": 2
                        },
                        "comboMarkup": null,
                        "equivFare": {
                            "amount": 0,
                            "currencyCode": null,
                            "decimalPlaces": 2
                        },
                        "serviceTax": {
                            "amount": 350900,
                            "currencyCode": null,
                            "decimalPlaces": 2
                        },
                        "totalFare": {
                            "amount": 1669900,
                            "currencyCode": null,
                            "decimalPlaces": 2
                        },
                        "totalTax": {
                            "amount": 0,
                            "currencyCode": null,
                            "decimalPlaces": 2
                        },
                        "totalPaxFee": {
                            "amount": 0,
                            "currencyCode": null,
                            "decimalPlaces": 2
                        }
                        },
                        "adultFare": {
                        "passengerTypeQuantities": {
                            "code": "ADT",
                            "quantity": 1
                        },
                        "fareBasisCodes": null,
                        "passengerFare": {
                            "baseFare": {
                            "amount": 1319000,
                            "currencyCode": null,
                            "decimalPlaces": 2
                            },
                            "comboMarkup": null,
                            "equivFare": null,
                            "serviceTax": {
                            "amount": 350900,
                            "currencyCode": null,
                            "decimalPlaces": 2
                            },
                            "taxes": null,
                            "totalFare": {
                            "amount": 1669900,
                            "currencyCode": null,
                            "decimalPlaces": 2
                            },
                            "totalPaxFee": {
                            "amount": 0,
                            "currencyCode": null,
                            "decimalPlaces": 2
                            },
                            "surcharges": [
                            {
                                "amount": 0,
                                "indicator": "Ticket fee per segment",
                                "type": "Ticket fee per segment"
                            }
                            ]
                        }
                        },
                        "childFare": null,
                        "infantFare": null
                    },
                    "originDestinationOptions": [
                        {
                        "originLocationCode": "HAN",
                        "originLocationName": "Sân bay Nội Bài",
                        "originCity": "Hà Nội",
                        "originDateTime": "2021-08-16T05:10:00Z",
                        "destinationLocationCode": "SGN",
                        "destinationLocationName": "Sân bay Tân Sơn Nhất",
                        "destinationCity": "Hồ Chí Minh",
                        "destinationDateTime": "2021-08-16T07:20:00Z",
                        "flightDirection": "D",
                        "journeyDuration": 130,
                        "flightSegments": [
                            {
                            "departureAirportLocationCode": "HAN",
                            "departureAirportLocationName": "Sân bay Nội Bài",
                            "departureCity": "Hà Nội",
                            "departureDateTime": "2021-08-16T05:10:00Z",
                            "arrivalAirportLocationCode": "SGN",
                            "arrivalAirportLocationName": "Sân bay Tân Sơn Nhất",
                            "arrivalCity": "Hồ Chí Minh",
                            "arrivalDateTime": "2021-08-16T07:20:00Z",
                            "cabinClassCode": "L1_ECO",
                            "cabinClassName": "ECONOMY",
                            "cabinClassText": "Economy",
                            "eticket": true,
                            "flightNumber": "135",
                            "journeyDuration": 130,
                            "marketingAirlineCode": "VJ",
                            "marriageGroup": null,
                            "mealCode": null,
                            "adultBaggage": null,
                            "childBaggage": null,
                            "infantBaggage": null,
                            "operatingAirline": {
                                "code": "VJ",
                                "name": "VietJet Air",
                                "equipment": null,
                                "flightNumber": "135"
                            },
                            "resBookDesignCode": "L1_ECO",
                            "seatsRemaining": null,
                            "stopQuantity": 0,
                            "stopQuantityInfo": null,
                            "flightDirection": "D",
                            "fareCode": null,
                            "fareBasicCode": null,
                            "supplierJourneyKey": "FE1G3mI6J96guNcAzJB8ySOHAwhKeuKrPN1RLIvlkec0JkXEWMPy6ItOC426vmwQR43zYvZ9J8VI6zaG7lw0LKmEHsO80BsCMC3Wd8iolbƒTmtG8M6L7bPi0uz2tkYAvXDMXc9HUGkG8lApWnPe3xpTBrE0U39yauxXCYdc1n9FtG7gDƒ01dSwfrBCjwi0vgtFCse3gS3k17xSKp05Uw44REYTvb82JA3bgQdkƒBFAmNfeceBsSG9xMBDMdYNrMIO¥oiODBDxq5ƒz06gIaktCwk0PN8BM5mGwƒ2LgRBYV0JrBwBdrM6oOcgDgC4OYyLgrDH9Knfns1ƒgDj27Ac0HAXbdbZ7XqkrzKbM4r9Q8cg8X47a9lNO4KƒqIvTnUvEY8M0c1wwuOOHYJTsJABLzVPo3kahvuxmO3QlZuBy4fOB8MXrƒzbqks9wZ46RcMmvj8rz2U¥hysKqksRuCInqmdWYetrTHeziXe1Hj2i44979g=",
                            "supplierFareKey": null,
                            "aircraft": "Airbus A321"
                            }
                        ],
                        "cabinClassName": "ECONOMY"
                        }
                    ],
                    "cabinClassName": "ECONOMY",
                    "validReturnCabinClasses": null,
                    "baggageItems": [
                        {
                        "id": "air-tickets.baggage-items.vietnam.vj.economy.baggage.adult.free",
                        "name": "7kg xách tay",
                        "code": "air-tickets.baggage-items.vietnam.vj.economy.baggage.adult.free",
                        "amount": 0,
                        "serviceType": "BAGGAGE",
                        "fareCode": null,
                        "direction": null,
                        "note": ""
                        }
                    ],
                    "mealItems": null,
                    "passportMandatory": true,
                    "onlyPayLater": false,
                    "allowHold": true,
                    "refundable": false
                    }
                ],
                "tourCode": null,
                "osiCode": null
                },
                {
                "groupId": "59136e62-a451-491c-bf57-1495a5eb8053",
                "airline": "VJ",
                "airlineName": "VietJet Air",
                "airSupplier": "VJ",
                "fightNo": "176",
                "flightType": "DOMESTIC",
                "roundType": "ROUNDTRIP",
                "originLocationCode": "SGN",
                "originLocationName": "Sân bay Tân Sơn Nhất",
                "originCity": "Hồ Chí Minh",
                "originCountryCode": null,
                "originCountry": null,
                "destinationLocationCode": "HAN",
                "destinationLocationName": "Sân bay Nội Bài",
                "destinationCity": "Hà Nội",
                "destinationCountryCode": null,
                "destinationCountry": null,
                "requiredFields": null,
                "aircraft": "Airbus A321",
                "vnaArea": null,
                "arrivalDateTime": "2021-08-24T07:35:00Z",
                "returnDateTime": null,
                "departureDateTime": "2021-08-24T05:25:00Z",
                "totalPricedItinerary": 1,
                "pricedItineraries": [
                    {
                    "sequenceNumber": "ibe4754299329767108",
                    "directionInd": "DEPARTURE",
                    "ticketType": "ETICKET",
                    "validatingAirlineCode": "VJ",
                    "validatingAirlineName": "VietJet Air",
                    "fightNo": "176",
                    "airItineraryPricingInfo": {
                        "fareSourceCode": "dom389dca01-c0fd-466b-8a98-daaa4d5a06d4",
                        "fareType": "PUBLIC",
                        "divideInPartyIndicator": false,
                        "fareInfoReferences": null,
                        "itinTotalFare": {
                        "baseFare": {
                            "amount": 1319000,
                            "currencyCode": null,
                            "decimalPlaces": 2
                        },
                        "comboMarkup": null,
                        "equivFare": null,
                        "serviceTax": {
                            "amount": 350900,
                            "currencyCode": null,
                            "decimalPlaces": 2
                        },
                        "totalFare": {
                            "amount": 1669900,
                            "currencyCode": null,
                            "decimalPlaces": 2
                        },
                        "totalTax": {
                            "amount": 0,
                            "currencyCode": null,
                            "decimalPlaces": 2
                        },
                        "totalPaxFee": {
                            "amount": 0,
                            "currencyCode": null,
                            "decimalPlaces": 2
                        }
                        },
                        "adultFare": {
                        "passengerTypeQuantities": {
                            "code": "ADT",
                            "quantity": 1
                        },
                        "fareBasisCodes": null,
                        "passengerFare": {
                            "baseFare": {
                            "amount": 1319000,
                            "currencyCode": null,
                            "decimalPlaces": 2
                            },
                            "comboMarkup": null,
                            "equivFare": null,
                            "serviceTax": {
                            "amount": 350900,
                            "currencyCode": null,
                            "decimalPlaces": 2
                            },
                            "taxes": null,
                            "totalFare": {
                            "amount": 1669900,
                            "currencyCode": null,
                            "decimalPlaces": 2
                            },
                            "totalPaxFee": {
                            "amount": 0,
                            "currencyCode": null,
                            "decimalPlaces": 2
                            },
                            "surcharges": [
                            {
                                "amount": 0,
                                "indicator": "Ticket fee per segment",
                                "type": "Ticket fee per segment"
                            }
                            ]
                        }
                        },
                        "childFare": null,
                        "infantFare": null
                    },
                    "originDestinationOptions": [
                        {
                        "originLocationCode": "HAN",
                        "originLocationName": "Sân bay Nội Bài",
                        "originCity": "Hà Nội",
                        "originDateTime": "2021-08-24T05:25:00Z",
                        "destinationLocationCode": "SGN",
                        "destinationLocationName": "Sân bay Tân Sơn Nhất",
                        "destinationCity": "Hồ Chí Minh",
                        "destinationDateTime": "2021-08-24T07:35:00Z",
                        "flightDirection": "R",
                        "journeyDuration": 130,
                        "flightSegments": [
                            {
                            "departureAirportLocationCode": "SGN",
                            "departureAirportLocationName": "Sân bay Tân Sơn Nhất",
                            "departureCity": "Hồ Chí Minh",
                            "departureDateTime": "2021-08-24T05:25:00Z",
                            "arrivalAirportLocationCode": "HAN",
                            "arrivalAirportLocationName": "Sân bay Nội Bài",
                            "arrivalCity": "Hà Nội",
                            "arrivalDateTime": "2021-08-24T07:35:00Z",
                            "cabinClassCode": "L1_ECO",
                            "cabinClassName": "ECONOMY",
                            "cabinClassText": "Economy",
                            "eticket": true,
                            "flightNumber": "176",
                            "journeyDuration": 130,
                            "marketingAirlineCode": "VJ",
                            "marriageGroup": null,
                            "mealCode": null,
                            "adultBaggage": null,
                            "childBaggage": null,
                            "infantBaggage": null,
                            "operatingAirline": {
                                "code": "VJ",
                                "name": "VietJet Air",
                                "equipment": null,
                                "flightNumber": "176"
                            },
                            "resBookDesignCode": "L1_ECO",
                            "seatsRemaining": null,
                            "stopQuantity": 0,
                            "stopQuantityInfo": null,
                            "flightDirection": "R",
                            "fareCode": null,
                            "fareBasicCode": null,
                            "supplierJourneyKey": "qPHglSL8tSGƒ3tYhxs32uoafExuaR6¥D8DPJRmgypKWbSPECY06rnAXXpKJGOuZb7NEUz4HasidS6Kcff52bObVg9sDEUOLmHkeV1TaDv58k1CDTNƒyCESrKIDxxmqYUmuLSƒffYjj90rjE3zanJvDlCWjzbJ0DBYAszIKjG¥o7RMqlwoq6wrrJdOd4WNgPiooIUl4X14bZwOJmwqCDLLQDkqSQEcF1¥9rRzwbHQskz1QbtcUSpjbSrCyzB¥dsN4QEz0q6cFXltqF¥kr1pa¥HPƒqJkPVl35AkZjpH5n9KIQrPeVQbFskIp3Qi¥Mgc3S¥gfRBdNwWHAGFWU00HmhtmMI5uEEJCxEvhs28wq2yƒQi9U0HMXqWHfKhaRG788ƒLgXn3nIiM¥T514T9ƒWW0uv1wckVgDkdYKN4X9Dzi1oF0lhKTUlinhfxz3NPh2VdhI¥Hg2f6ƒb3Zz1Ggt8Kl2bKz15PdYBNJvd3j4h314KYP9g=",
                            "supplierFareKey": null,
                            "aircraft": "Airbus A321"
                            }
                        ],
                        "cabinClassName": "ECONOMY"
                        }
                    ],
                    "cabinClassName": "ECONOMY",
                    "validReturnCabinClasses": null,
                    "baggageItems": [
                        {
                        "id": "air-tickets.baggage-items.vietnam.vj.economy.baggage.adult.free",
                        "name": "7kg xách tay",
                        "code": "air-tickets.baggage-items.vietnam.vj.economy.baggage.adult.free",
                        "amount": 0,
                        "serviceType": "BAGGAGE",
                        "fareCode": null,
                        "direction": null,
                        "note": ""
                        }
                    ],
                    "mealItems": null,
                    "passportMandatory": true,
                    "onlyPayLater": false,
                    "allowHold": true,
                    "refundable": false
                    }
                ],
                "tourCode": null,
                "osiCode": null
                }
            ],
            "hotelAvailability": null,
            "hotelProductPayload": null,
            "hotelProduct": null,
            "offlineBooking": null,
            "travelerInfo": null,
            "isPerBookingType": true
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

## 4.API lấy thông tin tiện ích được mua kèm

!!! info "GET: /api/air-tickets/ssr-offer/{bookingNumber}"

    Lấy thông tin tiện ích được mua kèm

### Parameter

=== "Parameters"
    ???+ example "Parameter"

        - bookingNumber (String, Required)

            !!! quote ""

                Mã tham chiếu đến booking

=== "Example"

    ?bookingNumber=`ADCO2107201223969`

### Response

#### Code 200

> OK

=== "Model"
    ???+ example "Model"
        `Chỉ định danh những trường/field cần thiết`

        - bookingNumber (String, Optional),

            !!! quote "" 

                Mã dùng tham chiếu đến booking. Mã này là duy nhất.
        

        - departSsrOfferItems (SSROfferItem, Optional)

            !!! quote 

                Các tiện ích cho vé chiều đi
            
            - departureAirportLocationCode (String, Optional)
                
                !!! quote ""

                    Mã định danh sân bay tại điểm khởi hành
            
            - arrivalAirportLocationCode (String, Optional)

                !!! quote ""

                    Mã định danh sân bay tại điểm đến

            - departureDateTime (String, Optional) 

                !!! quote ""

                    Ngày giờ khởi hành
            
            - arrivalDateTime (String, Optional)

                !!! quote ""

                    Ngày giờ đến
            
            - ssrItems (Array[SSRItem], Optional)

                !!! quote ""

                    Danh sách tiện ích hữu dụng

                - amount (Number, Optional)

                    !!! quote ""

                        Giá tiền

                - code (String, Optional)

                    !!! quote ""

                        Mã định danh tiện ích mua thêm của nhà cung cấp

                -~~direction (String, Optional)~~

                - id (String, Optional)

                    !!! quote ""

                        Mã định danh tiện ích. Mỗi mã là duy nhất không trùng trong cùng 1 hành trình

                - name (String, Optional)

                    !!! quote ""

                        Tên tiện ích dịch vụ mua thêm

                - serviceType (String, Optional)

                    !!! quote ""

                        Loại tiện ích dịch vụ mua thêm

                        - `BAGGAGE`: hành lý mua thêm

                        - `MEAL`: bữa ăn kèm

            - returnSsrOfferItems (SSROfferItem, Optional)

                !!! quote ""

                    Các tiện ích cho vé chiều về

                    Tương tự tiện ích cho vé chiều đi

        - duration (Integer, Optional),
        - errors (Array[Error], Optional),
        - infos (Array[Info], Optional),
        - success (Boolean, Optional),
        - textMessage (String, Optional)

=== "Example"
    ```json

    {
        "bookingNumber" : "ADCO2107201223969",
        "departSsrOfferItems" : [ {
            "arrivalAirportLocationCode" : "SGN",
            "arrivalAirportLocationName" : null,
            "arrivalCity" : null,
            "arrivalDateTime" : "2021-08-16T07:20:00.000Z",
            "departureAirportLocationCode" : "HAN",
            "departureAirportLocationName" : null,
            "departureCity" : null,
            "departureDateTime" : "2021-08-16T05:10:00.000Z",
            "ssrItems" : [ {
            "amount" : 170500.0,
            "code" : "Bag 15kgs",
            "direction" : null,
            "fareCode" : null,
            "id" : "SSRCode_2ae7cd77-cab3-497a-ac75-c7fcc8d9e9ed",
            "name" : "15kg ký gửi",
            "serviceType" : "BAGGAGE"
            }, {
            "amount" : 192500.0,
            "code" : "Bag 20kgs",
            "direction" : null,
            "fareCode" : null,
            "id" : "SSRCode_9f675ebc-bfbb-45c9-8c10-c8d07f45581f",
            "name" : "20kg ký gửi",
            "serviceType" : "BAGGAGE"
            }, {
            "amount" : 258500.0,
            "code" : "Bag 25kgs",
            "direction" : null,
            "fareCode" : null,
            "id" : "SSRCode_6a599353-8494-4286-91fa-a6941c5a945b",
            "name" : "25kg ký gửi",
            "serviceType" : "BAGGAGE"
            }, {
            "amount" : 368500.0,
            "code" : "Bag 30kgs",
            "direction" : null,
            "fareCode" : null,
            "id" : "SSRCode_f8ebf8bb-65d6-463c-942a-bed90f74b1fa",
            "name" : "30kg ký gửi",
            "serviceType" : "BAGGAGE"
            }, {
            "amount" : 423500.0,
            "code" : "Bag 35kgs",
            "direction" : null,
            "fareCode" : null,
            "id" : "SSRCode_25435c21-500c-45c5-92e8-b70227fad826",
            "name" : "35kg ký gửi",
            "serviceType" : "BAGGAGE"
            }, {
            "amount" : 478500.0,
            "code" : "Bag 40kgs",
            "direction" : null,
            "fareCode" : null,
            "id" : "SSRCode_a28ed2a2-df6e-4493-aa27-d46290424a32",
            "name" : "40kg ký gửi",
            "serviceType" : "BAGGAGE"
            }, {
            "amount" : 412500.0,
            "code" : "Oversize 20kgs",
            "direction" : null,
            "fareCode" : null,
            "id" : "SSRCode_3d767edf-7441-43e1-b4b0-80f0d6770f6e",
            "name" : "Quá khổ 20kgs ký gửi",
            "serviceType" : "BAGGAGE"
            }, {
            "amount" : 588500.0,
            "code" : "Oversize 30kgs",
            "direction" : null,
            "fareCode" : null,
            "id" : "SSRCode_6071aea5-06fd-4669-968c-769c8813d8b9",
            "name" : "Quá khổ 30kgs ký gửi",
            "serviceType" : "BAGGAGE"
            } ]
        } ],
        "duration" : 3686,
        "errors" : null,
        "infos" : null,
        "returnSsrOfferItems" : [ {
            "arrivalAirportLocationCode" : "HAN",
            "arrivalAirportLocationName" : null,
            "arrivalCity" : null,
            "arrivalDateTime" : "2021-08-24T07:35:00.000Z",
            "departureAirportLocationCode" : "SGN",
            "departureAirportLocationName" : null,
            "departureCity" : null,
            "departureDateTime" : "2021-08-24T05:25:00.000Z",
            "ssrItems" : [ {
            "amount" : 170500.0,
            "code" : "Bag 15kgs",
            "direction" : null,
            "fareCode" : null,
            "id" : "SSRCode_53563c43-daf8-44d6-ab75-d1e8056addf9",
            "name" : "15kg ký gửi",
            "serviceType" : "BAGGAGE"
            }, {
            "amount" : 192500.0,
            "code" : "Bag 20kgs",
            "direction" : null,
            "fareCode" : null,
            "id" : "SSRCode_18395f19-1eae-4741-9974-bc4154340351",
            "name" : "20kg ký gửi",
            "serviceType" : "BAGGAGE"
            }, {
            "amount" : 258500.0,
            "code" : "Bag 25kgs",
            "direction" : null,
            "fareCode" : null,
            "id" : "SSRCode_5beb92dd-f178-4b8c-b77f-777527540a36",
            "name" : "25kg ký gửi",
            "serviceType" : "BAGGAGE"
            }, {
            "amount" : 368500.0,
            "code" : "Bag 30kgs",
            "direction" : null,
            "fareCode" : null,
            "id" : "SSRCode_543dcfb6-a75c-4c5b-bfb3-ab425b20dbc7",
            "name" : "30kg ký gửi",
            "serviceType" : "BAGGAGE"
            }, {
            "amount" : 423500.0,
            "code" : "Bag 35kgs",
            "direction" : null,
            "fareCode" : null,
            "id" : "SSRCode_f5d90a7c-a1dd-4eaa-8a85-478195a5e8e2",
            "name" : "35kg ký gửi",
            "serviceType" : "BAGGAGE"
            }, {
            "amount" : 478500.0,
            "code" : "Bag 40kgs",
            "direction" : null,
            "fareCode" : null,
            "id" : "SSRCode_89bd8235-e51d-47bb-a712-3cf0e24c68da",
            "name" : "40kg ký gửi",
            "serviceType" : "BAGGAGE"
            }, {
            "amount" : 412500.0,
            "code" : "Oversize 20kgs",
            "direction" : null,
            "fareCode" : null,
            "id" : "SSRCode_ed1d0701-08e8-4e05-94f1-19d0e71d89fb",
            "name" : "Quá khổ 20kgs ký gửi",
            "serviceType" : "BAGGAGE"
            }, {
            "amount" : 588500.0,
            "code" : "Oversize 30kgs",
            "direction" : null,
            "fareCode" : null,
            "id" : "SSRCode_aeb6be0b-3ff0-498a-8093-d1bfaa3d4f9f",
            "name" : "Quá khổ 30kgs ký gửi",
            "serviceType" : "BAGGAGE"
            } ]
        } ],
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

## 5.API lấy thông tin bảo hiểm trễ chuyến

!!! info "GET: /gtd_service_inventory/api/insurance/available_plans"

    Lấy thông bảo hiểm trễ chuyến

### Parameter

=== "Parameters"
    ???+ example "Parameter"

        - adult (Integer, Required)

            !!! quote ""

                Số lượng người lớn
        
        - child (Integer, Required)

            !!! quote ""

                Số lượng trẻ em
            
        - infant (Integer, Required)

            !!! quote ""

                Số lượng em bé
        
        - departureDate (String, Required)

            !!! quote ""

                Ngày đi

                Định dạng: yyyy-mm-dd

        - returnDate (String, Optional)

            !!! quote ""

                Ngày về

                Định dạng: yyyy-mm-dd

        - fromLocation (String, Required)

            !!! quote ""

                Mã sân bay chiều đi

        - toLocation (String, Required)

            !!! quote ""

                Mã sân bay chiều về

=== "Example"

    ?adult=`2`&child=`0`&infant=`0`&departureDate=`2022-03-12`&fromLocation=`SGN`&returnDate=`2022-03-20`&toLocation=`HAN`

### Response

#### Code 200

> OK

=== "Model"
    ???+ example "Model"
        `Chỉ định danh những trường/field cần thiết`

        - data(Array[InsuranceDTO], Optional)

            !!! quote ""

                Danh sách thông tin bảo hiểm trễ chuyến

            - InsuranceDTO

                - id (String, Required) 

                    !!! quote ""

                        ID định danh cho bảo hiểm trễ chuyến
                
                - amount (Double, Required)

                    !!! quote ""

                        Tổng tiền bảo hiểm trễ chuyến

                - code (String, Required)

                    !!! quote ""

                        Mã định danh cho bảo hiểm trễ chuyến
                
                - name (String, Required)

                    !!! quote ""

                        Tên gói bảo hiểm trễ chuyến

                - extras

                    !!! quote ""

                        Thông tin của gói bảo hiểm trễ chuyến

                    - chargeType (String, Required)

                        !!! quote ""

                            Loại hình của gói 

                    - content (String, Optional)

                        !!! quote ""

                            Nội dung của gói bảo hiểm trễ  chuyến

                    - description (String, Optional)

                        !!! quote ""

                            Nội dung mô tả của gói bảo hiểm trễ  chuyến
                    
                    - pricingBreakdown:

                        - currencyCode (String, Optional)

                            !!! quote ""

                                Mã tiền tệ

                        - minAge (Integer, Optional)
                        - maxAge (Integer, Optional)    

        - errors (Integer, Required),
        - success (Boolean, Required),
        - message (String, Optional)

=== "Example"
    ```json

    {
        "success": true,
        "data": [
            {
            "id": "BV-GTD-TRAVEL DELAY-WD",
            "name": "Bảo hiểm trễ chuyến bay",
            "code": "INS2_VNBVGTDTD_TD",
            "amount": 140000,
            "extras": {
                "chargeType": "PER_PASSENGER",
                "description": "Cá nhân, Bảo hiểm Trễ chuyến bay",
                "pricingBreakdown": {
                "minAge": 0,
                "maxAge": 85,
                "gender": "B",
                "currencyCode": "VND",
                "premiumAmount": 70000
                },
                "content": "<table><tr><td colspan=\"2\">Bồi thường ngay lập tức 888.000 VNĐ khi chuyến bay trễ hơn hai (2) tiếng liên tục so với giờ khởi hành ban đầu.<td>\n<tr><td colspan=\"2\" height=\"5px\"></td></tr>\n<tr><td colspan=\"2\" height=\"5px\"></td></tr>\n<br>\n<tr><td colspan=\"2\" style=\"font-size:0.8em\"><p>Bảo hiểm trễ chuyến bay được cung cấp bởi Bảo hiểm Bảo Việt. Vui lòng vào <a href=\"https://appuat.baoviet.com.vn:7784/Uploads/product/TravelCare/Flight%20Easy_Policy%20Wording%20-%20EN.VN_17.06.2019.pdf\" target=\"_blank\" style=\"color:blue;text-decoration:underline;\">đây</a> để xem điều kiện điều khoản\n</td></tr>\n</table>\n\n"
            }
            }
        ],
        "message": "",
        "errorCode": 0
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

## 6.API cập nhật thông tin booking và giữ chỗ

!!! info "POST: /api/air-tickets/add-booking-traveller"

    Cập nhật các thông tin: Hành khách, người liên hệ, thông tin xuất hóa đơn, ... và yêu cầu giữ chỗ

### Request Body

=== "Model"
    ???+ example "Request Body"

        - bookingNumber (String, Optional),

            !!! quote "" 

                Mã dùng tham chiếu đến booking. Mã này là duy nhất.

        - bookingContacts (Array[BookingContact], Required)    

            !!! quote ""

                Danh sách thông tin liên hệ

                - email (String, Required)

                    !!! quote ""

                        Email của người liên hệ
                
                - firstName (String, Required)

                    !!! quote ""

                        Tên và tên đệm của người liên hệ

                - surName (String, Required)

                    !!! quote ""

                        Họ của người liên hệ

                - phoneNumber1 (String, Required)

                    !!! quote ""

                        Số điện thoại của người liên hệ
                
                - phoneNumber1 (String, Required)

                    !!! quote ""

                        Số điện thoại của người liên hệ
            
        - bookingTravelerInfos (Array(BookingTravelerInfoDTO), Required) 

            !!! quote ""

                Danh sách thông tin hàng khách, dịch vụ đi kèm

                - serviceRequests(Array[BookingServiceRequestDTO], Optional)

                    !!! quote ""

                        Thông tin các dịch vụ đi kèm

                        *Chú ý: Nếu SSR là bảo hiểm trễ chuyến khi bay 2 chiều thì bắt buộc phải mua cả 2 chứ không thể mua 1 chiều bỏ 1 chiều. Giá bảo hiểm trễ chuyến không bao gồm trẻ sơ sinh chỉ tính người lớn + trẻ em
                    
                    - bookingDirection (String, Required)

                        !!! quote ""

                            Chiều đi

                            - Hành lý
                            
                                - `DEPARTURE` : chiều đi

                                - `RETURN`: chiều về
                            
                            - Bảo hiểm 

                                - `ONEWAY`: cho 1 chiều

                                - `ROUNDTRIP`: cho cả 2 chiều

                    - ssrAmount (Number, Required)

                        !!! quote ""

                            Giá tiền

                    - ssrCode (String, Required)

                        !!! quote ""

                            Mã định danh tiện ích mua thêm của nhà cung cấp

                    - ssrId (String, Required)

                        !!! quote ""

                            Mã định danh tiện ích. Mỗi mã là duy nhất không trùng trong cùng 1 hành trình

                    - ssrName (String, Required)

                        !!! quote ""

                            Tên tiện ích dịch vụ mua thêm

                    - serviceType (String, Required)

                        !!! quote ""

                            Loại tiện ích dịch vụ mua thêm

                            - `BAGGAGE`: hành lý mua thêm

                            - `MEAL`: bữa ăn kèm

                            - `INSURANCE`: bảo hiểm trễ chuyến
                    
                    - fareCode(String, Required)

                        !!! quote ""

                            Thông tin mã định danh hành trình
                    
                    - bookingNumber (String, Required),

                        !!! quote "" 

                            Mã dùng tham chiếu đến booking. Mã này là duy nhất.
            
                - traveler (BookingTravelerDTO, Required) 

                    !!! quote ""

                        Thông tin hành khách

                    - adultType (String, Required)

                        !!! quote ""

                            Thể hiện loại hành khách

                            - `ADT`: người lớn

                            - `CHD`: trẻ em

                            - `INF`: em bé
                        
                    - firstName(String, Required)

                        !!! quote ""

                            Tên và tên đệm

                    - gender (String, Required)

                        !!! quote ""

                            Giới tính

                            - `MALE`: nam

                            - `FEMALE`: nữ

                            - `BOY`: bé trai

                            - `GIRL`: bé gái

                            - `INF`: trẻ sơ sinh
                    
                    - memberCard (Boolean, Optional)

                        !!! quote ""

                            Có thẻ thành viên hay không

                    - memberCardType (String, Optional)

                        !!! quote ""

                            Loại thẻ thành viên
                    
                    - memberCardNumber (String, Optional)

                        !!! quote ""

                            Số thẻ thành viên

                    - surName (String, Required)

                        !!! quote ""
                            
                            Họ
                    - bookingNumber(String, Required)

                    - dob (String, Optional)

                        !!! quote ""

                            Ngày tháng năm sinh

        - taxReceiptRequest(TaxReceiptRequest, Required)

            !!! quote ""

                Thông tin mã định danh hành trình

            - bookingNumber (String, Required)

            - taxReceiptRequest(Boolean, Required)

                !!! quote ""

                    Thông tin có xuất hóa đơn không
                
            - taxAddress1 (String, Optional)

                !!! quote ""

                    Địa chỉ xuất hóa đơn

            - taxCompanyName (String, Optional)

                !!! quote ""

                    Tên công ty xuất hóa đơn
            
            - taxNumber (String, Optional)

                !!! quote ""

                    Mã số thuế

            - taxPersonalInfoContact (String, Optional)

                !!! quote ""

                    Tên cá nhân liên hệ

=== "Example"

    ```json
        {
            "bookingNumber": "ADCO2107211224000",
            "bookingContacts": [
                {
                    "email": "dang.nguyenhai@gotadi.com",
                    "firstName": "HAI DANG",
                    "phoneCode1": "84",
                    "phoneNumber1": "0932909474",
                    "surName": "NGUYEN",
                    "bookingNumber": "ADCO2107211224000"
                }
            ],
            "bookingTravelerInfos": [
                {
                "traveler": {
                    "adultType": "ADT",
                    "documentNumber": null,
                    "documentExpiredDate": null,
                    "firstName": "HAI DANG",
                    "gender": "MALE",
                    "memberCard": false,
                    "memberCardType": null,
                    "memberCardNumber": null,
                    "surName": "NGUYEN",
                    "bookingNumber": "ADCO2107211224000",
                    "dob": null
                },
                "serviceRequests": [
                    {
                    "bookingDirection": "DEPARTURE",
                    "bookingNumber": "ADCO2107211224000",
                    "fareCode": "domdb93cf84-d023-4222-9b56-f096d9e5df35",
                    "serviceType": "BAGGAGE",
                    "ssrAmount": 258500,
                    "ssrCode": "Bag 25kgs",
                    "ssrId": "SSRCode_941c225f-0cb5-4e46-a669-5a75d7d3afde",
                    "ssrName": "25kg ký gửi"
                    },
                    {
                    "bookingNumber": "ADCO2107211224000",
                    "bookingDirection": "ONEWAY",
                    "fareCode": "domdb93cf84-d023-4222-9b56-f096d9e5df35",
                    "serviceType": "INSURANCE",
                    "ssrCode": "INS1_VNBVGTDTD_TD",
                    "ssrId": "BV-GTD-TRAVEL DELAY-WD-1W",
                    "ssrAmount": 35000,
                    "ssrName": "B%E1%BA%A3o%20hi%E1%BB%83m%20tr%E1%BB%85%20chuy%E1%BA%BFn%20bay"
                    }
                ]
                }
            ],
            "osiCodes": [],
            "taxReceiptRequest": {
                "bookingNumber": "ADCO2107211224000",
                "taxReceiptRequest": false
            }
        }

    ```

### Response

#### Code 200

> OK

=== "Model"
    ???+ example "Model"
        `Chỉ định danh những trường/field cần thiết`

        - bookingCode (BookingCode, Optional) 

            !!! quote ""

                Cập nhật thông tin và giữ chỗ 

            
            - bookingCode (String, Optional)

                !!! quote "" 

                    Mã dùng mô tả các thông tin cơ bản của booking

            - bookingNumber (String, Optional)

                !!! quote "" 

                    Mã dùng tham chiếu đến booking. Mã này là duy nhất.

        - duration (Integer, Optional),
        - errors (Array[Error], Optional),
        - infos (Array[Info], Optional),
        - success (Boolean, Optional),
        - textMessage (String, Optional)

=== "Example"
    ```json

    {
        "bookingCode" : {
            "bookingCode" : "BOD::210721::86088c0e-d84e-46e1-913c-5d450418a951",
            "bookingNumber" : "ADCO2107211224000"
        },
        "duration" : 15948,
        "errors" : null,
        "infos" : null,
        "isSuccess" : null,
        "otpServiceRes" : {
            "duration" : null,
            "errors" : null,
            "expDate" : null,
            "expired" : null,
            "fullQuota" : null,
            "infos" : null,
            "isSuccess" : null,
            "lifeTimeInMin" : null,
            "matched" : null,
            "notFound" : false,
            "outOfSlot" : null,
            "phoneNumber" : null,
            "serviceID" : null,
            "smsServiceAvailable" : null,
            "success" : true,
            "tag" : null,
            "textMessage" : null,
            "used" : null,
            "verificationCode" : null
        },
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

## 7.API xác nhận voucher

!!! info "GET: /api/payments/voucher/validate"

    Validate voucher cho booking cụ thể

### Request Body

=== "Model"
    ???+ example "Request Body"

        - bookingNumber (String, Required)

            !!! quote ""

                Mã định danh booking
        
        - voucherCode (String, Required)

            !!! quote ""

                Mã giảm giá

=== "Example"
    ```json
    
    {
        "bookingNumber": "ADCO2203011523483",
        "voucherCode": "AXOLXHLp"
    }

    ```

### Response

#### Code 200

> OK

=== "Model"
    ???+ example "Model"
        `Chỉ định danh những trường/field cần thiết`

        - bookingNumber (String)

            !!! quote ""

                Mã định dang booking

        - discountAmount (Double)

            !!! quote ""

                Số tiền giảm

        - trackingCode (String)

            !!! quote ""

                Mã định danh cho booking có voucher

        - voucherCode (String)

            !!! quote ""

                Mã giảm giá 
        
        - voucherValid (Boolean)

            !!! quote ""

                Mã giảm giá hợp lệ

        - duration (Integer, Optional),
        - errors (Array[Error], Optional),
        - infos (Array[Info], Optional),
        - success (Boolean, Optional),
        - textMessage (String, Optional)

=== "Example"
    ```json

    {
        "isSuccess": true,
        "duration": 3896,
        "textMessage": null,
        "errors": null,
        "infos": null,
        "bookingNumber": "ADCO2203011523483",
        "voucherCode": "AXOLXHLp",
        "voucherValid": true,
        "trackingCode": "track_xbhwiFai1HNQNCQLe2PmvdxJu/rd5zEG7NGuvjHI5CY=",
        "discountAmount": 1000,
        "percentOff": null,
        "type": "AMOUNT",
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