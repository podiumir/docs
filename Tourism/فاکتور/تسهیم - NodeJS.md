# تسهیم
## افزودن کسب‌وکار واسط
27. addDealer: در صورتی که بخشی از فروش شما به کسب و کار دیگری تعلق دارد و می خواهید فاکتور به نام همان کسب و کار ثبت شود، لازم است آن کسب و کار، به کسب و کار شما اجازه صدور فاکتور به عنوان معامله گر را داده باشد. با در اختیار داشتن شناسه کسب و کار دیگر با استفاده از این تابع می توانید این اجازه را صادر کنید.

```
let addDealerData = {
  // ------ REQUIRED ------
  dealerBizId: 0 // ID

  // ------ OPTIONAL ------
  // allProductAllow: true | false
};
podBillingService.addDealer(addDealerData)
  .then(function (result) {
    console.log('function: addDealer ============>', result, '\n');
  })
  .catch(function (error) {
    console.log('error addDealer ============>', error);
  });
```


نمونه خروجی
<br>

```
   { business:
      { id: 3605,
        name: '&#x641;&#x646;&#x627;&#x67E; &#x62A;&#x633;&#x62A; &#x645;&#x634;&#x647;&#x62F;',
        numOfProducts: 3,
        rate: [Object],
        sheba: '080570100611513898506001' },
     dealer:
      { id: 3612,
        name: '&#x6A9;&#x634;&#x62A; &#x6AF;&#x631;',
        image: 'https://core.pod.land/nzh/image?imageId=69973&hashCode=16a67f0bab0-0.2094907373026107',
        numOfProducts: 0,
        rate: [Object],
        sheba: '980570100680013557234101' },
     enable: true,
     allProductAllow: false } }
```

<div class="box-end">
</div>

## لیست کسب‌وکارهای واسط
28. dealerList: برای دریافت یا جستجوی لیست تمام کسب و کارهایی که به آنها مجوز معامله و صدور فاکتور داده اید  می توانید از این تابع استفاده کنید

```
let dealerListData = {
  // ------ REQUIRED ------

  // ------ OPTIONAL ------
  // dealerBizId: ID
  // enable: true | false
  // offset: OFFSET
  // size: SIZE
};

podBillingService.dealerList(dealerListData)
  .then(function (result) {
    console.log('function: dealerList ============>', JSON.stringify(result, null, 2), '\n');
  })
  .catch(function (error) {
    console.log('error dealerList ============>', error);
  });
```


نمونه خروجی
<br>

```
{
  "hasError": false,
  "messageId": 0,
  "referenceNumber": "235031199",
  "errorCode": 0,
  "count": 1,
  "ott": "403e86f6ae633517",
  "result": [
    {
      "business": {
        "id": 3605,
        "name": "&#x641;&#x646;&#x627;&#x67E; &#x62A;&#x633;&#x62A; &#x645;&#x634;&#x647;&#x62F;",
        "numOfProducts": 3,
        "rate": {
          "rate": 0,
          "rateCount": 0
        },
        "sheba": "080570100611513898506001"
      },
      "dealer": {
        "id": 3612,
        "name": "&#x6A9;&#x634;&#x62A; &#x6AF;&#x631;",
        "image": "https://core.pod.land/nzh/image?imageId=69973&hashCode=16a67f0bab0-0.2094907373026107",
        "numOfProducts": 0,
        "rate": {
          "rate": 0,
          "rateCount": 0
        },
        "sheba": "980570100680013557234101"
      },
      "enable": true,
      "allProductAllow": false
    }
  ]
}
```

<div class="box-end">
</div>

## فعالسازی کارگزار
29. enableDealer: با استفاده از این تابع می توانید کسب کارهای واسط را فعال کنید

```
let enableDealerData = {
  // ------ REQUIRED ------
  dealerBizId: 0 // ID

  // ------ OPTIONAL ------
};
podBillingService.enableDealer(enableDealerData)
  .then(function (result) {
    console.log('function: enableDealer ============>', JSON.stringify(result, null, 2), '\n');
  })
  .catch(function (error) {
    console.log('error enableDealer ============>', error);
  });
```


نمونه خروجی
<br>

