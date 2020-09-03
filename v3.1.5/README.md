## **Payment Initiation v3.1.5 Sandbox API** 
****
### **Introduction to the API**
This API helps you perform a Domestic or International Payment. You may perform an immediate payment, schedule a future payment or even schedule a Standing Order.
The api conforms to the UK Open Banking PSD2 specification.

### **Real Life Use Case Scenario**
Imagine you want to perform a Payment using your own application. What can you do about it? Just use this api to make a payment, in any platform you prefer.

### **Create Sandbox**
Your first job is to create a sandbox and save your **sandbox-id** in order to be able to **"play"** with the api.

We will create our sandbox by making an **HTTP POST** request to the following URL:
> https://apis.nbg.gr/sandbox/uk.openbanking.paymentinitiation/oauth2/v3.1.5/sandbox

Request Body:
```json
 {
   "sandbox-id": "my-payments-sandbox"
 }
``` 

**Note: Remember to store *sandbox-id* somewhere in your application, because you will need to provide it as a header
in each api call. Also remember to use the *Client-Id* provided when you create your application in the portal.**

When you create the sandbox application it has some default data.
## **Request Headers**
The following headers are required for every call. In postman they are in the appropriate environment variables.

**Request Headers**:
```
   'accept: application/json'
   'Client-Id: {{clientId}}'
   'sandbox-id: {{sandboxId}}'
   'x-fapi-interaction-id: {{$guid}}'
``` 
## **Scenario Request**
You send **POST /domestic-payments** request to make an immediate domestic payment.
> https://apis.nbg.gr/sandbox/uk.openbanking.paymentinitiation/oauth2/v3.1.5/domestic-payment-consents

**Request**
```json
{
	"Data": {
		"Initiation": {
			"InstructionIdentification":"INSTRUCTION-ID",
			"EndToEndIdentification": "END-TO-END-ID",
			"InstructedAmount": {
				"Amount": "2.5",
				"Currency": "EUR"
			},
			"DebtorAccount": {
				"Name": "DEBTOR NAME",
				"SchemeName":"UK.OBIE.IBAN",
				"Identification":"GR3201106970000069774934603"
			},
			"CreditorAccount": {
				"Name": "CREDITOR NAME",
				"SchemeName":"UK.OBIE.IBAN",
				"Identification":"GR2102600060000440200471249"
			},
			"RemittanceInformation": {
				"Unstructured": "TEST REMITTANCE INFO",
				"Reference": "TEST REFERENCE"
			}
		}
	},
	"Risk":{}
}
``` 

**Response**
```json
{
    "Data": {
        "ConsentId": "8c5fd993-b54f-4c06-b698-3220a4bd76c8",
        "CreationDateTime": "2020-09-03T13:24:57.906Z",
        "Status": "AwaitingAuthorisation",
        "StatusUpdateDateTime": "2020-09-03T13:24:57.97Z",
        "Initiation": {
            "InstructionIdentification": "INSTRUCTION-ID",
            "EndToEndIdentification": "END-TO-END-ID",
            "InstructedAmount": {
                "Amount": "2.5",
                "Currency": "EUR"
            },
            "DebtorAccount": {
                "SchemeName": "UK.OBIE.IBAN",
                "Identification": "GR3201106970000069774934603",
                "Name": "DEBTOR NAME"
            },
            "CreditorAccount": {
                "SchemeName": "UK.OBIE.IBAN",
                "Identification": "GR2102600060000440200471249",
                "Name": "CREDITOR NAME"
            },
            "RemittanceInformation": {
                "Unstructured": "TEST REMITTANCE INFO",
                "Reference": "TEST REFERENCE"
            }
        },
        "Debtor": {
            "Name": "DEBTOR NAME"
        }
    },
    "Risk": {},
    "Links": {
        "Self": "https://apis.nbg.gr/sandbox/uk.openbanking.paymentinitiation/oauth2/v3.1.5/domestic-payment-consents/8c5fd993-b54f-4c06-b698-3220a4bd76c8"
    },
    "Meta": {
        "TotalPages": 1
    }
}

``` 


Created by **NBG**.\
See more at https://developer.nbg.gr/