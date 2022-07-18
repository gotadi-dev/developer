# Document API Payment 

---

## 1.API xác nhận voucher

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

## 2.API xác nhận sử dụng voucher

!!! info "GET: /api/payments/voucher/redeem"

    Redeem voucher cho booking cụ thể

### Request Body

=== "Model"
    ???+ example "Request Body"

        - bookingNumber (String, Required)

            !!! quote ""

                Mã định danh booking
        
        - voucherCode (String, Required)

            !!! quote ""

                Mã giảm giá
        
        - trackingCode (String, Required)

            !!! quote ""

                Mã tracking sử dụng ở api validate

=== "Example"
    ```json
    
    {
        "bookingNumber": "ADCO2203011523483",
        "trackingCode": "track_xbhwiFai1HNQNCQLe2PmvdxJu/rd5zEG7NGuvjHI5CY="
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

        - redeemValid (Boolean)

            !!! quote ""

                Xác nhận sử dụng voucher thành công

        - voucherCode (String)

            !!! quote ""

                Mã giảm giá 

        - duration (Integer, Optional),
        - errors (Array[Error], Optional),
        - infos (Array[Info], Optional),
        - success (Boolean, Optional),
        - textMessage (String, Optional)

=== "Example"
    ```json

        {
            "isSuccess": true,
            "duration": 6508,
            "textMessage": null,
            "errors": null,
            "infos": null,
            "voucherCode": "gtd_fpt_test",
            "bookingNumber": "ADCO2203101541927",
            "redeemValid": true,
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

## 3. API Yêu cầu thanh toán booking

!!! info "GET: /api/partner/place-order"
    Yêu cầu thanh toán booking - khởi tạo payment order

    !!! note "Chú ý"
        Yêu cầu bảo mật: Mã hóa dữ liệu và kèm theo chữ ký điện tử

        - Request: Không yêu cầu phải được mã hóa và kèm theo chữ ký điện tử

        - Response: Một phần dữ liệu của respond được yêu cầu phải mã hóa và kèm theo chữ ký điện tử


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
        - result (String, optional),

            !!! quote ""

                Thông tin trả về dưới định dạng:

                ```
                <payment_url>?key=<encrypted_key>?data=<encrypted_data>
                ```

                *Signature data schema:*

                ``` 
                <access_code>|<booking_number>|<product_type>|<total_amount>
                ```    

                *Original data schema:*
                ```
                <access_code>|<booking_number>|<product_type>|<signature>|<total_amount>
                ```

                - access_code (String, required)

                    !!! quote ""

                        Access code do Gotadi cung cấp cho Đối tác.

                - bookingNumber (String, optional)

                    !!! quote ""

                        Mã dùng tham chiếu đến booking

                - product_type (String, optional)

                    !!! quote ""

                        Loại sản phẩm, có giá trị là `AIR` hoặc `HOTEL` tương ứng với loại sản phẩm được mua

                - total_amount (String, optional)

                    !!! quote ""

                        Tổng số tiền phải thanh toán

                - payment_url (String, required)

                    !!! quote ""

                        Đường dẫn đến trang thanh toán

                - encrypted_key (String, required)

                    !!! quote ""

                        Key giải mã dữ liệu (đã được mã hóa). Cách giải mã tham khảo mục: [Mã hóa dữ liệu truyền và xác thực chữ ký điện tử](/dev-guide/#3-ma-hoa-du-lieu-truyen-va-xac-thuc-chu-ky-ien-tu)

                - encrypted_data (String, required) 

                    !!! quote "" 

                        Dữ liệu kèm theo chữ ký điện tử (đã được mã hóa). Cách giải mã tham khảo mục: [Mã hóa dữ liệu truyền và xác thực chữ ký điện tử](/dev-guide/#3-ma-hoa-du-lieu-truyen-va-xac-thuc-chu-ky-ien-tu)
                    
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

---

## 4. API Ghi nhận thanh toán và commit booking 

!!! info "POST: /api/partner/commit"
    Yêu cầu commit booking được cập nhật đầy đủ thông tin và hoàn tất thanh toán

    !!! note "Chú ý"
        Yêu cầu bảo mật: Mã hóa dữ liệu và kèm theo chữ ký điện tử

        - Request: Không yêu cầu phải được mã hóa và kèm theo chữ ký điện tử

        - Response: Một phần dữ liệu của response được yêu cầu phải mã hóa và kèm theo chữ ký điện tử


### Request Body 

=== "Model"
    ???+ example "Model"                 

        - key (string, required),

            !!! quote ""

                Key giải mã dữ liệu (đã được mã hóa). **Cách giải mã tham khảo mục: Mã hóa dữ liệu truyền và xác thực chữ ký điện tử**

        - data (string, required),

            !!! quote ""

                Dữ liệu kèm theo chữ ký điện tử (đã được mã hóa). **Cách giải mã tham khảo mục: Mã hóa dữ liệu truyền và xác thực chữ ký điện tử**

                *Signature data schema:*

                ``` 
                <access_code>|<booking_number>|<partner_trans_id>|<product_type>
                ```    

                *Original data schema:*
                ```
                <access_code>|<booking_number>|<partner_trans_id>|<product_type>|<signature>
                ```

                - access_code (String, required)

                    !!! quote ""

                        Access code do Gotadi cung cấp cho Đối tác.

                - bookingNumber (String, required)

                    !!! quote ""

                        Mã dùng tham chiếu đến booking

                - partner_trans_id (String, optional)

                    !!! quote ""

                        Mã định danh giao dịch của đối tác. Nếu đối tác không truyền giá trị cho trường này, giá trị mặc định sẽ được gán bằng booking_number

                - product_type (String, required)

                    !!! quote ""

                        Loại sản phẩm, có giá trị là `AIR` hoặc `HOTEL` tương ứng với loại sản phẩm được mua

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
                <access_code>|<booking_number>|<error_code>|<product_type>|<properties>|<return_url>|<total_amount>
                ```    

                *Original data schema:*
                ```
                <access_code>|<booking_number>|<error_code>|<product_type>|<properties>|<return_url>|<signature>|<total_amount>
                ```

                - access_code (String, required)

                    !!! quote ""

                        Access code do Gotadi cung cấp cho Đối tác.

                - booking_number (String, required)

                    !!! quote ""

                        Mã dùng tham chiếu đến booking

                - error_code (String, required)

                    !!! quote ""

                        [Mã lỗi](/dev-guide/#7-ma-loi) 

                - product_type (String, optional)

                    !!! quote ""

                        Loại sản phẩm, có giá trị là `AIR` hoặc `HOTEL` tương ứng với loại sản phẩm được mua

                - properties (String, optional)

                    !!! quote ""

                        Các thông tin mở rộng trả về cho đối tác. `Json string`

                - return_url (String, optional)

                    !!! quote ""

                        Trang hiển thị kết quả giao dịch của Gotadi. Sử dụng trong trường hợp đối tác không tự xây dựng trang hiển thị kết quả cuối cùng.

                - total_amount (Double, required)

                    !!! quote ""

                        Tổng số tiền phải thanh toán.

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