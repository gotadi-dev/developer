# API Chứng thực

---
???+ info "Đặc tả API"
    - Method: POST
    - URL: <API_GATEWAY\>/partnership/v1/login
    - Mô tả: API Chứng thực cho Booker và PreBooker
???+ info "Example Request"
    ```json
    
    {
        "agencyInfo": {
            "partnerRefCode": "CHI_NHANH_123",
            "fullName": "Chi nhanh Sai Gon",
            "shortName": "Cty X, Chi nhanh Sai Gon",
            "taxCode": "123456",
            "faxNumber": "123456",
            "phoneNumber": "0123456789",
            "address": "194 Nguyen Thi Minh Khai, Phuong 17, Quan Phu Nhuan",
            "email": "user_y@partner_x.com",
            "representativeName": "Nguyen Van A",
            "representativePhone": "0123456789",
            "representativeEmail": "user_y@partner_x.com",
            "extends": {
                "key": "value",
                "key1": "value1"
            }
        },
        "userInfo": {
            "partnerRefCode": "USER_123",
            "firstName": "Nguyen",
            "lastName": "Van A",
            "address": "194 Nguyen Thi Minh Khai, Phuong 17, Quan Phu Nhuan",
            "email": "user_y@partner_x.com",
            "phoneNumber": "0932909474",
            "roles": [
                "BOOKER", "PRE_BOOKER"
            ],
            "extends": {
                "key": "value",
                "key1": "value1"
            }
        },
        "signature": "..."
    }
    ``` 
Signature data schema: "ACCESSCODE|agencyInfo.partnerRefCode|userInfo.partnerRefCode|userInfo.email|userInfo.phoneNumber"



???+ info "Example Response"
    ```json
    {
        "url": "https://uat-v2-vendor.gotadi.com/?merchant_code=A::1_29001&access_token=...",
        "signature": "X6qzaHFxx4FBOhLTg74zifAXXP0lxumkv55se9ejAAMJLzxrAgwL/2QdoVQKGF4zQ0y8DSvNvPhSXTBiHYTS8b+On9IHt5RwWM5pLUoMLmQzB4KXnDgcC0fdDItTYnxNV2CpsEac0hQl/p6FN87QqedAgDKILVneIJ3GRggk2Q8=",
        "errorCode": "00"
    }
    ```

???+ example "HTTP Code"
    - 400: Bad Request
    - 401: Unauthorized
    - 403: Forbidden
    - 404: Not Found
    - 500: Unknown Internal Error
    - 503: Service Unavailable