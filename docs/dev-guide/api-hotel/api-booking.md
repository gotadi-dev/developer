# Document Hotel API Booking 

## 1. API Kiểm tra tình trạng phòng (checkout) 

!!! info "POST: /api/v3/hotel/checkout"
    Trả về kết quả tình trạng của phòng 

### Request Body 
=== "Model"
    ???+ example "Request Body"
        - tripId (String, Required)

            !!! quote ""

                Mã định danh kết quả search-all-rate, lấy từ kết quả trả về search-all-rates

        - roomId (String, Required)

            !!! quote "" 
                
                Mã định danh phòng, lấy từ kết quả trả về search-all-rates

        - ratePlanId (String, Required)

            !!! quote "" 
                
                Mã định danh tùy chọn giá, lấy từ kết quả trả về search-all-rates

        - metadata (String, Required)

            !!! quote "" 
                
                Thông tin mở rộng 

            - customer-ip (String, Required)
            
                !!! quote ""

                    Địa chỉ IP của người dùng cuối 

=== "Example"
    ```json 
    {
        "tripId": "QtmwRXkB5hnyw2pfga4b",
        "roomId": "201866846",
        "ratePlanId": "209445837",
        "metadata": {
            "customer-ip": "118.xxx.xxx.xxx"
        }
    }
    ```

### Response 
#### Code 200
> OK

=== "Model" 
    ???+ example "Model"
        - result (CheckoutResult, Optional)

            !!! quote ""

                Thông tin kết quả trả về 

            - status (string, optional) = ['AVAILABLE', 'PRICE_CHANGED', 'SOLD_OUT', 'UNKNOWN']

                !!! quote "" 

                    Thông tin xác định trạng thái của phòng 
                    
                    - `AVAILABLE`: Phòng đang tồn tại sẳn sàng để book 

                    - `PRICE_CHANGED`: Giá phòng đã bị thay đổi, thông tin giá thay đổi được cập nhật trong HotelProduct 

                    - `SOLD_OUT`: Phòng đã hết 

                    - `UNKNOWN`: Không xác định trạng thái phòng 

            - hotelProduct (HotelProduct, optional),

                !!! quote ""

                    Thông tin phòng trả về 

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

                - amenities (Array[Attribute], optional),

                    !!! quote "" 
                            
                        Mảng đối tượng chứa thông tin tiện nghi của khách sạn 

                    - id (string, optional),
                    
                    !!! quote "" 
                        
                        Mã tiện nghi khách sạn 

                    - name (string, optional),
                    
                        !!! quote "" 
                        
                            Tên của tiện nghi khách sạn

                    - ~~value (string, optional)~~

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

                - customerIp (string, optional),

                    !!! quote "" 
                            
                        Thông tin địa chỉ ip của người dùng cuối

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

                - productId (string, optional),

                    !!! quote "" 
                        
                        Mã định danh sản phẩm

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
                                
                                Mô tả các hình thức phạt khi hủy đặt phòng với tùy chọn giá này. Xem thêm chi tiết ở tài liệu api search-all-rates.

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

                - searchId (string, optional),

                    !!! quote "" 

                        - Mã tham chiếu đến kết quả tìm kiếm (search-best-rate)


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

                - supplier (string, optional) = ['EXPEDIA', 'AXISROOM', 'BEDLINKER'],

                    !!! quote "" 
                        
                        Nguồn khách sạn 
                
                - themes (Array[Attribute], optional),

                    !!! quote "" 

                        Mảng đối tượng chứa thông tin về chủ đề của khách sạn 

                    - id (string, optional),
                    
                        !!! quote "" 
                        
                            Mã định chủ đề  

                    - name (string, optional),
                    
                        !!! quote "" 
                        
                            Tên chủ đề 

                    - ~~value (string, optional)~~

                - tripId (string, optional)

                    !!! quote "" 

                        Mã liên kết đến kết quả search-all-rates 

        - duration (Integer, Optional)
        - success (Integer, Bool)
        - infos (Array[InfosDTO], Optional)
        - errors (Array[ErrorsDTO], Optional)
        - textMessage (String, Optional)

