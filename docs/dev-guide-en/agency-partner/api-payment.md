# APIs for Payment 

---

## Voucher validation API

!!! info "GET: /api/payments/voucher/validate"

    Validate voucher for specific booking

### Request Body
| Parameter | Description |
| --- | --- |
| bookingNumber (String, Required) | Booking Identifier |
| voucherCode (String, Required) | Voucher code  |

=== "Example"
    ```json
    
    {
        "bookingNumber": "ADCO2203011523483",
        "voucherCode": "AXOLXHLp"
    }

    ``` 

### Response
| Parameter                         | Description |
|-----------------------------------| --- |
| bookingNumber (String)            | Booking identifier |
| discountAmount (Double)           | Discount money amount  |
| trackingCode (String)             | Identifier for booking with voucher |
| voucherCode (String)              | Voucher code  |
| voucherValid (Boolean)            | Is valid voucher code? |
| duration (Integer, Optional)      |  |
| errors (Array\[Error\], Optional) |  |
| infos (Array\[Info\], Optional)   |  |
| success (Boolean, Optional)       |  |
| textMessage (String, Optional)    |  |

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
---

## Voucher usage confirmation API

!!! info "GET: /api/payments/voucher/redeem"

    Redeem voucher for specific booking

### Request Body

| Parameter | Description |
| --- | --- |
| bookingNumber (String, Required) | Booking identifier |
| voucherCode (String, Required) | Voucher code |
| trackingCode (String, Required) | Tracking code used in api validate |

=== "Example"
    ```json
    
    {
        "bookingNumber": "ADCO2203011523483",
        "trackingCode": "track_xbhwiFai1HNQNCQLe2PmvdxJu/rd5zEG7NGuvjHI5CY="
        "voucherCode": "AXOLXHLp"
    }

    ``` 

### Response
| Parameter | Description |
| --- | --- |
| bookingNumber (String) | Booking identifier |
| redeemValid (Boolean) | Confirmation of success using Voucher |
| voucherCode (String) | Voucher code  |
| duration (Integer, Optional) |  |
| errors (Array[Error], Optional) |  |
| infos (Array[Info], Optional) |  |
| success (Boolean, Optional) |  |
| textMessage (String, Optional) |  |

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
---

## Booking Payment Request API

!!! info "GET: /api/partner/place-order"
    Request payment booking - initiate payment order

    !!! note "Note"
        - Security requirements: Encrypt data and include a digital signature
        - Request: Does not require encryption and includes a digital signature
        - Response: Part of the response data is required to be encrypted and accompanied by a digital signature


### Request 

| Parameter | Description |
| --- | --- |
| bookingNumber query (string, required), | Reference code to booking |

    - bookingNumber `query` (string, required),

        !!! quote ""

            Reference code to booking


### Response 

=== "Model"
    ???+ example "Model"
        - result (String, optional),

            !!! quote ""

               Information returned in the format:

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

                        Access code provided by Gotadi to Partners.

                - bookingNumber (String, optional)

                    !!! quote ""

                        Code used to refer to booking

                - product_type (String, optional)

                    !!! quote ""

                        Type of product, whose value is AIR or HOTEL corresponding to the type of product purchased

                - total_amount (String, optional)

                    !!! quote ""

                        Total payment amount

                - payment_url (String, required)

                    !!! quote ""

                        URL navigate to payment page 

                - encrypted_key (String, required)

                    !!! quote ""

                        Key decrypts (encrypted) data. How to decrypt refer to the section: Encryption of transmission data and digital signature authentication

                - encrypted_data (String, required) 

                    !!! quote "" 

                        Data with digital signature (encrypted). How to decrypt refer to the section: Encryption of transmission data and digital signature authentication
                    
        - duration (integer, optional),
        - errors (Array[Error], optional),
        - infos (Array[Info], optional),
        - success (boolean, optional),
        - textMessage (string, optional)

---

## Payment Recording and Booking Commit API

!!! info "POST: /api/partner/commit"
    Yêu cầu commit booking được cập nhật đầy đủ thông tin và hoàn tất thanh toán

    !!! note "Chú ý"
        - Security requirements: Encrypt data and include a digital signature
        - Request: Does not require encryption and includes a digital signature
        - Response: Part of the response data is required to be encrypted and accompanied by a digital signature


### Request Body 

=== "Model"
    ???+ example "Model"                 

        - key (string, required),

            !!! quote ""

                Data decrypted key. How to decrypt refer to the section: Encryption of transmission data and digital signature authentication

        - data (string, required),

            !!! quote ""

                Data with digital signature (encrypted). How to decrypt refer to the section: Encryption of transmission data and digital signature authentication

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

                         Access code provided by Gotadi to Partners.

                - bookingNumber (String, required)

                    !!! quote ""

                        Code used to refer to booking

                - partner_trans_id (String, optional)

                    !!! quote ""

                        Partner transaction identifier. If the partner does not pass a value to this field, the default value will be assigned using booking_number

                - product_type (String, required)

                    !!! quote ""

                        Type of product, whose value is AIR or HOTEL corresponding to the type of product purchased

=== "Example"
    ```json
    {
        "data": "string",
        "key": "string"
    }
    ```

### Response 

=== "Model"
    ???+ example "Model"
        - key (String, required)

            !!! quote ""

                 Data decrypted key. How to decrypt refer to the section: Encryption of transmission data and digital signature authentication

        - data (String, required)

            !!! quote ""

                Data with digital signature (encrypted). How to decrypt refer to the section: Encryption of transmission data and digital signature authentication

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

                        Access code provided by Gotadi to Partners.

                - booking_number (String, required)

                    !!! quote ""

                        Code used to refer to booking

                - error_code (String, required)

                    !!! quote ""

                        Error code 

                - product_type (String, optional)

                    !!! quote ""

                        Type of product, whose value is AIR or HOTEL corresponding to the type of product purchased

                - properties (String, optional)

                    !!! quote ""

                        ...

                - return_url (String, optional)

                    !!! quote ""

                        ...

                - total_amount (Double, required)

                    !!! quote ""

                        ...