```
{
  "hasError": false,
  "messageId": 0,
  "referenceNumber": "235035141",
  "errorCode": 0,
  "count": 0,
  "ott": "753c508ef245852a",
  "result": {
    "business": {
      "id": 3605,
      "name": "&#x641;&#x646;&#x627;&#x67E; &#x62A;&#x633;&#x62A; &#x645;&#x634;&#x647;&#x62F;",
      "numOfProducts": 3,
      "rate": {
        "rate": 0,
        "rateCount": 0
      },
      "sheba": "080570100611513898506001"
    },
    "dealer": {
      "id": 3612,
      "name": "&#x6A9;&#x634;&#x62A; &#x6AF;&#x631;",
      "image": "https://core.pod.land/nzh/image?imageId=69973&hashCode=16a67f0bab0-0.2094907373026107",
      "numOfProducts": 0,
      "rate": {
        "rate": 0,
        "rateCount": 0
      },
      "sheba": "980570100680013557234101"
    },
    "enable": true,
    "allProductAllow": false
  }
}
```

<div class="box-end">
</div>

## غیرفعالسازی کسب‌وکار واسط
30. disableDealer: با استفاده از این تابع می توانید کسب کارهای واسط را غیر فعال کنید

```
let disableDealerData = {
  // ------ REQUIRED ------
  dealerBizId: 0 // ID

  // ------ OPTIONAL ------
};
podBillingService.disableDealer(disableDealerData)
  .then(function (result) {
    console.log('function: disableDealer ============>', JSON.stringify(result, null, 2), '\n');
  })
  .catch(function (error) {
    console.log('error disableDealer ============>', error);
  });
```


نمونه خروجی
<br>

```
{
  "hasError": false,
  "messageId": 0,
  "referenceNumber": "235036062",
  "errorCode": 0,
  "count": 0,
  "ott": "135f86428674bb26",
  "result": {
    "business": {
      "id": 3605,
      "name": "&#x641;&#x646;&#x627;&#x67E; &#x62A;&#x633;&#x62A; &#x645;&#x634;&#x647;&#x62F;",
      "numOfProducts": 3,
      "rate": {
        "rate": 0,
        "rateCount": 0
      },
      "sheba": "080570100611513898506001"
    },
    "dealer": {
      "id": 3612,
      "name": "&#x6A9;&#x634;&#x62A; &#x6AF;&#x631;",
      "image": "https://core.pod.land/nzh/image?imageId=69973&hashCode=16a67f0bab0-0.2094907373026107",
      "numOfProducts": 0,
      "rate": {
        "rate": 0,
        "rateCount": 0
      },
      "sheba": "980570100680013557234101"
    },
    "enable": false,
    "allProductAllow": false
  }
}
```

<div class="box-end">
</div>

## لیست کسب‌وکارهایی که واسط آن‌ها شده‌اید
31. businessDealingList: با فراخوانی سرویس ذیل می توانید لیست کسب و کارهایی که واسط آن ها شده اید را دریافت نمایید.

```
let businessDealingListData = {
  // ------ REQUIRED ------

  // ------ OPTIONAL ------
  // dealingBusinessId: ID
  // enable: true | false
  // offset: OFFSET
  // size: SIZE
};

podBillingService.businessDealingList(businessDealingListData)
  .then(function (result) {
    console.log('function: businessDealingList ============>', JSON.stringify(result, null, 2), '\n');
  })
  .catch(function (error) {
    console.log('error businessDealingList ============>', error);
  });
```


نمونه خروجی
<br>

```
{
  "hasError": false,
  "messageId": 0,
  "referenceNumber": "235040226",
  "errorCode": 0,
  "count": 2,
  "ott": "2617cb9af8c4b908",
  "result": [
    {
      "business": {
        "id": 3612,
        "name": "&#x6A9;&#x634;&#x62A; &#x6AF;&#x631;",
        "image": "https://core.pod.land/nzh/image?imageId=69973&hashCode=16a67f0bab0-0.2094907373026107",
        "numOfProducts": 0,
        "rate": {
          "rate": 0,
          "rateCount": 0
        },
        "sheba": "980570100680013557234101"
      },
      "dealer": {
        "id": 3605,
        "name": "&#x641;&#x646;&#x627;&#x67E; &#x62A;&#x633;&#x62A; &#x645;&#x634;&#x647;&#x62F;",
        "numOfProducts": 3,
        "rate": {
          "rate": 0,
          "rateCount": 0
        },
        "sheba": "080570100611513898506001"
      },
      "enable": false,
      "allProductAllow": false
    },
    {
      "business": {
        "id": 3615,
        "name": "&#x62A;&#x633;&#x62A; &#x627;&#x646;&#x648;&#x631;&#x6CC;",
        "numOfProducts": 0,
        "rate": {
          "rate": 0,
          "rateCount": 0
        },
        "sheba": "290570100680013555510101"
      },
      "dealer": {
        "id": 3605,
        "name": "&#x641;&#x646;&#x627;&#x67E; &#x62A;&#x633;&#x62A; &#x645;&#x634;&#x647;&#x62F;",
        "numOfProducts": 3,
        "rate": {
          "rate": 0,
          "rateCount": 0
        },
        "sheba": "080570100611513898506001"
      },
      "enable": false,
      "allProductAllow": false
    }
  ]
}
```