=== "Example"
    ```json 
    {
        "result": {
            "hotelProduct": {
                "address": {
                    "city": "TP.Hồ Chí Minh",
                    "countryCode": "VN",
                    "countryName": "",
                    "lineOne": "132 - 134 Đồng Khởi, Q.1",
                    "lineTow": "",
                    "postalCode": "70000",
                    "stateProvinceCode": "",
                    "stateProvinceName": ""
                },
                "amenities": [
                    {
                        "id": "2063",
                        "name": "Quầy tiếp tân 24 giờ",
                        "value": ""
                    },
                    {
                        "id": "2065",
                        "name": "Trung tâm hành chính, văn phòng",
                        "value": ""
                    },
                    {
                        "id": "3",
                        "name": "Bar/lounge",
                        "value": ""
                    },
                    {
                        "id": "2537",
                        "name": "Số lượng nhà hàng:  - 2",
                        "value": ""
                    },
                    {
                        "id": "4003",
                        "name": "Trông giữ/bảo quản hành lý",
                        "value": ""
                    }
                ],
                "checkin": {
                    "beginTime": "02:00 PM",
                    "endTime": "02:00 PM"
                },
                "checkout": {
                    "endTime": "12:00"
                },
                "currency": "VND",
                "customerIp": "",
                "descriptions": [
                    {
                        "id": "1",
                        "name": "overview",
                        "value": "<p><strong>1 giường cỡ queen hoặc 2 giường đơn</strong></p><p>35 mét vuông</p><br/><p><b>Internet</b> - Wifi miễn phí <br /> <p><b>Giải trí</b> - TV LCD 46 inch với các kênh truyền hình cáp</p><p><b>Ăn uống</b> - Dụng cụ pha cà phê/trà, minibar, dịch vụ phòng 24 giờ và nước đóng chai miễn phí</p> <p><b>Giấc ngủ</b> - Dịch vụ dọn phòng buổi tối</p> <p><b>Phòng tắm</b> - Phòng tắm riêng với vòi sen/bồn tắm kết hợp, áo choàng tắm và dép đi trong nhà</p><p><b>Tiện nghi</b> - Két an toàn, báo miễn phí các ngày trong tuần và bàn</p><p><b>Tiện nghi</b> - Máy điều hòa nhiệt độ và dịch vụ dọn phòng hàng ngày</p><p><b>Thông tin cần biết</b> - Không có bộ trải giường</p> <p>Không hút thuốc</p>"
                    }
                ],
                "fees": [],
                "images": [
                    {
                        "caption": "Ảnh nổi bật",
                        "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/cbe48cdd_z.jpg",
                        "position": 1
                    },
                    {
                        "caption": "Tiền sảnh",
                        "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/580dff7d_z.jpg",
                        "position": 2
                    },
                    {
                        "caption": "Phòng",
                        "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/394e4ca3_z.jpg",
                        "position": 3
                    },
                    {
                        "caption": "Phòng",
                        "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/b6e21a19_z.jpg",
                        "position": 4
                    },
                    {
                        "caption": "Phòng",
                        "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/03f49af2_z.jpg",
                        "position": 5
                    },
                    {
                        "caption": "Phòng",
                        "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/7563f797_z.jpg",
                        "position": 6
                    },
                    {
                        "caption": "Phòng",
                        "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/d7bc598e_z.jpg",
                        "position": 7
                    },
                    {
                        "caption": "Phòng",
                        "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/698c8de8_z.jpg",
                        "position": 8
                    },
                    {
                        "caption": "Phòng",
                        "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/eb9050ee_z.jpg",
                        "position": 9
                    },
                    {
                        "caption": "Phòng",
                        "link": "https://i.travelapi.com/hotels/1000000/490000/481700/481659/e9786e7a_z.jpg",
                        "position": 10
                    }
                ],
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
                    }
                ],
                "language": "vi",
                "latitude": 10.776629,
                "longitude": 106.702459,
                "policies": [
                    {
                        "id": "1",
                        "name": "know_before_you_go",
                        "value": "<ul>  <li>Chỉ khách đã đăng ký được lưu trú tại phòng. </li><li>Khách không được phép mang vật nuôi, bao gồm cả vật nuôi hỗ trợ người khuyết tật, vào nơi lưu trú này. </li><li>Nơi lưu trú cho biết đang áp dụng các biện pháp vệ sinh tăng cường và an toàn cho khách.</li><li>Vệ sinh nơi lưu trú bằng dung dịch khử trùng, những bề mặt thường có nhiều tiếp xúc được vệ sinh bằng dung dịch khử trùng giữa các lần lưu trú và giặt tấm trải giường và khăn ở nhiệt độ tối thiểu 60°C.</li><li>Giãn cách xã hội, nhân viên mang thiết bị bảo hộ cá nhân, kiểm tra nhiệt độ cho nhân viên định kỳ, kiểm tra nhiệt độ cho khách và cung cấp nước rửa tay cho khách.</li><li>Tất cả phòng đều được để trống tối thiểu 24 giờ giữa mỗi lượt khách.</li><li>Nơi lưu trú xác nhận đang áp dụng biện pháp vệ sinh và khử trùng theo quy định Intertek Cristal (Chuyên viên bên thứ 3 - Toàn cầu).</li>\n </ul>"
                    }
                ],
                "productId": "1235",
                "propertyCategory": {
                    "id": "",
                    "name": ""
                },
                "propertyId": null,
                "propertyName": "Khách sạn Continental Sài Gòn",
                "rank": 11042,
                "rating": {
                    "ratingGuest": {
                        "amenities": "",
                        "cleanliness": "",
                        "comfort": "",
                        "condition": "",
                        "count": 995,
                        "location": "",
                        "neighborhood": "",
                        "overall": "",
                        "quality": "",
                        "recommendationPercent": "80.2",
                        "score": "",
                        "service": "",
                        "value": ""
                    },
                    "ratingProperty": {
                        "rating": "4.0",
                        "type": "Star"
                    }
                },
                "rooms": [
                    {
                        "descriptions": [],
                        "id": "201866846",
                        "images": null,
                        "name": "Phòng Superior",
                        "ratePlans": [
                            {
                                "amenities": [
                                    {
                                        "id": "2205",
                                        "name": "Bữa sáng buffet",
                                        "value": ""
                                    },
                                    {
                                        "id": "1073742786",
                                        "name": "Bữa sáng miễn phí",
                                        "value": ""
                                    },
                                    {
                                        "id": "2109",
                                        "name": "Đậu xe miễn phí",
                                        "value": ""
                                    },
                                    {
                                        "id": "2192",
                                        "name": "Wifi miễn phí",
                                        "value": ""
                                    }
                                ],
                                "basePrice": 1043681.0,
                                "basePriceBeforePromo": 0.0,
                                "bedGroups": [
                                    {
                                        "configurations": [],
                                        "description": "2 giường đơn",
                                        "id": "37341"
                                    },
                                    {
                                        "configurations": [],
                                        "description": "1 giường cỡ queen",
                                        "id": "37310"
                                    }
                                ],
                                "breakfastIncluded": true,
                                "cancelFree": true,
                                "cancelFreeBeforeDate": "26/07/2021 00:00",
                                "cancelPenalties": [
                                    {
                                        "amount": "",
                                        "currency": "VND",
                                        "description": "",
                                        "endDate": "09/08/2021 18:00",
                                        "nights": "",
                                        "percent": "100%",
                                        "startDate": "26/07/2021 18:00",
                                        "type": "PERCENT"
                                    }
                                ],
                                "fees": {},
                                "paxPrice": [
                                    {
                                        "nightPrices": [
                                            {
                                                "nightKey": "0",
                                                "nightPriceDetails": [
                                                    {
                                                        "name": "base_rate",
                                                        "value": 1043681.0,
                                                        "valueByHotelCurrency": "1043681.0 VND"
                                                    },
                                                    {
                                                        "name": "tax_and_service_fee",
                                                        "value": 161771.0,
                                                        "valueByHotelCurrency": "161771.0 VND"
                                                    }
                                                ]
                                            }
                                        ],
                                        "paxInfo": {
                                            "adultQuantity": 2,
                                            "childAges": [],
                                            "childQuantity": 0,
                                            "infantQuantity": 0
                                        }
                                    }
                                ],
                                "promo": true,
                                "promoDescription": "Tiết kiệm 30%",
                                "ratePlanId": "209445837",
                                "ratePlanName": "",
                                "refundable": true,
                                "taxAndFees": 161771.0,
                                "totalPrice": 1205452.0,
                                "totalPriceByHotelCurrency": 1205452.0,
                                "totalRooms": 5
                            }
                        ],
                        "roomArea": {
                            "squareFeet": 377,
                            "squareMeters": 35
                        }
                    }
                ],
                "searchId": "eyJzZWFyY2hJZCI6IiIsImNoZWNrSW4iOiIyMDIxLTA4LTA5IiwiY2hlY2tPdXQiOiIyMDIxLTA4LTEwIiwicGF4SW5mb3MiOlt7ImFkdWx0UXVhbnRpdHkiOjIsImNoaWxkUXVhbnRpdHkiOjAsImluZmFudFF1YW50aXR5IjowLCJjaGlsZEFnZXMiOltdfV0sImxhbmd1YWdlIjoidmkiLCJjdXJyZW5jeSI6IlZORCIsInN1cHBsaWVyIjoiRVhQRURJQSIsInNlYXJjaENvZGUiOiIxNzgyNjIiLCJzZWFyY2hUeXBlIjoiTVVMVElfQ0lUWV9WSUNJTklUWSJ9",
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
                "supplier": "EXPEDIA",
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
                "tripId": "etfDRXkBXssFjzQQN4yE"
            },
            "status": "AVAILABLE"
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

## 2. API Khởi tạo booking

!!! info "POST: /api/v3/hotel/create-draft-booking"
    Khởi tạo booking 

### Request Body 
=== "Model"
    ???+ example "Request Body"
        - tripId (String, Required)

            !!! quote ""

                Mã định danh kết quả search-all-rate, lấy từ kết quả trả về search-all-rates

        - roomId (String, Required)

            !!! quote "" 
                
                Mã định danh phòng, lấy từ kết quả trả về search-all-rates

        - ratePlanId (String, Required)

            !!! quote "" 
                
                Mã định danh tùy chọn giá, lấy từ kết quả trả về search-all-rates

        - metadata (String, Required)

            !!! quote "" 
                
                Thông tin mở rộng 

            - customer-ip (String, Required)
            
                !!! quote ""

                    Địa chỉ IP của người dùng cuối 

=== "Example"
    ```json 
    {
        "tripId": "QtmwRXkB5hnyw2pfga4b",
        "roomId": "201866846",
        "ratePlanId": "209445837",
        "metadata": {
            "customer-ip": "118.xxx.xxx.xxx"
        }
    }
    ```

### Response
#### Code 200
=== "Model" 
    ???+ example "Model"
        - result (Booking, optional)

            !!! quote ""
        
                Thông tin booking đã tạo 
        
            - additionalFee (number, optional),

                !!! quote ""
        
                    Các khoản phí khác 

            - agencyCode (string, optional),

                !!! quote "" 

                    Mã đại lý. Mã dùng tham chiếu đến tác giả của booking

            - ~~agencyMarkupValue (number, optional),~~

            - agentCode (string, optional),

                !!! quote "" 

                    Mã nhân viên đại lý. Mã dùng tham chiếu đến tác giả của booking

            - agentId (integer, optional),

                !!! quote "" 

                    Id nhân viên đại lý

            - agentName (string, optional),

                !!! quote "" 

                    Tên nhân viên đại lý 

            - baseFare (number, optional),

                !!! quote ""
        
                    Giá phòng chưa bao gồm thuế phí 

            - bookBy (string, optional),

                !!! quote ""
        
                    Người đặt booking 

            - bookByCode (string, optional),

                !!! quote ""
        
                    Mã người đặt 

            - bookingCode (string, optional),

                !!! quote "" 

                    Mã dùng mô tả các thông tin cơ bản của booking

            - bookingDate (string, optional),

                !!! quote "" 

                    Ngày tạo booking 

            - bookingNote (string, optional),

                !!! quote "" 

                    Ghi chú của booking 

            - bookingNumber (string, optional),

                !!! quote "" 

                    Mã dùng tham chiếu đến booking. Mã này là duy nhất.

            - bookingType (string, optional) = ['DOME', 'INTE'],

                !!! quote "" 

                    Xác định điểm đến là trong nước hay quốc tế 

                    - `DOME`: Trong nước 

                    - `INTE`: Quốc tế 

            - branchCode (string, optional),

                !!! quote "" 

                    Mã chi nhánh 

            - cancellationBy (string, optional),

                !!! quote "" 

                    Hủy đặt phòng bởi ...

            - cancellationDate (string, optional),

                !!! quote "" 

                    Ngày hủy đặt phòng 

            - cancellationFee (number, optional),

                !!! quote "" 

                    Phí hủy đặt phòng 

            - cancellationNotes (string, optional),

                !!! quote "" 

                    Ghi chú hủy 

            - channelType (string, optional) = ['ONLINE', 'OFFLINE'],

                !!! quote "" 

                    Loại kênh đặt phòng

            - commissionValue (number, optional),

                !!! quote "" 

                    Giá trị hoa hồng 

            - createdBy (string, optional),

                !!! quote "" 

                    Người tạo booking

            - createdDate (string, optional),

                !!! quote "" 

                    Ngày tạo booking 

            - customerCode (string, optional),

                !!! quote "" 

                    Mã khách hàng 

            - customerEmail (string, optional),

                !!! quote "" 

                    Email của khách hàng 

            - customerFirstName (string, optional),

                !!! quote "" 

                    Họ của khách hàng 

            - customerId (integer, optional),

                !!! quote "" 

                    Id của khách hàng 

            - customerLastName (string, optional),

                !!! quote "" 

                    Tên của khách hàng 

            - customerPhoneNumber1 (string, optional),

                !!! quote "" 

                    Số điện thoại 1 của khách hàng 

            - customerPhoneNumber2 (string, optional),

                !!! quote "" 

                    Số điện thoại 2 của khách hàng 

            - departureDate (string, optional),

                !!! quote "" 

                    Ngày nhận phòng 

            - discountAmount (number, optional),

                !!! quote "" 

                    Số tiền được giảm 

            - discountDate (string, optional),

                !!! quote "" 

                    Ngày sử dụng mã giảm giá 

            - discountRedeemCode (string, optional),

                !!! quote "" 

                    Mã liên kết đổi thưởng 

            - discountRedeemId (string, optional),

                !!! quote "" 

                    Id định danh liên kết đổi thường 

            - discountTrackingCode (string, optional),

                !!! quote "" 

                    Mã theo dõi thông tin giảm giá 

            - discountVoucherCode (string, optional),

                !!! quote "" 

                    Mã voucher 

            - discountVoucherName (string, optional),

                !!! quote "" 

                    Tên voucher 

            - ~~equivFare (number, optional),~~

            - ~~fromCity (string, optional),~~

            - ~~fromLocationCode (string, optional),~~

            - ~~fromLocationName (string, optional),~~

            - id (integer, optional),
            
                !!! quote "" 

                    Id của booking 

            - ~~internalBookingNote (string, optional),~~

            - ~~isDeleted (boolean, optional),~~

            - issuedBy (string, optional),

                !!! quote "" 

                    Xuất phòng bởi ...

            - issuedByCode (string, optional),

                !!! quote "" 

                    Mã người xuất phòng 

            - issuedDate (string, optional),

                !!! quote "" 

                    Ngày xuất phòng 

            - issuedStatus (string, optional) = ['PENDING', 'TICKET_ON_PROCESS', 
            'SUCCEEDED', 'FAILED'],

                !!! quote "" 

                    Trạng thái xuất phòng 

                    - `PENDING`: Đợi xuất phòng 

                    - `TICKET_ON_PROCESS`: Xuất phòng đang được xử lý 

                    - `SUCCEEDED`: Xuất phòng thành công 

                    - `FAILED`: Xuất phòng thất bại 
            
            - ~~markupValue (number, optional),~~

            - orgCode (string),

                !!! quote "" 

                    Mã tổ chức 

            - partnerOrderId (string, optional),

                !!! quote "" 

                    Id định danh đặt hàng của đối tác 

            - partnerRequestId (string, optional),

                !!! quote "" 

                    Id định danh request của đối tác 

            - paymentBy (string, optional),

                !!! quote "" 

                    Thanh toán bởi ...

            - paymentByCode (string, optional),

                !!! quote "" 

                    Mã người thanh toán 

            - paymentDate (string, optional),

                !!! quote "" 

                    Thời gian thanh toán 

            - paymentFee (number, optional),

                !!! quote "" 

                    Phí thanh toán 

            - paymentRefNumber (string, optional),

                !!! quote "" 

                    Mã tham chiếu thanh toán 

            - paymentStatus (string, optional) = ['SUCCEEDED', 'FAILED', 'REFUNDED', 'PENDING'],

                !!! quote "" 

                    Trạng thái thanh toán 

                    - `PENDING`: Chờ thanh toán 

                    - `SUCCEEDED`: Thanh toán thành công 

                    - `FAILED`: Thanh toán thất bại 

                    - `REFUNDED`: Hoàn tiền 

            - paymentTotalAmount (number, optional),

                !!! quote "" 

                    Tổng số tiền thanh toán 

            - paymentType (string, optional) = ['BALANCE', 'CREDIT', 'ATM_DEBIT', 'VNPAYQR', 'VIETTELPAY', 'MOMO', 'ZALO', 'AIRPAY', 'PAYOO', 'CASH', 'TRANSFER', 'PARTNER', 'OTHER'],

                !!! quote "" 

                    Hình thức thanh toán 

            - ~~promotionID (Array[string], optional),~~

            - ~~reconciliationType (string, optional) = ['NEW', 'ALREADY_RECONCILIATION'],~~

            - refundAmount (number, optional),

                !!! quote "" 

                    Số tiền hoàn trả 

            - refundBy (string, optional),

                !!! quote "" 

                    Người hoàn trả 

            - refundByCode (string, optional),

                !!! quote "" 

                    Mã của người thực hiện hoàn trả  

            - refundDate (string, optional),

                !!! quote "" 

                    Ngày hoàn trả 

            - ~~refundNextVoidDate (string, optional),~~

            - returnDate (string, optional),

                !!! quote "" 

                    Ngày trả phòng 

            - roundType (string, optional) = ['RoundTrip],

            - saleChannel (string, optional) = ['B2B', 'B2C', 'B2B2C', 'B2C_WEB', 'B2C_WEB_APP', 'B2C_MOBILE'],

                !!! quote "" 

                    Kênh phân phối 

            - serviceTax (number, optional),

                !!! quote "" 

                    Thuế và phí

            - ~~sessionSearchId (string, optional),~~

            - status (string, optional) = ['PENDING', 'BOOKING_ON_PROCESS', 'BOOKED', 'FAILED', 'CANCELLED', 'EXPIRED'],

                !!! quote "" 

                    Trạng thái của booking 

                    - `PENDING`: Chờ xác nhận booking 

                    - `BOOKING_ON_PROCESS`: Booking đang được xử lý 

                    - `BOOKED`: Booking đã được xác nhận 

                    - `FAILED`: Booking thất bại 

                    - `EXPIRED`: Booking hết hạn 

                    - `CANCELLED`: Booking đã bị hủy 

            - supplierType (string, optional) = ['AIR', 'HOTEL', 'TOURS', 'TRAIN', 'SHIP', 'OTHER'],

                !!! quote "" 

                    Loại sản phẩm 

            - ~~tags (string, optional),~~

            - taxAddress1 (string, optional),

                !!! quote "" 

                    Địa chỉ xuất hóa đơn dòng 1

            - taxAddress2 (string, optional),

                !!! quote "" 

                    Địa chỉ xuất hóa đơn dòng 2

            - taxCompanyName (string, optional),

                !!! quote "" 

                    Tên công ty xuất hóa đơn 

            - taxNumber (string, optional),

                !!! quote "" 

                    Mã số thuế cần xuất hóa đơn 

            - taxPersonalInfoContact (string, optional),

                !!! quote "" 

                    Người nhận hóa đơn 

            - taxReceiptRequest (boolean, optional),

                !!! quote "" 

                    Yêu cầu xuất hóa đơn hay không 

            - timeToLive (string, optional),

                !!! quote "" 

                    Thời gian chờ thanh toán, sau thời gian này trạng thái của booking sẽ chuyển sang `EXPIRED`

            - ~~timeToLiveExpired (string, optional),~~

            - toCity (string, optional),

                !!! quote "" 

                    Tên tỉnh, thành phố nơi đặt phòng khách sạn 

            - toLocationCode (string, optional),

                !!! quote "" 

                    Mã định danh khách sạn 

            - toLocationName (string, optional),

                !!! quote "" 

                    Tên khách sạn 

            - totalFare (number, optional),

                !!! quote "" 

                    Tổng giá phòng 

            - ~~totalSsrValue (number, optional),~~

            - totalTax (number, optional),

                !!! quote "" 

                    Tổng số tiền thuế phí 

            - updatedBy (string, optional),

                !!! quote "" 

                    Người cập nhật 

            - updatedDate (string, optional),

                !!! quote "" 

                    Ngày cập nhật 

            - ~~vat (number, optional)~~

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

## 3. API Lấy chi tiết booking

!!! info "POST: /api/products/booking-detail"
    Lấy thông tin chi tiết của booking 

### Parameters 
???+ example "Parameters"

    - bookingNumber `query` (string, required),

        !!! quote ""

            Mã tham chiếu đến booking


### Response 
#### Code 200
> OK

=== "Model"
    ???+ example "Model"
        - id (string, optional),

            !!! quote ""

                Mã định danh chi tiết booking 

        - agencyCode (string, optional),

            !!! quote "" 

                Mã đại lý. Mã dùng tham chiếu đến tác giả của booking

        - agentCode (string, optional),

            !!! quote "" 

                Mã nhân viên đại lý. Mã dùng tham chiếu đến tác giả của booking

        - bookingCode (string, optional),

            !!! quote "" 

                Mã dùng mô tả các thông tin cơ bản của booking
                
        - bookingDate (string, optional),

            !!! quote "" 

                Ngày tạo booking 

        - bookingInfo (BookingInfo, optional),

            !!! quote "" 

                Thông tin booking 

            - additionalFee (number, optional),

                !!! quote ""
        
                    Các khoản phí khác 

            - agencyCode (string, optional),

                !!! quote "" 

                    Mã đại lý. Mã dùng tham chiếu đến tác giả của booking

            - ~~agencyMarkupInfos (Array[BookingAgencyMarkupInfo], optional),~~

            - ~~agencyMarkupValue (number, optional),~~

            - agentCode (string, optional),

                !!! quote "" 

                    Mã nhân viên đại lý. Mã dùng tham chiếu đến tác giả của booking

            - agentId (integer, optional),

                !!! quote "" 

                    Id nhân viên đại lý

            - agentName (string, optional),

                !!! quote "" 

                    Tên nhân viên đại lý 

            - allowHold (boolean, optional),

                !!! quote "" 

                    Cho phép giữ phòng hay không 

                    `true`: cho phép giữ phòng 

                    `false`: Không cho phép giữ phòng 

            - baseFare (number, optional),

                !!! quote ""
        
                    Giá phòng chưa bao gồm thuế phí 

            - bookBy (string, optional),

                !!! quote ""
        
                    Người đặt booking 

            - bookByCode (string, optional),

                !!! quote ""
        
                    Mã người đặt 

            - bookingCode (string, optional),

                !!! quote "" 

                    Mã dùng mô tả các thông tin cơ bản của booking

            - bookingDate (string, optional),

                !!! quote "" 

                    Ngày tạo booking 

            - ~~bookingIssuedType (string, optional) = ['INSTANT_BOOKING', 'CONFIRM_OFFLINE'],~~

            - bookingNote (string, optional),

                !!! quote "" 

                    Ghi chú của booking 

            - bookingNumber (string, optional),

                !!! quote "" 

                    Mã dùng tham chiếu đến booking. Mã này là duy nhất.

            - bookingType (string, optional) = ['DOME', 'INTE'],

                !!! quote "" 

                    Xác định điểm đến là trong nước hay quốc tế 

                    - `DOME`: Trong nước 

                    - `INTE`: Quốc tế 

            - branchCode (string, optional),

                !!! quote "" 

                    Mã chi nhánh 

            - cancellationBy (string, optional),

                !!! quote "" 

                    Hủy đặt phòng bởi ...

            - cancellationDate (string, optional),

                !!! quote "" 

                    Ngày hủy đặt phòng 

            - cancellationFee (number, optional),

                !!! quote "" 

                    Phí hủy đặt phòng 

            - cancellationNotes (string, optional),

                !!! quote "" 

                    Ghi chú hủy 

            - channelType (string, optional) = ['ONLINE', 'OFFLINE'],

                !!! quote "" 

                    Loại kênh đặt phòng

            - contactInfos (Array[BookingContactInfo], optional),

                !!! quote "" 

                    Mảng đối tượng chứ thông tin người liên hệ 

                - bookingNumber (string, optional),

                    !!! quote ""

                        Mã tham chiếu đến booking

                - contactLevel (string, optional) = ['PRIMARY', 'SECONDARY', 'OTHER'],

                    !!! quote ""

                        Cấp của người liên hệ 

                - contactType (string, optional) = ['CUSTOMER', 'AGENCY'],
                
                    !!! quote ""

                        Loại của người liên hệ 

                - email (string, optional),

                    !!! quote ""

                        Địa chỉ email 

                - firstName (string, optional),

                    !!! quote ""

                        Tên đêm và tên người liên hệ 
                        
                - phoneCode1 (string, optional),

                    !!! quote ""

                        Mã quốc gia 

                - phoneNumber1 (string, optional),

                    !!! quote ""

                        Số điện thoại 1

                - surName (string, optional)

                    !!! quote ""

                        Họ người liên hệ 

            - customerCode (string, optional),

                !!! quote "" 

                    Mã khách hàng 

            - customerEmail (string, optional),

                !!! quote "" 

                    Email của khách hàng 

            - customerFirstName (string, optional),

                !!! quote "" 

                    Họ của khách hàng 

            - customerId (integer, optional),

                !!! quote "" 

                    Id của khách hàng 

            - customerLastName (string, optional),

                !!! quote "" 

                    Tên của khách hàng 

            - customerPhoneNumber1 (string, optional),

                !!! quote "" 

                    Số điện thoại 1 của khách hàng 

            - customerPhoneNumber2 (string, optional),

                !!! quote "" 

                    Số điện thoại 2 của khách hàng 

            - ~~deleted (boolean, optional),~~

            - departureDate (string, optional),

                !!! quote "" 

                    Ngày nhận phòng 

            - discountAmount (number, optional),

                !!! quote "" 

                    Số tiền được giảm 
            
            - discountDate (string, optional),

                !!! quote "" 

                    Ngày sử dụng mã giảm giá 
            
            - discountRedeemCode (string, optional),

                !!! quote "" 

                    Mã liên kết đổi thưởng 
            
            - discountRedeemId (string, optional),

                !!! quote "" 

                    Id định danh liên kết đổi thường 
            
            - discountVoucherCode (string, optional),

                !!! quote "" 

                    Mã voucher 
            
            - discountVoucherName (string, optional),

                !!! quote "" 

                    Tên voucher
            
            - ~~displayPriceInfo (BookingPriceInfo, optional),~~
            
            - ~~equivFare (number, optional),~~

            - etickets (string, optional),

                !!! quote "" 

                    Mã liên kết với nhà cung cấp, được sử dụng để nhận phòng 

            - ~~fromCity (string, optional),~~

            - ~~fromLocationCode (string, optional),~~

            - ~~fromLocationName (string, optional),~~

            - id (integer, optional),

                !!! quote "" 

                    Id của booking 

            - ~~internalBookingNote (string, optional),~~

            - issuedByCode (string, optional),

                !!! quote "" 

                    Xuất phòng bởi ...

            - issuedDate (string, optional),

                !!! quote "" 

                    Ngày xuất phòng 

            - issuedStatus (string, optional) = ['PENDING', 'TICKET_ON_PROCESS', 'SUCCEEDED', 'FAILED'],

                !!! quote "" 

                    Trạng thái xuất phòng 

                    - `PENDING`: Đợi xuất phòng 

                    - `TICKET_ON_PROCESS`: Xuất phòng đang được xử lý 

                    - `SUCCEEDED`: Xuất phòng thành công 

                    - `FAILED`: Xuất phòng thất bại 

            - ~~markupValue (number, optional),~~

            - ~~onlyPayLater (boolean, optional),~~

            - orgCode (string, optional),

                !!! quote "" 

                    Mã tổ chức 

            - ownerBooking (boolean, optional),

                !!! quote "" 

                    Chủ sở hữu đặt chỗ 

            - passengerNameRecords (string, optional),

                !!! quote "" 

                    Mã liên kết với nhà cung cấp, được sử dụng để nhận phòng

            - paymentBy (string, optional),

                !!! quote "" 

                    Thanh toán bởi ...

            - paymentByCode (string, optional),

                !!! quote "" 

                    Mã người thanh toán 

            - paymentDate (string, optional),

                !!! quote "" 

                    Thời gian thanh toán 

            - paymentFee (number, optional),

                !!! quote "" 

                    Phí thanh toán 

            - paymentRefNumber (string, optional),

                !!! quote "" 

                    Mã tham chiếu thanh toán 

            - paymentStatus (string, optional) = ['SUCCEEDED', 'FAILED', 'REFUNDED', 'PENDING'],

                !!! quote "" 

                    Trạng thái thanh toán 

                    - `PENDING`: Chờ thanh toán 

                    - `SUCCEEDED`: Thanh toán thành công 

                    - `FAILED`: Thanh toán thất bại 

                    - `REFUNDED`: Hoàn tiền 

            - paymentTotalAmount (number, optional),

                !!! quote "" 

                    Tổng số tiền thanh toán 

            - paymentType (string, optional) = ['BALANCE', 'CREDIT', 'ATM_DEBIT', 'AIRPAY', 'VNPAYQR', 'VIETTELPAY', 'MOMO', 'ZALO', 'PAYOO', 'CASH', 'TRANSFER', 'PARTNER', 'OTHER'],

                !!! quote "" 

                    Hình thức thanh toán 

            - ~~promotionID (Array[string], optional),~~
            
            - ~~reasonCodePaymentFailed (string, optional),~~
            
            - refundBy (string, optional),

                !!! quote "" 

                    Người hoàn trả 

            - refundByCode (string, optional),

                !!! quote "" 

                    Mã của người thực hiện hoàn trả  
            
            - refundable (boolean, optional),

                !!! quote "" 

                    Ngày hoàn trả 
            
            - returnDate (string, optional),

                !!! quote "" 

                    Ngày trả phòng 
            
            - roundType (string, optional) = ['RoundTrip],
            
            - saleChannel (string, optional) = ['B2B', 'B2C', 'B2B2C', 'B2C_WEB', 'B2C_WEB_APP', 'B2C_MOBILE'],

                !!! quote "" 

                    Kênh phân phối 
            
            - serviceTax (number, optional),

                !!! quote "" 

                    Thuế và phí

            - ~~showPayLaterOption (boolean, optional),~~

            - ~~showPayNowOption (boolean, optional),~~

            - status (string, optional) = ['PENDING', 'BOOKING_ON_PROCESS', 'BOOKED', 'FAILED', 'CANCELLED', 'EXPIRED'],

                !!! quote "" 

                    Trạng thái của booking 

                    - `PENDING`: Chờ xác nhận booking 

                    - `BOOKING_ON_PROCESS`: Booking đang được xử lý 

                    - `BOOKED`: Booking đã được xác nhận 

                    - `FAILED`: Booking thất bại 

                    - `EXPIRED`: Booking hết hạn 

                    - `CANCELLED`: Booking đã bị hủy 

            - ~~supplierBookingStatus (string, optional),~~

            - supplierType (string, optional) = ['AIR', 'HOTEL', 'TOURS', 'TRAIN', 'SHIP', 'OTHER'],

                !!! quote "" 

                    Loại nhà cung cấp 

            - taxAddress1 (string, optional),

                !!! quote "" 

                    Địa chỉ xuất hóa đơn dòng 1

            - taxAddress2 (string, optional),

                !!! quote "" 

                    Địa chỉ xuất hóa đơn dòng 2

            - taxCompanyName (string, optional),

                !!! quote "" 

                    Tên công ty xuất hóa đơn 

            - taxNumber (string, optional),

                !!! quote "" 

                    Mã số thuế cần xuất hóa đơn 

            - taxPersonalInfoContact (string, optional),

                !!! quote "" 

                    Người nhận hóa đơn 

            - taxReceiptRequest (boolean, optional),

                !!! quote "" 

                    Yêu cầu xuất hóa đơn hay không 

            - timeToLive (string, optional),

                !!! quote "" 

                    Thời gian chờ thanh toán, sau thời gian này trạng thái của booking sẽ chuyển sang `EXPIRED`

            - toCity (string, optional),

                !!! quote "" 

                    Tên tỉnh, thành phố nơi đặt phòng khách sạn 

            - toLocationCode (string, optional),

                !!! quote "" 

                    Mã định danh khách sạn 

            - toLocationName (string, optional),

                !!! quote "" 

                    Tên khách sạn 
                    
            - totalFare (number, optional),

                !!! quote "" 

                    Tổng giá phòng 

            - ~~totalSsrValue (number, optional),~~

            - totalTax (number, optional),

                !!! quote "" 

                    Tổng số tiền thuế phí 

            - transactionInfos (Array[BookingTransactionInfo], optional),

                !!! quote "" 

                    Mảng đối tượng chứa thông tin giao dịch 

                - id (integer, optional),

                    !!! quote "" 

                        Id định danh giao dịch 

                - ~~agencyMarkupValue (number, optional),~~

                - allowHold (boolean, optional),

                    !!! quote "" 

                        Cho phép giữ phòng hay không 

                - bookingCode (string, optional),

                    !!! quote "" 

                        Mã dùng mô tả các thông tin cơ bản của booking

                - bookingDate (string, optional),

                    !!! quote "" 

                        Ngày tạo booking 

                - bookingDirection (string, optional) = ['TRIP'],

                - bookingNumber (string, optional),

                    !!! quote "" 

                        Mã dùng tham chiếu đến booking.

                - bookingRefNo (string, optional),

                    !!! quote "" 

                        Mã liên kết với nhà cung cấp 

                - channelType (string, optional) = ['ONLINE', 'OFFLINE'],

                    !!! quote "" 

                        Loại kênh bán 

                - checkIn (string, optional),

                    !!! quote "" 

                        Ngày nhận phòng 

                - checkOut (string, optional),

                    !!! quote "" 

                        Ngày trả phòng

                - destinationLocationCode (string, optional),

                    !!! quote "" 

                        Mã định danh khách sạn 
                
                - detail (string, optional),

                    !!! quote "" 

                        Tên khách sạn 

                - etickets (string, optional),

                    !!! quote "" 

                        Mã liên kết với nhà cung cấp, được sử dụng để nhận phòng 
                
                - issuedDate (string, optional),

                    !!! quote "" 

                        Ngày xuất phòng 

                - issuedStatus (string, optional) = ['PENDING', 'TICKET_ON_PROCESS', 'SUCCEEDED', 'FAILED'],

                    !!! quote "" 

                        Trạng thái xuất phòng 

                        - `PENDING`: Đợi xuất phòng 

                        - `TICKET_ON_PROCESS`: Xuất phòng đang được xử lý 

                        - `SUCCEEDED`: Xuất phòng thành công 

                        - `FAILED`: Xuất phòng thất bại 

                - ~~markupCode (string, optional),~~

                - ~~markupFormula (string, optional),~~

                - ~~markupKey (string, optional),~~

                - ~~markupValue (number, optional),~~

                - noAdult (integer, optional),

                    !!! quote "" 

                        Số người lớn 

                - noChild (integer, optional),

                    !!! quote "" 

                        Số trể em 

                - onlyPayLater (boolean, optional),

                    !!! quote "" 

                        Cho phép trả sau hay không 

                - passengerNameRecord (string, optional),

                    !!! quote "" 

                        Mã liên kết với nhà cung cấp, được sử dụng để nhận phòng 

                - paymentAmount (number, optional),

                    !!! quote "" 

                        Số tiền thanh toán 

                - productSeqNumber (string, optional),

                    !!! quote ""

                        Mã sản phẩm 

                - refundable (boolean, optional),

                    !!! quote "" 

                        Có hoàn tiền khi hủy phòng hay không 

                - saleChannel (string, optional) = ['B2B', 'B2C', 'B2B2C', 'B2C_WEB', 'B2C_WEB_APP', 'B2C_MOBILE'],

                    !!! quote "" 

                        Kênh phân phối 

                - serviceTax (number, optional),

                    !!! quote "" 

                        Thuế và phí

                - status (string, optional) = ['PENDING', 'BOOKING_ON_PROCESS', 'BOOKED', 'FAILED', 'CANCELLED', 'EXPIRED'],

                    !!! quote "" 

                        Trạng thái của booking 

                        - `PENDING`: Chờ xác nhận booking 

                        - `BOOKING_ON_PROCESS`: Booking đang được xử lý 

                        - `BOOKED`: Booking đã được xác nhận 

                        - `FAILED`: Booking thất bại 

                        - `EXPIRED`: Booking hết hạn 

                        - `CANCELLED`: Booking đã bị hủy 

                - supplierCode (string, optional),

                    !!! quote "" 

                        Mã nhà cung cấp 

                - supplierName (string, optional),

                    !!! quote "" 

                        Tên nhà cung cấp 

                - supplierType (string, optional) = ['AIR', 'HOTEL', 'TOURS', 'TRAIN', 'SHIP', 'OTHER']

                    !!! quote "" 

                        Loại sản phẩm 

                - totalFare (number, optional),
                
                    !!! quote ""

                        Tổng giá phòng 

                - totalTax (number, optional)

                    !!! quote ""

                        Tổng thuế và phí 
                
                - baseFare (number, optional),

                    !!! quote "" 

                        Giá phòng không bao gồm thuế phí 

            - travelerInfos (Array[BookingTravelerInfo], optional),

                !!! quote ""

                    Mảng đối tượng chứa thông tin người nhận phòng. Người nhận phòng phải là người lớn. Mỗi một phòng tương ứng với 1 phần tử của mảng.

                - bookingNumber (string),

                    !!! quote ""

                        Mã tham chiếu đến booking 

                - firstName (string),

                    !!! quote ""

                        Tên đêm và tên người nhận phòng 

                - surName (string)

                    !!! quote ""

                        Họ của người nhận phòng 

        - bookingNumber (string, optional),

            !!! quote "" 

                Mã dùng tham chiếu đến booking. Mã này là duy nhất.

        - bookingType (string, optional),

            !!! quote "" 

                Xác định điểm đến là trong nước hay quốc tế 

                - `DOME`: Trong nước 

                - `INTE`: Quốc tế 

        - branchCode (string, optional),

            !!! quote "" 

                Mã chi nhánh 

        - cacheType (string, optional) = ['HOTEL'],

        - ~~channelType (string, optional) = ['ONLINE', 'OFFLINE'],~~

            !!! quote "" 

                Loại kênh đặt phòng

        - ~~customerCode (string, optional),~~

            !!! quote "" 

                Mã khách hàng 

        - ~~groupPricedItineraries (Array[GroupPricedItinerary], optional),~~

        - ~~hotelAvailability (HotelAvailability, optional),~~

        - hotelProduct (HotelProduct, optional),

            !!! quote ""

                Đối tượng chứa thông tin phòng (Xem thêm ở response API checkout)

        - hotelProductPayload (HotelProductPayload, optional),

            !!! quote "" 

                Đối tượng chứa thông tin định danh sản phẩm

            - tripId (String, optional)

                !!! quote "" 

                    Mã định danh kết quả search-all-rate

            - roomId (String, optional)

                !!! quote ""

                    Mã định danh phòng 

            - ratePlanId (String, optional)

                !!! quote ""

                    Mã định danh tùy chọn giá 

        - ~~isPerBookingType (boolean, optional),~~

        - ~~markupType (string, optional),~~

        - ~~offlineBooking (OfflineBooking, optional),~~

        - orgCode (string, optional),

            !!! quote "" 

                Mã tổ chức 

        - saleChannel (string, optional) = ['B2B', 'B2C', 'B2B2C', 'B2C_WEB', 'B2C_WEB_APP', 'B2C_MOBILE'],

            !!! quote "" 

                Kênh phân phối 

        - supplierType (string, optional)  = ['AIR', 'HOTEL', 'TOURS', 'TRAIN', 'SHIP', 'OTHER'],

            !!! quote "" 

                Loại nhà cung cấp 

        - ~~travelerInfo (TravelerInfo, optional),~~
        - ~~updatedDate (string, optional)~~

=== "Example"
    ```json 
    {
        "id": "BOD::210510::b4176592-056a-452e-9244-f3d373927ceb",
        "updatedDate": "2021-05-10T02:33:33.346Z",
        "cacheType": "HOTEL",
        "orgCode": "A::1",
        "agencyCode": "A::1",
        "branchCode": null,
        "saleChannel": "B2C_WEB",
        "channelType": "ONLINE",
        "supplierType": "HOTEL",
        "bookingCode": "BOD::210510::b4176592-056a-452e-9244-f3d373927ceb",
        "bookingType": "DOME",
        "agentCode": null,
        "customerCode": "C::A::1|91968",
        "bookingNumber": "HDCO2105109318609",
        "bookingDate": "2021-05-10T02:33:33.345Z",
        "markupType": null,
        "bookingInfo": {
            "id": 9318609,
            "orgCode": "A::1",
            "agencyCode": "A::1",
            "saleChannel": "B2C_WEB",
            "channelType": "ONLINE",
            "supplierType": "HOTEL",
            "bookingCode": "BOD::210510::b4176592-056a-452e-9244-f3d373927ceb",
            "bookingType": "DOME",
            "agentCode": null,
            "agentId": null,
            "agentName": null,
            "branchCode": null,
            "customerCode": "C::A::1|91968",
            "customerId": 91968,
            "bookingNumber": "HDCO2105109318609",
            "roundType": "RoundTrip",
            "fromLocationCode": "481659",
            "fromLocationName": "Khách sạn Continental Sài Gòn",
            "fromCity": "TP.Hồ Chí Minh",
            "toLocationCode": "481659",
            "toLocationName": "Khách sạn Continental Sài Gòn",
            "toCity": "TP.Hồ Chí Minh",
            "status": "BOOKED",
            "bookingDate": "2021-05-10T02:33:33.345Z",
            "departureDate": "2021-07-22T17:00:00Z",
            "returnDate": "2021-07-23T17:00:00Z",
            "baseFare": 1043681.0,
            "equivFare": 0.0,
            "serviceTax": 161771.0,
            "vat": null,
            "totalFare": 1205452.0,
            "totalTax": 161771.0,
            "agencyMarkupValue": 0.0,
            "markupValue": 0.0,
            "totalSsrValue": 0.0,
            "paymentTotalAmount": 0.0,
            "paymentFee": 0.0,
            "paymentType": "OTHER",
            "paymentStatus": "PENDING",
            "paymentDate": null,
            "paymentRefNumber": null,
            "issuedStatus": "PENDING",
            "issuedDate": null,
            "customerFirstName": "THE HOAN",
            "customerLastName": "TRAN",
            "customerPhoneNumber1": "0399903620",
            "customerPhoneNumber2": null,
            "customerEmail": "tranthehoanis@gmail.com",
            "taxReceiptRequest": true,
            "taxCompanyName": "CÔNG TY TNHH DỊCH VỤ HÀNG KHÔNG HƯƠNG GIANG",
            "taxAddress1": "194 Nguyễn Thị Minh Khai, Phường Võ Thị Sáu, Quận 3, TP.HCM",
            "taxAddress2": null,
            "taxNumber": "0305130620",
            "paymentBy": null,
            "paymentByCode": null,
            "issuedByCode": null,
            "refundBy": null,
            "refundByCode": null,
            "bookBy": "tranthehoanis@gmail.com",
            "bookByCode": "C::A::1|91968",
            "displayPriceInfo": {
                "bookingNumber": "HDCO2105109318609",
                "baseFare": 1043681.0,
                "equivFare": 0.0,
                "serviceTax": 161771.0,
                "totalFare": 1043681.0,
                "totalTax": 161771.0,
                "agencyMarkupValue": 0.0,
                "markupValue": 0.0,
                "totalSsrValue": 0.0,
                "cancellationFee": 0.0,
                "paymentFee": 0.0,
                "discountAmount": 0.0,
                "additionalFee": 0.0,
                "additionalTaxPerTraveler": 0.0,
                "vat": null
            },
            "transactionInfos": [
                {
                    "id": 9318709,
                    "saleChannel": "B2C_WEB",
                    "channelType": "ONLINE",
                    "supplierType": "HOTEL",
                    "bookingCode": "HDCO2105109318609::E-481659::lIMfVHkB0y3GNIc_QS_f",
                    "bookingNumber": "HDCO2105109318609",
                    "status": "BOOKED",
                    "bookingDate": "2021-05-10T02:38:22.317Z",
                    "supplierCode": "E",
                    "supplierName": "Expedia",
                    "bookingRefNo": "GTDE-1041",
                    "passengerNameRecord": "GTDE-1041",
                    "timeToLive": null,
                    "signature": null,
                    "detail": "Khách sạn Continental Sài Gòn",
                    "originLocationCode": "481659",
                    "destinationLocationCode": "481659",
                    "carrierNo": "EXPEDIA::481659",
                    "checkIn": "2021-07-22T17:00:00Z",
                    "checkOut": "2021-07-23T17:00:00Z",
                    "baseFare": 1043681.0,
                    "equivFare": 0.0,
                    "serviceTax": 161771.0,
                    "totalFare": 1205452.0,
                    "totalTax": 161771.0,
                    "agencyMarkupValue": 0.0,
                    "markupValue": null,
                    "totalSsrValue": 0.0,
                    "markupKey": null,
                    "markupCode": null,
                    "markupFormula": null,
                    "paymentAmount": null,
                    "issuedStatus": "PENDING",
                    "issuedDate": null,
                    "etickets": null,
                    "listETickets": null,
                    "productSeqNumber": "4355",
                    "productClass": null,
                    "bookingDirection": "TRIP",
                    "noAdult": 2,
                    "noChild": 0,
                    "noInfant": 0,
                    "supplierBookingStatus": "BOOKED",
                    "supplierPaymentStatus": null,
                    "allowHold": false,
                    "refundable": true,
                    "onlyPayLater": false
                }
            ],
            "agencyMarkupInfos": [
                {
                    "agencyCode": "A::1",
                    "baseFare": 1043681.0,
                    "equivFare": 0.0,
                    "serviceTax": 161771.0,
                    "totalFare": 1043681.0,
                    "totalTax": 161771.0,
                    "markupValue": 0.0,
                    "agencyMarkupValue": 0.0
                }
            ],
            "contactInfos": [],
            "travelerInfos": [
                {
                    "id": null,
                    "bookingNumber": "HDCO2105109318609",
                    "bookingTransCode": null,
                    "email": null,
                    "gender": null,
                    "firstName": "THE HOAN",
                    "surName": "TRAN",
                    "dob": null,
                    "adultType": null,
                    "country": null,
                    "city": null,
                    "address1": null,
                    "address2": null,
                    "postalCode": null,
                    "phoneNumber1": null,
                    "phoneNumber2": null,
                    "phoneNumber3": null,
                    "phoneNumber4": null,
                    "phoneNumber5": null,
                    "documentType": null,
                    "nationality": null,
                    "documentNumber": null,
                    "documentExpiredDate": null,
                    "documentIssuedDate": null,
                    "documentIssuingCountry": null,
                    "memberCard": null,
                    "memberCardType": null,
                    "memberCardNumber": null,
                    "memberCardExpiredDate": null,
                    "orderIdx": 0,
                    "eticket": null,
                    "bookingId": null,
                    "serviceRequests": null
                }
            ],
            "timeToLive": "2021-05-10T09:43:21Z",
            "supplierBookingStatus": "BOOKED",
            "passengerNameRecords": "GTDE-1041",
            "etickets": "",
            "cancellationFee": 0.0,
            "cancellationNotes": null,
            "cancellationBy": null,
            "cancellationDate": null,
            "discountAmount": 0.0,
            "discountVoucherCode": null,
            "discountVoucherName": null,
            "discountRedeemId": null,
            "discountRedeemCode": null,
            "discountDate": null,
            "additionalFee": null,
            "taxPersonalInfoContact": "{\"name\":\"Tran\",\"fname\":\"The Hoan\",\"phone\":\"0399903620\",\"email1\":\"hoan.tranthe@gmail.com\",\"phoneCode3\":\"84\"}",
            "bookingNote": null,
            "internalBookingNote": null,
            "promotionID": null,
            "reasonCodePaymentFailed": null,
            "bookingFinalStatus": null,
            "bookingIssuedType": "CONFIRM_OFFLINE",
            "ownerBooking": false,
            "allowHold": false,
            "refundable": true,
            "onlyPayLater": false,
            "deleted": null,
            "showPayLaterOption": false,
            "showPayNowOption": true
        },
        "groupPricedItineraries": null,
        "hotelAvailability": {
            "id": null,
            "supplierCode": null,
            "supplierSessionId": null,
            "hotelCode": null,
            "hotelMeta": null,
            "checkIn": null,
            "checkInInstructions": null,
            "specialCheckInInstructions": null,
            "checkOut": null,
            "city": null,
            "country": null,
            "payAtHotel": null,
            "hotelCurrency": null,
            "hotelImages": null,
            "hotelPrice": null,
            "hotelAvailableCode": null,
            "roomRates": null,
            "tripAdvisorRating": null,
            "tripAdvisorReviewCount": null,
            "tripAdvisorRatingUrl": null,
            "products": null
        },
        "hotelProductPayload": {
            "tripId": "lIMfVHkB0y3GNIc_QS_f",
            "roomId": "201866846",
            "ratePlanId": "209445837"
        },
        "hotelProduct": {
            "productId": "4355",
            "searchId": "eyJzZWFyY2hJZCI6IiIsImNoZWNrSW4iOiIyMDIxLTA3LTIzIiwiY2hlY2tPdXQiOiIyMDIxLTA3LTI0IiwicGF4SW5mb3MiOlt7ImFkdWx0UXVhbnRpdHkiOjIsImNoaWxkUXVhbnRpdHkiOjAsImluZmFudFF1YW50aXR5IjowLCJjaGlsZEFnZXMiOltdfV0sImxhbmd1YWdlIjoidmkiLCJjdXJyZW5jeSI6IlZORCIsInN1cHBsaWVyIjoiRVhQRURJQSIsInNlYXJjaENvZGUiOiIxNzgyNjIiLCJzZWFyY2hUeXBlIjoiTVVMVElfQ0lUWV9WSUNJTklUWSJ9",
            "tripId": "lIMfVHkB0y3GNIc_QS_f",
            "propertyId": null,
            "propertyName": "Khách sạn Continental Sài Gòn",
            "supplier": "EXPEDIA",
            "currency": "VND",
            "language": "vi",
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
            "propertyCategory": {
                "id": "",
                "name": ""
            },
            "latitude": 10.776629,
            "longitude": 106.702459,
            "rank": 11042,
            "rating": {
            "ratingProperty": {
                "rating": "4.0",
                "type": "Star"
            },
            "ratingGuest": {
                "count": 995,
                "score": "",
                "recommendationPercent": "80.2",
                "overall": "",
                "cleanliness": "",
                "service": "",
                "comfort": "",
                "condition": "",
                "location": "",
                "neighborhood": "",
                "quality": "",
                "value": "",
                "amenities": ""
            }
            },
            "checkin": {
                "beginTime": "02:00 PM",
                "endTime": "02:00 PM"
            },
            "checkout": {
                "endTime": "12:00"
            },
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
                    "name": "overview",
                    "value": "<p><strong>1 giường cỡ queen hoặc 2 giường đơn</strong></p><p>35 mét vuông</p><br/><p><b>Internet</b> - Wifi miễn phí <br /> <p><b>Giải trí</b> - TV LCD 46 inch với các kênh truyền hình cáp</p><p><b>Ăn uống</b> - Dụng cụ pha cà phê/trà, minibar, dịch vụ phòng 24 giờ và nước đóng chai miễn phí</p> <p><b>Giấc ngủ</b> - Dịch vụ dọn phòng buổi tối</p> <p><b>Phòng tắm</b> - Phòng tắm riêng với vòi sen/bồn tắm kết hợp, áo choàng tắm và dép đi trong nhà</p><p><b>Tiện nghi</b> - Két an toàn, báo miễn phí các ngày trong tuần và bàn</p><p><b>Tiện nghi</b> - Máy điều hòa nhiệt độ và dịch vụ dọn phòng hàng ngày</p><p><b>Thông tin cần biết</b> - Không có bộ trải giường</p> <p>Không hút thuốc</p>"
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
                    "value": ""
                },
                {
                    "id": "2063",
                    "name": "Quầy tiếp tân 24 giờ",
                    "value": ""
                },
                {
                    "id": "2537",
                    "name": "Số lượng nhà hàng:  - 2",
                    "value": ""
                },
                {
                    "id": "3",
                    "name": "Bar/lounge",
                    "value": ""
                },
                {
                    "id": "3637",
                    "name": "Một phòng họp",
                    "value": ""
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
                }
            ],
            "rooms": [
                {
                    "id": "201866846",
                    "name": "Phòng Superior",
                    "descriptions": [],
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
                            "basePrice": 1043681.0,
                            "promo": true,
                            "basePriceBeforePromo": 0.0,
                            "amenities": [
                                {
                                    "id": "2205",
                                    "name": "Bữa sáng buffet",
                                    "value": ""
                                },
                                {
                                    "id": "1073742786",
                                    "name": "Bữa sáng miễn phí",
                                    "value": ""
                                },
                                {
                                    "id": "2109",
                                    "name": "Đậu xe miễn phí",
                                    "value": ""
                                },
                                {
                                    "id": "2192",
                                    "name": "Wifi miễn phí",
                                    "value": ""
                                }
                            ],
                            "bedGroups": [
                                {
                                    "id": "37341",
                                    "description": "2 giường đơn",
                                    "configurations": []
                                },
                                {
                                    "id": "37310",
                                    "description": "1 giường cỡ queen",
                                    "configurations": []
                                }
                            ],
                            "cancelPenalties": [
                                {
                                    "startDate": "09/07/2021 18:00",
                                    "endDate": "23/07/2021 18:00",
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
                                            "name": "tax_and_service_fee",
                                            "value": 161771.0,
                                            "valueByHotelCurrency": "161771.0 VND"
                                        },
                                        {
                                            "name": "base_rate",
                                            "value": 1043681.0,
                                            "valueByHotelCurrency": "1043681.0 VND"
                                        }
                                        ]
                                    }
                                    ]
                                }
                            ],
                            "totalPrice": 1205452.0,
                            "totalPriceByHotelCurrency": 1205452.0,
                            "taxAndFees": 161771.0,
                            "fees": {},
                            "promoDescription": "Tiết kiệm 25%",
                            "cancelFreeBeforeDate": "09/07/2021 00:00"
                        }
                    ]
                }
            ],
            "customerIp": ""
        },
        "offlineBooking": null,
        "travelerInfo": {
            "airTravelers": [
                {
                    "idx": 0,
                    "transCode": null,
                    "productCode": "lIMfVHkB0y3GNIc_QS_f",
                    "passengerId": null,
                    "passengerType": null,
                    "gender": null,
                    "passengerName": {
                    "title": null,
                    "firstName": "THE HOAN",
                    "lastName": "TRAN"
                    },
                    "dateOfBirth": null,
                    "passport": {
                    "passportNumber": null,
                    "passportType": null,
                    "country": null,
                    "expiryDate": null
                    },
                    "frequentFlyerType": null,
                    "frequentFlyerNumber": null,
                    "phone1": null,
                    "phone2": null,
                    "email": null,
                    "specialServiceRequest": null,
                    "extraServicesRequest": null,
                    "eticket": null
                }
            ],
            "contactInfos": [
                {
                    "title": null,
                    "firstName": "THE HOAN",
                    "lastName": "TRAN",
                    "areaCode": "84",
                    "countryCode": null,
                    "city": null,
                    "phoneNumber1": "0399903620",
                    "phoneNumber2": null,
                    "email": "tranthehoanis@gmail.com",
                    "postCode": null
                }
            ]
        },
        "isPerBookingType": false
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

