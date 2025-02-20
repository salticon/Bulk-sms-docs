---

## **Bulk SMS API Documentation**

### **Base URL**

https://apisalticon.onekitty.co.ke/kitty/send-sms/

---

### **Overview**

This API allows you to send bulk SMS messages to one or more recipients by making a POST request. You must include an API key for authentication and provide the message details.

---

### **HTTP Method**

`POST`

---

### **Request Headers**

| Header | Description |
| ----- | ----- |
| `Content-Type` | Specifies the media type of the request body. Set this to `application/json`. |

---

### **Request Body**

The request body should be in JSON format and include the following fields:

| Field | Type | Required | Description |
| ----- | ----- | ----- | ----- |
| `api_key` | `string` | Yes | The API key provided to authenticate your request. |
| `message` | `string` | Yes | The content of the SMS message to send. |
| `recipient` | `array` | Yes | An array of recipient phone numbers in international format (e.g., `254712345678`, `254701345678`). |

#### **Sample Request**

curl \-X POST https://apisalticon.onekitty.co.ke/kitty/send-sms/ \\  
     \-H "Content-Type: application/json" \\  
     \-d '{  
          "api\_key": "be3286365acabe67cad456d5f5c2ea3f61d526144348a1976d67cc9313r1271a",  
          "message": "Hello\! This is a test SMS.",  
          "recipient": \["`254712345678`", "`254712345678`"\]  
         }'

{  
  "api\_key": "be3286365acab\*\*\*\*\*\*\*\*\*\*\*271a",  
  "message": "Hello\! This is a test SMS sent using the Bulk SMS API.",  
  "recipient": \[  
	"254733550051",  
	"254733550051"  
  \]  
}

---

### **Response**

The API will return a JSON response with the details of the SMS sent and the status of the request.

| Field | Type | Description |
| ----- | ----- | ----- |
| `status` | `string` | Indicates the success or failure of the request (e.g., `success`, `error`). |
| `message` | `string` | A human-readable description of the status (e.g., `SMS sent successfully`, `Invalid API key`). |
| `data` | `object` | Contains additional details about the request, such as delivery reports for each recipient. |

#### **Sample Success Response**

{  
  "status": "success",  
  "message": "SMS sent successfully",  
  "data": {  
    "recipients": \[  
      {  
        "number": "`254712345678`",  
        "status": "delivered"  
      },  
      {  
        "number": "`254712345678`",  
        "status": "queued"  
      }  
    \]  
  }  
}

#### **Sample Error Response**

{  
  "status": "error",  
  "message": "Invalid API key",  
  "data": null  
}

---

### **Error Codes**

| Code | Message | Description |
| ----- | ----- | ----- |
| 401 | Invalid API key | The provided API key is incorrect or unauthorized. |
| 400 | Bad Request | The request payload is malformed or missing required fields. |
| 500 | Internal Server Error | An unexpected error occurred on the server. |

---

### **Notes**

* Ensure all phone numbers are in international format (e.g., starting with the country code `254` for Kenya).  
* The maximum length of the `message` is 160 characters for a single SMS. If exceeded, the message will be split and sent as multiple SMS.  
* API rate limits may apply; check with the provider for usage thresholds.

---

### **Best Practices**

1. **Secure API Key**: Never expose your API key publicly or hard-code it in client-side applications. Use environment variables for secure storage.  
2. **Validate Input**: Ensure recipient phone numbers are valid before sending the request to avoid unnecessary errors.  
3. **Handle Errors Gracefully**: Implement logic in your application to retry or handle errors such as queued or failed delivery statuses.

---

