# APIs for Login

---

## API Login

!!! info "POST: /api/partner/login"
    Create a new session for the user

    !!! note "Note"
        Security requirements: Encrypt data and include a digital signature

### Request Body 

=== "Model"
    ???+ example "Model"

        - key (string, required),

            !!! quote ""

                Key decrypts (encrypted) data. How to establish refer to the section: Encryption of transmitted data and authentication of digital signature

        - data (string, required),

            !!! quote ""

                Data with electronic signature (encrypted). How to decrypt refer to the section: Encryption of transmitted data and authentication of digital signature

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

                        Access code provided by Gotadi to Partners.

                - user_id (String, required)

                    !!! quote ""

                        User identifier on the Partner's system.

                - layout (String, optional)

                    !!! quote ""

                        The value is dual or single corresponding to 2 types of layout Gotadi provides to partners.

                - product (String, required)

                    !!! quote ""

                        - The value is flight or hotel. Corresponding to 2 products Gotadi provided to partners.
                        - When the layout is single: Used to select the display service on the webview.
                        - When the layout is dual: Used to focus the service displayed on the webview.

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

                Key decrypts (encrypted) data. How to establish refer to the section: Encryption of transmitted data and authentication of digital signature

        - data (String, required)

            !!! quote ""

                Data with electronic signature (encrypted). How to decrypt refer to the section: Encryption of transmitted data and authentication of digital signature

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

                        Access code provided by Gotadi to Partners.

                - error_code (String, required)

                    !!! quote ""

                        [Error code ](/dev-guide-en/agency-partner/integration-documentation/#error-code)

                - redirect_url (String, optional)

                    !!! quote ""

                        Link to Gotadi Webview with jwtToken included.
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