## 4. API Cập nhật thông tin booking và giữ chỗ

!!! info "POST: /api/v3/hotel/add-booking-traveller"
    Cập nhật các thông tin: Hành khách, người liên hệ, thông tin xuất hóa đơn, … và yêu cầu giữ chỗ

### Request Body 

=== "Model"
    ???+ example "Request Body"

        - bookingNumber (string, required),

            !!! quote ""

                Mã tham chiếu đến booking

        - bookingContacts (Array[BookingContactDTO], required),

            !!! quote "" 

                Mảng đối tượng chứ thông tin người liên hệ 

            - bookingNumber (string),

                !!! quote ""

                    Mã tham chiếu đến booking

            - phoneNumber1 (string, optional),

                !!! quote ""

                    Số điện thoại 1

            - email (string, optional),

                !!! quote ""

                    Địa chỉ email người liên hệ 

            - surName (string)

                !!! quote ""

                    Họ người liên hệ 

            - firstName (string),

                !!! quote ""

                    Tên đêm và tên người liên hệ 

            - phoneCode1 (string, optional),

                !!! quote ""

                    Mã quốc gia 

        - bookingTravelerInfos (Array[BookingTravelerInfoDTO], required),

            !!! quote ""

                Mảng đối tượng chứa thông tin người nhận phòng. Người nhận phòng phải là người lớn. Mỗi một phòng tương ứng với 1 phần tử của mảng.

            - traveler (BookingTravelerDTO, optional)

                !!! quote ""

                    Thông tin người nhận phòng 

                - bookingNumber (string),

                    !!! quote ""

                        Mã tham chiếu đến booking 

                - firstName (string),

                    !!! quote ""

                        Tên đêm và tên người nhận phòng 

                - surName (string)

                    !!! quote ""

                        Họ của người nhận phòng 
            
        - taxReceiptRequest (BookingTaxReceiptRequestDTO, optional)

            !!! quote ""

                Yêu cầu xuất hóa đơn. Nếu không yêu cầu xuất hóa đơn thì để trống 

            - bookingNumber (string, optional),

                !!! quote ""

                    Mã tham chiếu đến booking 

            - taxAddress1 (string, optional),

                !!! quote ""

                    Địa chỉ công ty 

            - taxCompanyName (string, optional),

                !!! quote ""

                    Tên công ty 
            - taxNumber (string, optional),

                !!! quote ""

                    Mã số thuế 

            - taxPersonalInfoContact (string, optional),

                !!! quote ""

                    Thông tin liên hệ người yêu cầu xuất hóa đơn 

                    Là chuỗi json của đối tượng: 

                    - name (string, required)

                        !!! quote ""

                            Họ người liên hệ 

                    - fname (string, required)

                        !!! quote ""

                            Tên đệm và tên người liên hệ 

                    - phone (string, required)

                        !!! quote ""

                            Số điện thoại người liên hệ 

                    - email (string, required)

                        !!! quote ""

                            Email người liên hệ 

                    - phonecode3 (string, required)

                        !!! quote ""

                            Mã điện thoại 

            - taxReceiptRequest (boolean, optional)

                !!! quote ""

                    Yêu cầu xuất hóa đơn 

                    - `true`: Yêu cầu xuất hóa đơn  