<div class="box-end">
</div>

## صدور فاکتور تسهیمی
32. issueMultiInvoice: کسب و کار معامله گر می تواند با استفاده از این تابع یک فاکتور تسهیمی ثبت نماید

```
let issueMultiInvoiceData = {
  // ------ REQUIRED ------
  data: {
    // redirectURL: 'REDIRECT URL',
    // userId: 0, // USER ID
    // currencyCode: 'CURRENCY', // OPTIONAL
    // voucherHashs: ARRAY OF STRINGS,
    // preferredTaxRate: 0, // OPTIONAL
    // verificationNeeded: true | false, // OPTIONAL
    // preview: true | false, // OPTIONAL
    mainInvoice: {
      // billNumber: 'BILL NUMBER', // OPTIONAL
      guildCode: 'GUILD CODE',
      // metadata: OBJECT, // OPTIONAL
      // description: 'DESCRIPTION', // OPTIONAL
      invoiceItemVOs: [{
        productId: 0,
        price: 0,
        quantity: 0,
        description: 'DESCRIPTION'
      }]
    },
    subInvoices: [{
      businessId: 0, // ID
      guildCode: 'GUILD CODE',
      // billNumber: 'BILL NUMBER', // OPTIONAL
      // metadata: OBJECT, // OPTIONAL
      // description: 'DESCRIPTION', // OPTIONAL
      invoiceItemVOs: [{
        productId: 0,
        price: 0,
        quantity: 0,
        description: 'DESCRIPTION'
      }]
    }],
    // customerDescription: 'DESCRIPTION', // OPTIONAL
    // customerMetadata: OBJECT, // OPTIONAL
    customerInvoiceItemVOs: [{
      productId: 0,
      price: 0,
      quantity: 0,
      description: 'DESCRIPTION'
    }]
  }

  // ------ OPTIONAL ------
  // delegatorId: ARRAY OF INTEGERS
  // delegationHash: ARRAY OF STRING
  // forceDelegation: 'FORCE DELIGATION'
};

podBillingService.issueMultiInvoice(issueMultiInvoiceData)
  .then(function (result) {
    console.log('function: issueMultiInvoice ============>', JSON.stringify(result, null, 2), '\n');
  })
  .catch(function (error) {
    console.log('error issueMultiInvoice ============>', error);
  });
```


نمونه خروجی
<br>

