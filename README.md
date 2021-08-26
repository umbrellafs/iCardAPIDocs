# iCard API Documentation
iCard is an online store for giftcards and vouchers of local brands in Libya as well as international brands and services.
The main and only payment method on the iCard store is by using an iCash wallet.

In addition to the website, Android and iOS apps; the iCard store is also acessable via an API (Application Progeramming Interface).

## Base URL
There are two base URLs for the iCard store.

This base URL is for testing and all purchase requests will return cards with dummy secret numbers.

    https://icardtestapp.azurewebsites.net

The other base URL is for production and should replace the previous URL once integrartion testing has been completed.
    
    http://icardsysp1.azurewebsites.net

Below is a list of all the functions/endpoints paths and the required headers, parameters and body for each function:
 
 - [Retrieve Cards](#retrieve-cards-get)
 - [Purchase](#purchase-post)     
 - [Get Cards List ](#get-cards-list-get)  
 - [Get Brand Logo ](#get-brand-logo-get)  
 
## Get Cards List (GET)

### Path

    {base URL}/Fulllist

### Headers
This function requires no headers

### Parameters
This function requires the followung URL parameters:

    {
    "all" = true
    "pack" = 712
    }

### Body
This function requires no body parameters

### Response

    [
        {
            "id": 1,
            "name": "ليبيانا للهاتف المحمول",
            "nameEn": "Libyana",
            "recharegeFormat": "*120*{0}#",
            "viewOnFastBuy": true,
            "image": "1.png",
            "rank": 0,
            "qrFormat": "{0}",
            "cats": [
                {
                    "id": 12,
                    "card_name": "ليبيانا 3",
                    "cardNameEn": "3 LIBYANA",
                    "card_price": 2.94,
                    "quentity": 10,
                    "shortName": "ليبيانا 3",
                    "shortNameEn": "Libyana 3",
                    "currency": 0
                },
                {
                    "id": 13,
                    "card_name": "ليبيانا 5",
                    "cardNameEn": "5 LIBYANA",
                    "card_price": 4.9,
                    "quentity": 10,
                    "shortName": "ليبيانا 5",
                    "shortNameEn": "Libyana 5",
                    "currency": 0
                },
                {
                    "id": 1,
                    "card_name": "ليبيانا 10",
                    "cardNameEn": "10 LIBYANA",
                    "card_price": 9.8,
                    "quentity": 10,
                    "shortName": "ليبيانا 10",
                    "shortNameEn": "Libyana 10",
                    "currency": 0
                },
                {
                    "id": 2,
                    "card_name": "ليبيانا 30",
                    "cardNameEn": "30 LIBYANA",
                    "card_price": 29.4,
                    "quentity": 10,
                    "shortName": "ليبيانا 30",
                    "shortNameEn": "Libyana 30",
                    "currency": 0
                },
                {
                    "id": 355,
                    "card_name": "ليبيانا 40",
                    "cardNameEn": "40 LIBYANA",
                    "card_price": 39.2,
                    "quentity": 10,
                    "shortName": "ليبيانا 40",
                    "shortNameEn": "Libyana 40",
                    "currency": 0
                },
                {
                    "id": 14,
                    "card_name": "ليبيانا 100",
                    "cardNameEn": "100 LIBYANA",
                    "card_price": 98,
                    "quentity": 10,
                    "shortName": "ليبيانا 100",
                    "shortNameEn": "Libyana 100",
                    "currency": 0
                }
            ]
        }
    ]

## Get Brand Logo (GET)

### Path

    {base URL}/img/brands/100x100/{brandID}.png
    
### Headers
This function requires no headers.

### Parameters
This function requires no URL parameters.

### Body
This function requires no body parameters.

### Response

![iCash Logo](brand_logo.png)

## Purchase (POST)

### Path

    {base URL}/APIPay

### Headers

    {
    "apitoken" : c7fghj3#kleu2i$^oeddk3w4dow253kdlk+%#%DE$G^HDS874Dhhr%^H+55Ssrf#9g
    }

The API token above is just an example.
The real token will be provided with the credentials.

### Parameters
This function requires the following url parameters:

    {
    "confirmcode" : 543210,
    "items" : [{"id":12,"quantity":1}],
    "cardno" : 7121234567,
    "captchaCode" : 363843
    }

where:
 - `confirmcode` is the payment code obtained using the `Generate Payment Code` endpoint in the iCash API.
 - `item` is a simple JSON array where each JSON object containing:
   - `id` is the card category ID (not to be confused with brand ID).
   - `quantity` is the count of cards to be purchased from that particular category.
### Body
This function requires no body parameters

### Response

    {
        "invoice_id": 1230010,
        "public_id": "BJF+2bkVfTgS/MYrQ908l2Fsqpc4dXCgLb+Y+rQvjhPwwKCA9/Zm8nXYZH1vtsCOsOYH+BDW0su+hpHbrxZ2Fw==",
        "cards": [
            {
                "brandId": 1,
                "catId": 13,
                "cid": 1296424,
                "card_brand": "ليبيانا للهاتف المحمول",
                "card_name": "ليبيانا 5",
                "card_price": 5,
                "sn": "992432224359111",
                "secret_num": "HYUN123IY678MD23",
                "expiry_date": "5/9/2022 12:00:00 AM",
                "tafaniId": null,
                "rechargeFormat": "*120*HYUN123IY678MD23#",
                "extra": null,
                "PrintingCount": 0,
                "currency": 0,
                "invoice": null
            }
        ],
        "date": "5/25/2021 11:20:46 AM"
    }

## Retrieve Cards (GET)

### Path

    {base URL}/Retrieve

### Headers
This function requires no headers

### Parameters
This function requires the following url parameters:

    {
    "cc" : 123456,
    "icashno" : 7121234567,
    "captchaCode" : 363843
    }

where:
 - `cc` is the payment code for shop #10 and amount 0 LYD.
### Body
This function requires no body parameters.

### Response

    [
        {
            "id": 1219733,
            "created_date": "13:55:30 2021/05/20",
            "public_id": "g8yce5TncBJcuuMQjyGjDMmC0Tixp966DJMf5StuLFscMPl9UGDZz4iM6yrbyduewjUa3F1jzafxAzw0rI6S7Q=="
        },
        {
            "id": 1189187,
            "created_date": "20:24:04 2021/05/08",
            "public_id": "YVCsjPtJVnSPIf38cgpUQtBKZgjM/FSA95dFXPVz1RA+4s9wLqJhWp+MTp08rvnliWNbETbHCSU7XG4SWNfnUQ=="
        },
        {
            "id": 1151485,
            "created_date": "17:21:24 2021/04/21",
            "public_id": "K9oLyv80G+zvKs8YLAVZ48svoyLVojn/ikMTwASVFmIiSAXK5mJM901jb8sjxIzlwKaAw/WUmMot0xLm5Xgoyw=="
        }
    ]