=== "Example" 
    ```json 
    {
        "bookingContacts": [
            {
                "bookingNumber": "HDCO2105109318609",
                "phoneNumber1": "0XXXXXXXXX",
                "email": "nguyenvana@gotadi.com",
                "firstName": "VAN A",
                "surName": "NGUYEN",
                "phoneCode1": "84"
            }
        ],
        "bookingNumber": "HDCO2105109318609",
        "bookingTravelerInfos": [
            {
                "traveler": {
                    "bookingNumber": "HDCO2105109318609",
                    "firstName": "VAN A",
                    "surName": "NGUYEN"
                }
            }
        ],
        "taxReceiptRequest": {
            "bookingNumber": "HDCO2105109318609",
            "taxAddress1": "194 Nguyễn Thị Minh Khai, Phường Võ Thị Sáu, Quận 3, TP.HCM",
            "taxCompanyName": "CÔNG TY TNHH DỊCH VỤ X",
            "taxNumber": "XXXXXXXXXX",
            "taxReceiptRequest": true,
            "taxPersonalInfoContact": "{\"name\":\"Nguyen\",\"fname\":\"Van A\",\"phone\":\"XXXXXXXXXX\",\"email1\":\"nguyenvana@gotadi.com\",\"phoneCode3\":\"84\"}"
        }
    }
    ```

### Response 
#### Code 200
> OK

=== "Model"
    ???+ example "Model"
        - result (SearchAllRatesResult, optional),

            - bookingCode (BookingCode, optional),
                    
                !!! quote "" 
                        
                    Mã định danh kết quả search-all-rate, mỗi lần gọi search-all-rate sẽ tạo ra tripId mới, nó được sử dụng khi đi thao tác đặt phòng 

                - bookingCode (string, optional)

                    !!! quote "" 

                        Mã dùng mô tả các thông tin cơ bản của booking

                - bookingNumber (string, optional)
                
                    !!! quote "" 

                        Mã dùng tham chiếu đến booking
                    
        - duration (integer, optional),
        - errors (Array[Error], optional),
        - infos (Array[Info], optional),
        - success (boolean, optional),
        - textMessage (string, optional)

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

