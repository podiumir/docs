- [مقدمه](#menu)
- [پیش از شروع](#menu)
- [استعلام قبض](#menu)

## مقدمه


## پیش از شروع



## استعلام قبض


- شناسه سرویس : 49956
- پارامترهای ورودی : 

|توضیحات|پارامتر| 
|-------|-----------|
| شماره موبایل |mobileNumber |

- پاسخ‌های برگشتی


#### فراخوانی موفق

```javascript 

{

  "IsSuccess": "true",

  "ResultData": {

    "BillAmount":"میزان بدهی",

    "BillId": "شناسه قبض",

    "PaymentId": "شناسه پرداخت"

  },

  "Message": null,

  "SeqNumber": "0",

  "RefrenceNumber": "0",

  "Result": "Unknown"

}
```

#### شماره موبایل نامعتبر

```javascript 

{
  "IsSuccess": "false",

  "ResultData": "10",

  "Message": "شماره موبایل یافت نشد",

  "SeqNumber": "0",

  "RefrenceNumber": "0",

  "Result": "Unknown"

}
```

#### قبض پرداخت شده است:


```javascript 

{

  "IsSuccess": "false",

  "ResultData": "30",

  "Message": "تسویه شده است",

  "SeqNumber": "0",

  "RefrenceNumber": "0",

  "Result": "Unknown"

}

```
