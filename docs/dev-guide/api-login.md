# Document API Login

---

## 1. API Đăng nhập

!!! info "POST: /api/partner/login"
    Khởi tạo phiên làm việc mới cho người dùng

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
                <access_code>|<user_id>|<layout>|<product>
                ```    

                *Original data schema:*
                ```
                <access_code>|<user_id>|<layout>|<product>|<signature>
                ```

                - access_code (String, required)

                    !!! quote ""

                        Access code do Gotadi cung cấp cho Đối tác.

                - user_id (String, required)

                    !!! quote ""

                        Mã định danh người dùng trên hệ thống của Đối tác.

                - layout (String, optional)

                    !!! quote ""

                        Có giá trị là `dual` hoặc `single` tương ứng với 2 loại layout Gotadi cung cấp cho đối tác.

                - product (String, required)

                    !!! quote ""

                        Có giá trị là `flight` hoặc `hotel`. Tương ứng với 2 sản phẩm Gotadi cung cấp cho đối tác.
                        
                        Khi layout là `single`: Dùng để chọn dịch vụ hiển thị trên webview.

                        Khi layout là `dual`: Dùng để focus dịch vụ hiển thị trên webview.

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
                <access_code>|<error_code>|<redirect_url>
                ```    

                *Original data schema:*
                ```
                <access_code>|<error_code>|<redirect_url>|<signature>
                ```

                - access_code (String, required)

                    !!! quote ""

                        Access code do Gotadi cung cấp cho Đối tác.

                - error_code (String, required)

                    !!! quote ""

                        [Mã lỗi](/dev-guide/#7-ma-loi)

                - redirect_url (String, optional)

                    !!! quote ""

                        Đường dẫn tới Webview Gotadi có kèm theo jwtToken.
                        ```
                        https://<gotadi_webview_url>?access_token=<jwtToken>
                        ```
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