```
{
  "hasError": false,
  "messageId": 0,
  "referenceNumber": "235044247",
  "errorCode": 0,
  "count": 0,
  "ott": "2889093d560c9894",
  "result": {
    "id": 3526913,
    "totalAmountWithoutDiscount": 0,
    "delegationAmount": 0,
    "totalAmount": 0,
    "payableAmount": 0,
    "vat": 0,
    "issuanceDate": 1563115794187,
    "deliveryDate": 0,
    "paymentBillNumber": "6047257",
    "uniqueNumber": "c176e2f840842d3a",
    "paymentDate": 0,
    "payed": false,
    "serial": 0,
    "canceled": false,
    "cancelDate": 0,
    "business": {
      "id": 3605,
      "name": "&#x641;&#x646;&#x627;&#x67E; &#x62A;&#x633;&#x62A; &#x645;&#x634;&#x647;&#x62F;",
      "numOfProducts": 3,
      "rate": {
        "rate": 0,
        "rateCount": 0
      },
      "sheba": "080570100611513898506001"
    },
    "invoiceItemSrvs": [
      {
        "id": 3564753,
        "amount": 0,
        "description": "ss",
        "quantity": 0,
        "voucherUsageSrvs": []
      }
    ],
    "guildSrv": {
      "id": 47,
      "name": "&#x641;&#x646;&#x627;&#x648;&#x631;&#x6CC; &#x627;&#x637;&#x644;&#x627;&#x639;&#x627;&#x62A;",
      "code": "INFORMATION_TECHNOLOGY_GUILD"
    },
    "closed": false,
    "verificationNeeded": false,
    "customerInvoice": {
      "id": 3526912,
      "totalAmountWithoutDiscount": 1100,
      "delegationAmount": 0,
      "totalAmount": 1100,
      "payableAmount": 1199,
      "vat": 99,
      "issuanceDate": 1563115794186,
      "deliveryDate": 0,
      "paymentBillNumber": "6047257",
      "uniqueNumber": "1963cf87a2de34d3",
      "paymentDate": 0,
      "payed": false,
      "serial": 0,
      "canceled": false,
      "cancelDate": 0,
      "business": {
        "id": 3605,
        "name": "&#x641;&#x646;&#x627;&#x67E; &#x62A;&#x633;&#x62A; &#x645;&#x634;&#x647;&#x62F;",
        "numOfProducts": 3,
        "rate": {
          "rate": 0,
          "rateCount": 0
        },
        "sheba": "080570100611513898506001"
      },
      "invoiceItemSrvs": [
        {
          "id": 3564752,
          "amount": 110,
          "description": "Hello",
          "quantity": 10,
          "voucherUsageSrvs": []
        }
      ],
      "guildSrv": {
        "id": 47,
        "name": "&#x641;&#x646;&#x627;&#x648;&#x631;&#x6CC; &#x627;&#x637;&#x644;&#x627;&#x639;&#x627;&#x62A;",
        "code": "INFORMATION_TECHNOLOGY_GUILD"
      },
      "closed": false,
      "verificationNeeded": false,
      "safe": false,
      "postVoucherEnabled": false,
      "referenceNumber": "235044247",
      "issuerSrv": {
        "id": 1454449,
        "name": "&#x627;&#x62D;&#x633;&#x627;&#x646; &#x634;&#x6A9;&#x627;&#x631;&#x6CC;",
        "ssoId": "6254762",
        "ssoIssuerCode": 1,
        "profileImage": "https://core.pod.land:443/nzh/image/?imageId=69962&width=498&height=498&hashCode=16a679c6ad9-0.3413974672033351"
      },
      "willBeBlocked": false,
      "willBePaid": false,
      "edited": false,
      "waiting": false,
      "subInvoice": false
    },
    "subInvoices": [
      {
        "id": 3526914,
        "totalAmountWithoutDiscount": 1100,
        "delegationAmount": 0,
        "totalAmount": 1100,
        "payableAmount": 1199,
        "vat": 99,
        "issuanceDate": 1563115794188,
        "deliveryDate": 0,
        "paymentBillNumber": "6047257",
        "uniqueNumber": "34a30224cfc63c2d",
        "paymentDate": 0,
        "payed": false,
        "serial": 0,
        "canceled": false,
        "cancelDate": 0,
        "business": {
          "id": 3605,
          "name": "&#x641;&#x646;&#x627;&#x67E; &#x62A;&#x633;&#x62A; &#x645;&#x634;&#x647;&#x62F;",
          "numOfProducts": 3,
          "rate": {
            "rate": 0,
            "rateCount": 0
          },
          "sheba": "080570100611513898506001"
        },
        "invoiceItemSrvs": [
          {
            "id": 3564754,
            "amount": 110,
            "description": "Hello",
            "quantity": 10,
            "voucherUsageSrvs": []
          }
        ],
        "guildSrv": {
          "id": 47,
          "name": "&#x641;&#x646;&#x627;&#x648;&#x631;&#x6CC; &#x627;&#x637;&#x644;&#x627;&#x639;&#x627;&#x62A;",
          "code": "INFORMATION_TECHNOLOGY_GUILD"
        },
        "closed": false,
        "verificationNeeded": false,
        "safe": false,
        "postVoucherEnabled": false,
        "referenceNumber": "235044247",
        "issuerSrv": {
          "id": 1454449,
          "name": "&#x627;&#x62D;&#x633;&#x627;&#x646; &#x634;&#x6A9;&#x627;&#x631;&#x6CC;",
          "ssoId": "6254762",
          "ssoI
```

<div class="box-end">
</div>
