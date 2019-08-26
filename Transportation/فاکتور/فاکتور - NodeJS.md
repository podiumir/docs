
# فاکتور - NodeJS

**ماژول** **pod-billing-service**

توابع این ماژول قابلیت های زیر را در اختیار شما قرار می دهد:

* 	تمامی چرخه مربوط به فاکتور از ایجاد، پرداخت، تایید تا ابطال آن
* 	روش های پرداخت (لینک های پرداخت کیف پول و درگاه، پرداخت نامتعارف)
* 	ایجاد و مدیریت فاکتورهای تسهیمی
* 	تسویه حساب کسب و کار

با توجه به نیاز خود می توانید از هر کدام از قابلیت های ذکر شده استفاده کنید.

**دریافت ماژول **

```
npm install pod-billing-service
```


**ایجاد یک نمونه از ماژول:**

در هنگام ایجاد شی از این سرویس حتما باید توکن دسترسی کسب و کار خود (API TOKEN) را به سازنده ماژول ارسال کنید. همچنین اگر بخواهید به سرور تست (sandbox) وصل شوید باید از حالت دوم ایجاد سرویس استفاده کنید و مقدار پارامتر serverType را برابر با sandbox قرار دهید.
<br>

```
const PodBillingService = require('pod-billing-service');
let podBillingService = new PodBillingService({
  apiToken: 'API TOKEN'
});
/* let podBillingService = new PodBillingService({
  apiToken: 'API TOKEN',
  serverType: 'sandboxs'
}); */
```


**توابع:**

1. getOtt
2. issueInvoice
3. createPreInvoice
4. getInvoiceList
5. payInvoice
6. sendInvoicePaymentSMS
7. getInvoiceListByMetadata
8. getInvoiceListAsFile
9. verifyInvoice
10. cancelInvoice
11. reduceInvoice
12. verifyAndCloseInvoice
13. closeInvoice
14. getInvoicePaymentLink
15. payInvoiceByInvoice
16. payInvoiceInFuture
17. getExportList
18. requestWalletSettlement
19. requestGuildSettlement
20. requestSettlementByTool
21. listSettlements
22. addAutoSettlement
23. removeAutoSettlement
24. getPayInvoiceByWalletLink
25. getPayInvoiceByUniqueNumberLink
26. guildList
27. addDealer
28. dealerList
29. enableDealer
30. disableDealer
31. businessDealingList
32. issueMultiInvoice
33. reduceMultiInvoice
34. addDealerProductPermission
35. dealerProductPermissionList
36. dealingProductPermissionList
37. disableDealerProductPermission
38. enableDealerProductPermission
<div class="box-end">
</div>

## گرفتن توکن یکبارمصرف
1. getOtt: برای گرفتنott (توکن یک بار مصرف) از این تابع استفاده می شود


```
let getOttData = {
  // ------ REQUIRED ------
  // ------ OPTIONAL ------
};

podBillingService.getOtt(getOttData)
  .then(function (result) {
    console.log('function: getOtt ============>', result, '\n');
  })
  .catch(function (error) {
    console.log('error getOtt ============>', error);
  });
```

نمونه خروجی:

```
{ hasError: false,
  messageId: 0,
  referenceNumber: '234890294',
  errorCode: 0,
  count: 0,
  ott: 'e3b3e04303a09500' }
```

<div class="box-end">
</div>

## ایجاد فاکتور
2. issueInvoice: با این تابع می توانید یک فاکتور ایجاد کنید. ott مورد نیاز را از تابع  getOtt دریافت کنید. مقدار پیش فرض مالیات برابر با 0.09  است.

```
let issueInvoiceData = {
  // ------ REQUIRED ------
  _ott_: 'OTT', // get the ott from getOtt API
  productList: [
    { productId: 0, price: 0, quantity: 0, productDescription: 'DESCRIPTION' },
    { productId: 0, price: 0, quantity: 0, productDescription: 'DESCRIPTION' }
  ],
  guildCode: 'GUILD CODE'

  // ------ OPTIONAL ------
  // redirectURL: 'REDIRECT URL'
  // userId: USER ID
  // billNumber: 'BILL NUMBER'
  // description: 'DESCRIPTION'
  // deadline: 'DEADLINE'
  // currencyCode: 'CURRENCY CODE'
  // addressId: ADDRESS ID
  // voucherHash: 'VOUCHER HASH'
  // preferredTaxRate: TAX RATE
  // verificationNeeded: true | false
  // verifyAfterTimeout: true | false
  // preview: true | false
  // metadata: OBJECT
  // safe: 'SAFE'
  // postVoucherEnabled: 'POST VOUCHER ENABLED'
  // hasEvent: 'HAS EVENT'
  // eventTitle: 'EVENT TITLE'
  // eventTimeZone: 'TIME ZONE'
  // eventReminders: ARRAY OF OBJECTS
  // eventDescription: 'DESCRIPTION'
  // eventMetadat: OBJECT
};
podBillingService.issueInvoice(issueInvoiceData)
  .then(function (result) {
    console.log('function: issueInvoice ============>', result, '\n');
  })
  .catch(function (error) {
    console.log('error issueInvoice ============>', error);
  });
```

نمونه خروجی:

```
{ hasError: false,
  messageId: 0,
  referenceNumber: '234895676',
  errorCode: 0,
  count: 0,
  ott: 'd88757b1f3e9a198',
  result:
   { id: 3523363,
     totalAmountWithoutDiscount: 2200,
     delegationAmount: 0,
     totalAmount: 2200,
     payableAmount: 2398,
     vat: 198,
     issuanceDate: 1563105877970,
     deliveryDate: 0,
     paymentBillNumber: '6043042',
     uniqueNumber: 'ca7c5292f173673c',
     paymentDate: 0,
     payed: false,
     serial: 0,
     canceled: false,
     cancelDate: 0,
     business:
      { id: 3605,
        name: '&#x641;&#x646;&#x627;&#x67E; &#x62A;&#x633;&#x62A; &#x645;&#x634;&#x647;&#x62F;',
        numOfProducts: 3,
        rate: [Object],
        sheba: '080570100611513898506001' },
     invoiceItemSrvs: [ [Object], [Object] ],
     guildSrv:
      { id: 47,
        name: '&#x641;&#x646;&#x627;&#x648;&#x631;&#x6CC; &#x627;&#x637;&#x644;&#x627;&#x639;&#x627;&#x62A;',
        code: 'INFORMATION_TECHNOLOGY_GUILD' },
     userSrv:
      { id: 1453911,
        name: '&#x627;&#x62D;&#x633;&#x627;&#x646; &#x634;&#x6A9;&#x627;&#x631;&#x6CC;',
        ssoId: '6253140',
        ssoIssuerCode: 1,
        profileImage: 'https://core.pod.land:443/nzh/image/?imageId=104132&width=409&height=409&hashCode=16afd4e69b5-0.30817062367834125' },
     phoneNumber: '05138945234',
     cellphoneNumber: '09155234338',
     closed: false,
     verificationNeeded: false,
     metadata: '{"name":"ehsan"}',
     safe: false,
     postVoucherEnabled: false,
     referenceNumber: '234895676',
     issuerSrv:
      { id: 1454449,
        name: '&#x627;&#x62D;&#x633;&#x627;&#x646; &#x634;&#x6A9;&#x627;&#x631;&#x6CC;',
        ssoId: '6254762',
        ssoIssuerCode: 1,
        profileImage: 'https://core.pod.land:443/nzh/image/?imageId=69962&width=498&height=498&hashCode=16a679c6ad9-0.3413974672033351' },
     willBeBlocked: false,
     willBePaid: false,
     edited: false,
     waiting: false,
     subInvoice: false } }
```

<div class="box-end">
</div>

## ایجاد پیش‌فاکتور
3. createPreInvoice: با استفاده از این تابع می توانید یک پیش فاکتور ایجاد کنید. از خروجی این تابع می توانید لینک نمایش این پیش فاکتور را دریافت کنید. با ورود کاربر به صفحه پرداخت این فاکتور برای شما ثبت خواهد شد.

```
let createPreInvoiceData = {
  // ------ REQUIRED ------
  _ott_: 'OTT',
  productList: [
    { productId: 0, price: 0, quantity: 0, productDescription: 'My first product!' },
    { productId: 0, price: 0, quantity: 0, productDescription: 'My Second Product!' }
  ],
  guildCode: 'GUILD CODE',
  redirectURL: 'REDIRECT URL',
  userId: 0

  // ------ OPTIONAL ------
  // callUrl: 'CALL URL'
  // billNumber: 'BILL NUMBER'
  // description: 'DESCRIPTION'
  // deadline: 'DEADLINE'
  // currencyCode: 'CURRENCY CODE'
  // addressId: ADDRESS ID
  // preferredTaxRate: TAX RATE
  // verificationNeeded: true | false
};
podBillingService.createPreInvoice(createPreInvoiceData)
  .then(function (result) {
    console.log('function: createPreInvoice ============>', result, '\n');
  })
  .catch(function (error) {
    console.log('error createPreInvoice ============>', error);
  });
```


نمونه خروجی:


```
{ Ott: 'ZMwBqgyu7W',
  ErrorCode: 0,
  Count: 0,
  Result:
   { hash: 'YqKvIug6fuvqgj8P',
     url: 'https://pay.pod.land/v1/pbc/preinvoice/YqKvIug6fuvqgj8P' },
  ErrorMessage: null,
  HasError: false }
```

<div class="box-end">
</div>

## گرفتن لیست فاکتورها

4. getInvoiceList: با این تابع می توانید لیست فاکتورهای خود را ببنید و در آن ها بر اساس معیارهای مختلف همانند وضعیت و تاریخ جست و جو کنید

```
let getInvoiceListData = {
  // ------ REQUIRED ------
  offset: 0

  // ------ OPTIONAL ------
  // size: SIZE
  // id: ID
  // billNumber: 'BILL NUMBER'
  // uniqueNumber: 'UNIQUE NUMBER'
  // trackerId: ID
  // fromDate: 'FROM DATE'
  // toDate: 'TO DATE'
  // isCanceled: true | false
  // isPayed: true | false
  // isClosed: true | false
  // isWaiting: true | false
  // guildCode: 'GUILD CODE'
  // referenceNumber: 'REFERENCE NUMBER'
  // userId: ID
  // issuerId: ID
  // query: 'QUERY'
  // firstId: ID
  // lastId: ID
  // productIdList: ARRAY OF INTEGERS
};

podBillingService.getInvoiceList(getInvoiceListData)
  .then(function (result) {
    console.log('function: getInvoiceList ============>', result, '\n');
  })
  .catch(function (error) {
    console.log('error getInvoiceList ============>', error);
  });
```

نمونه خروجی:

```
{ hasError: false,
  messageId: 0,
  referenceNumber: '234905523',
  errorCode: 0,
  count: 412,
  ott: '38a87663be64292e',
  result:
   [ { id: 3523587,
       totalAmountWithoutDiscount: 2200,
       delegationAmount: 0,
       totalAmount: 2200,
       payableAmount: 2398,
       vat: 198,
       issuanceDate: 1563106619707,
       deliveryDate: 0,
       paymentBillNumber: '6043350',
       uniqueNumber: '5d5bebef79ea180',
       paymentDate: 0,
       payed: false,
       serial: 0,
       canceled: false,
       cancelDate: 0,
       business: [Object],
       invoiceItemSrvs: [Object],
       guildSrv: [Object],
       userSrv: [Object],
       phoneNumber: '05138945234',
       cellphoneNumber: '09155234338',
       closed: false,
       verificationNeeded: false,
       metadata: '{"name":"ehsan"}',
       safe: false,
       postVoucherEnabled: false,
       referenceNumber: '234905206',
       issuerSrv: [Object],
       willBeBlocked: false,
       willBePaid: false,
       waiting: false,
       edited: false,
       subInvoice: false } ],
  aggregations:
   { payableAmountSum: 393306599.7,
     delegationAmountSum: 0,
     totalAmountSum: 361229841 } }
```

<div class="box-end">
</div>

## پرداخت فاکتور 
5. payInvoice: با این تابع می توانید پرداخت های غیر متعارف (خارج از پلتفرم را کنترل کنید) به عنوان مثال اگر مبلغ فاکتور را به صورت حضوری از مشتری دریافت کردید می توانید با صدا زدن این تابع وضعیت فاکتور مورد نظر خود را به صورت پرداخت شده ببرید.

```
let payInvoiceData = {
  // ------ REQUIRED ------
  invoiceId: 0

  // ------ OPTIONAL ------
};

podBillingService.payInvoice(payInvoiceData)
  .then(function (result) {
    console.log('function: payInvoice ============>', result, '\n');
  })
  .catch(function (error) {
    console.log('error payInvoice ============>', error);
  });
```


نمونه خروجی:


```
{ hasError: false,
  messageId: 0,
  referenceNumber: '234910992',
  errorCode: 0,
  count: 0,
  ott: 'c1c25f4661687649',
  result: true }
```

<div class="box-end">
</div>

## ارسال پیامک پرداخت فاکتور
6. sendInvoicePaymentSMS: با استفاده از این تابع می توانید پیامک پرداخت فاکتور را برای کاربر ارسال کنید و در صورت تایید او فاکتور پرداخت خواهد شد.

```
let sendInvoicePaymentSMSData = {
  // ------ REQUIRED ------
  invoiceId: 0

  // ------ OPTIONAL ------
  // wallet: 'WALLET NAME'
  // callbackUri: 'CALLBACK URI'
  // redirectUri: 'REDIRECT URI'
  // delegationId: ARRAY OF INTEGERS
  // forceDeligation: 'FORCE DELIGATION'
};

podBillingService.sendInvoicePaymentSMS(sendInvoicePaymentSMSData)
  .then(function (result) {
    console.log('function: sendInvoicePaymentSMS ============>', result, '\n');
  })
  .catch(function (error) {
    console.log('error sendInvoicePaymentSMS ============>', error);
  });
```


نمونه خروجی

```
{ hasError: false,
  messageId: 0,
  referenceNumber: '234913357',
  errorCode: 0,
  count: 0,
  ott: 'de229e25d169d116',
  result: true }
```

<div class="box-end">
</div>

## گرفتن لیست فاکتورها بر اساس متادیتا
7. getInvoiceListByMetadata: در هنگام ثبت فاکتور می توانید اطلاعات دلخواه خود را در کلید metadata قرار دهید. در صورتی که بخواهید در بین متا دیتای فاکتورهای خود جستجو کنید می توانید از این تابع استفاده کنید.

```
let getInvoiceListByMetadataData = {
  // ------ REQUIRED ------

  // ------ OPTIONAL ------
  // metaQuery: OBJECT
  // offset: OFFSET
  // size: SIZE
  // isPayed: true | false
  // isCancelled: true | false
};

podBillingService.getInvoiceListByMetadata(getInvoiceListByMetadataData)
  .then(function (result) {
    console.log('function: getInvoiceListByMetadata ============>', result, '\n');
  })
  .catch(function (error) {
    console.log('error getInvoiceListByMetadata ============>', error);
  });
```

نمونه خروجی

```
{ hasError: false,
  messageId: 0,
  referenceNumber: '234915872',
  errorCode: 0,
  count: 206,
  ott: '38f43a3dac677549',
  result:
   [ { id: 3523723,
       totalAmountWithoutDiscount: 2200,
       delegationAmount: 0,
       totalAmount: 2200,
       payableAmount: 2398,
       vat: 198,
       issuanceDate: 1563107220446,
       deliveryDate: 0,
       paymentBillNumber: '6043554',
       uniqueNumber: 'f4428c9d7d82595f',
       paymentDate: 0,
       payed: false,
       serial: 0,
       canceled: false,
       cancelDate: 0,
       business: [Object],
       invoiceItemSrvs: [Object],
       guildSrv: [Object],
       userSrv: [Object],
       phoneNumber: '05138945234',
       cellphoneNumber: '09155234338',
       closed: false,
       verificationNeeded: false,
       metadata: '{"name":"ehsan"}',
       safe: false,
       postVoucherEnabled: false,
       referenceNumber: '234913356',
       issuerSrv: [Object],
       willBeBlocked: false,
       willBePaid: false,
       edited: false,
       waiting: false,
       subInvoice: false } ],
  aggregations: { totalAmountSum: 39762160 } }
```

<div class="box-end">
</div>

## گرفتن لیست فاکتورها به صورت فایل

8. getInvoiceListAsFile: ا این تابع می توانید بر اساس پارامترهای مختلف فاکتورها را فیلتر کنید و از نتیجه حاصل یک فایل اکسل تولید کنید. خروجی این تابع دارای خصیصه id ساخت که در ادامه برای دانلود فایل اکسل مورد نیاز است. ساخت فایل اکسل مدت زمانی طول می کشید و برای دریافت آن باید از تابع getExportList و id گرفته شده در این مرحله استفاده کرد.

```
let getInvoiceListAsFileData = {
  // ------ REQUIRED (One of these fields is required) ------
  lastNRows: 0,
  fromDate: 'YYYY/MM/DD HH:MM:SS', // or 'YYYY/MM/DD'
  toDate: 'YYYY/MM/DD HH:MM:SS' // or 'YYYY/MM/DD'

  // ------ OPTIONAL ------
  // id: ID
  // billNumber: 'BILL NUMBER'
  // uniqueNumber: 'UNIQUE NUMBER'
  // trackerId: ID
  // isCancelled: true | false
  // isPayed: true | false
  // isClosed: true | false
  // isWaiting: true | false
  // guildCode: 'GUILD CODE'
  // referenceNumber: 'REFERENCE NUMBER'
  // query: 'QUERY'
  // productIdList: ARRAY OF INTEGERS
  // callbackUrl: 'CALL BACK URL'
};

podBillingService.getInvoiceListAsFile(getInvoiceListAsFileData)
  .then(function (result) {
    console.log('function: getInvoiceListAsFile ============>', result, '\n');
  })
  .catch(function (error) {
    console.log('error getInvoiceListAsFile ============>', error);
  });
```

نمونه خروجی

```
{ hasError: false,
  messageId: 0,
  referenceNumber: '234922848',
  errorCode: 0,
  count: 0,
  ott: '6597da3e76c88f4f',
  result:
   { id: 1714,
     statusCode: 'EXPORT_SERVICE_STATUS_CREATED',
     creationDate: 1563107956237,
     service: '/nzh/biz/getInvoiceList/' } }
```

<div class="box-end">
</div>

## تایید فاکتور
9. verifyInvoice: اگر در هنگام صدور فاکتور کلید verificationNeeded را برابر با true قرار دهیم. فاکتور سه مرحله ایجاد شده و با استفاده از این تابع بعد از پرداخت فاکتور، می توانید پرداخت شدن آن را تایید کنید.

```
let verifyInvoiceData = {
  // ------ REQUIRED (One of these fields is required) ------
  id: 0, // Invoice ID
  billNumber: 'BILLNUMBER'

  // ------ OPTIONAL ------
};
podBillingService.verifyInvoice(verifyInvoiceData)
  .then(function (result) {
    console.log('function: verifyInvoice ============>', result, '\n');
  })
  .catch(function (error) {
    console.log('error verifyInvoice ============>', error);
  });
```

<div class="box-end">
</div>

## ابطال فاکتور
10. cancelInvoice: با استفاده از این تابع می توانید یک فاکتور را ابطال کنید.

```
let cancelInvoiceData = {
  // ------ REQUIRED ------
  id: 0 // Invoice ID

  // ------ OPTIONAL ------
};
podBillingService.cancelInvoice(cancelInvoiceData)
  .then(function (result) {
    console.log('function: cancelInvoice ============>', result, '\n');
  })
  .catch(function (error) {
    console.log('error cancelInvoice ============>', error);
  });
```

نمونه خروجی:

```
{ hasError: false,
  messageId: 0,
  referenceNumber: '234931814',
  errorCode: 0,
  count: 0,
  ott: 'f8db5afde57bfdb1',
  result: true }
```

<div class="box-end">
</div>

## کاهش فاکتور
11. reduceInvoice: در مواردی ممکن است نیاز به تغییری در بندهای فاکتور داشته باشید. در صورتی که فاکتور پرداخت نشده است، فاکتور قبلی را باطل (cancel) نمایید و فاکتور جدیدی صادر کنید. اگر فاکتور پرداخت شده است(در صورتی که باید پول بیشتری از مشتری دریافت نمایید)، لازم است فاکتوری جداگانه به مبلغ افزوده شده، با ذکر دلیل صادر نموده و مشتری را مجددا برای پرداخت هدایت نمایید. <u>در برخی مواقع لازم است مبلغی از فاکتور پرداخت شده به مشتری بازگردانده شود. برای این منظور از این تابع استفاده کنید.</u>

```
let reduceInvoiceData = {
  // ------ REQUIRED ------
  id: 0, // INVOICE ID
  invoiceItemList: [
    { productId: 0, price: 0, quantity: 0, productDescription: 'DESCRIPTION' },
    { productId: 0, price: 0, quantity: 0, productDescription: 'DESCRIPTION' }
  ]

  // ------ OPTIONAL ------
  // preferredTaxRate: TAX RATE

};
podBillingService.reduceInvoice(reduceInvoiceData)
  .then(function (result) {
    console.log('function: reduceInvoice ============>', result, '\n');
  })
  .catch(function (error) {
    console.log('error reduceInvoice ============>', error);
  });
```

نمونه خروجی:

```
{ hasError: false,
  messageId: 0,
  referenceNumber: '234937866',
  errorCode: 0,
  count: 0,
  ott: 'd853f7108a9ecf2f',
  result:
   { id: 3524200,
     totalAmountWithoutDiscount: 30,
     delegationAmount: 0,
     totalAmount: 30,
     payableAmount: 30,
     vat: 0,
     issuanceDate: 1563109099536,
     deliveryDate: 0,
     paymentBillNumber: '6044300',
     uniqueNumber: '14b6d913730ea2d7',
     paymentDate: 0,
     payed: false,
     serial: 0,
     canceled: false,
     cancelDate: 0,
     business:
      { id: 3605,
        name: '&#x641;&#x646;&#x627;&#x67E; &#x62A;&#x633;&#x62A; &#x645;&#x634;&#x647;&#x62F;',
        numOfProducts: 3,
        rate: [Object],
        sheba: '080570100611513898506001' },
     invoiceItemSrvs: [ [Object], [Object] ],
     guildSrv:
      { id: 47,
        name: '&#x641;&#x646;&#x627;&#x648;&#x631;&#x6CC; &#x627;&#x637;&#x644;&#x627;&#x639;&#x627;&#x62A;',
        code: 'INFORMATION_TECHNOLOGY_GUILD' },
     userSrv:
      { id: 1453911,
        name: '&#x627;&#x62D;&#x633;&#x627;&#x646; &#x634;&#x6A9;&#x627;&#x631;&#x6CC;',
        ssoId: '6253140',
        ssoIssuerCode: 1,
        profileImage: 'https://core.pod.land:443/nzh/image/?imageId=104132&width=409&height=409&hashCode=16afd4e69b5-0.30817062367834125' },
     phoneNumber: '05138945234',
     cellphoneNumber: '09155234338',
     closed: false,
     verificationNeeded: false,
     editedInvoiceId: 3524198,
     metadata: '{"name":"ehsan"}',
     safe: false,
     postVoucherEnabled: false,
     referenceNumber: '234937866',
     issuerSrv:
      { id: 1454449,
        name: '&#x627;&#x62D;&#x633;&#x627;&#x646; &#x634;&#x6A9;&#x627;&#x631;&#x6CC;',
        ssoId: '6254762',
        ssoIssuerCode: 1,
        profileImage: 'https://core.pod.land:443/nzh/image/?imageId=69962&width=498&height=498&hashCode=16a679c6ad9-0.3413974672033351' },
     willBeBlocked: false,
     willBePaid: false,
     waiting: false,
     edited: false,
     subInvoice: false } }
```

<div class="box-end">
</div>

## تایید و بستن فاکتور
12. verifyAndCloseInvoice: اگر در هنگام صدور فاکتور کلید verificationNeeded را برابر با true قرار دهیم. فاکتور سه مرحله ایجاد شده و با استفاده از این تابع بعد از پرداخت فاکتور، می توانید پرداخت شدن آن را تایید کنید و همزمان فاکتور را نیز ببندید.

```
let verifyAndCloseInvoiceData = {
  // ------ REQUIRED ------
  id: 0 // INVOICE ID

  // ------ OPTIONAL ------
};

podBillingService.verifyAndCloseInvoice(verifyAndCloseInvoiceData)
  .then(function (result) {
    console.log('function: verifyAndCloseInvoice ============>', result, '\n');
  })
  .catch(function (error) {
    console.log('error verifyAndCloseInvoice ============>', error);
  });
```

<div class="box-end">
</div>

## بستن فاکتور
13. closeInvoice: با این تابع می توانید یک فاکتور را ببندید. دقت داشته باشید برای تسویه باید فاکتورها را بسته باشید.

```
let closeInvoiceData = {
  // ------ REQUIRED ------
  id: 0 // INVOICE ID

  // ------ OPTIONAL ------
};

podBillingService.closeInvoice(closeInvoiceData)
  .then(function (result) {
    console.log('function: closeInvoice ============>', result, '\n');
  })
  .catch(function (error) {
    console.log('error closeInvoice ============>', error);
  });
```


نمونه خروجی
<br>

```
{ hasError: false,
  messageId: 0,
  referenceNumber: '234953365',
  errorCode: 0,
  count: 0,
  ott: '9407b53648854388',
  result: true }
```

<div class="box-end">
</div>

## گرفتن لینک پرداخت فاکتور
14. getInvoicePaymentLink: با این تابع می توانید لینک پرداخت یک فاکتور را دریافت کنید و فاکتور را از طریق درگاه بانکی پرداخت کنید

```
let getInvoicePaymentLinkData = {
  // ------ REQUIRED ------
  invoiceId: 0 // INVOICE ID

  // ------ OPTIONAL ------
  // callbackUri: 'CALLBACK URI'
  // redirectUri: 'REDIRECT URI'
  // gateway: 'PEP'
};

podBillingService.getInvoicePaymentLink(getInvoicePaymentLinkData)
  .then(function (result) {
    console.log('function: getInvoicePaymentLink ============>', result, '\n');
  })
  .catch(function (error) {
    console.log('error getInvoicePaymentLink ============>', error);
  });
```


نمونه خروجی
<br>

```
{ hasError: false,
  messageId: 0,
  referenceNumber: '234959959',
  errorCode: 0,
  count: 0,
  ott: 'dcdfd6a89be5232e',
  result: 'https://gw.pod.land/v1/pbc/PayInvoiceDispatcher/?h=a2c55acb239f4ef184222ce4662bb6bc&' }
```

<div class="box-end">
</div>

## پرداخت فاکتور به وسیله‌ی فاکتور
15. payInvoiceByInvoice: از طریق این سرویس کسب و کار قادر خواهد بود که پرداخت شدن برخی فاکتورهای خود را منوط به پرداخت شدن فاکتورهای دیگری نماید. یا به عبارتی نوعی تهاتر را بوسیله فاکتورها انجام دهد.

```
let payInvoiceInFutureData = {
  // ------ REQUIRED ------
  invoiceId: 0, // INVOICE ID
  date: 'YYYY/MM/DD'

  // ------ OPTIONAL (Use just one of them) ------
  // guildCode: 'GUILD CODE'
  // wallet: 'WALLET'
};

podBillingService.payInvoiceInFuture(payInvoiceInFutureData)
  .then(function (result) {
    console.log('function: payInvoiceInFuture ============>', result, '\n');
  })
  .catch(function (error) {
    console.log('error payInvoiceInFuture ============>', error);
  });
```

<div class="box-end">
</div>

## پرداخت فاکتور در آینده
16. payInvoiceInFuture: از طریق این تابع کسب و کار قادر خواهد بود فاکتورهایی که برایش توسط دیگران صادر شده را درتاریخ آینده یا سررسید توافقی از طریق مبلغی که در کیف پول یا اصناف خود دارد پرداخت نماید .این سرویس باید توسط کسب و کار یا کاربر بدهکار یا شخصی که فاکتور برایش صادر شده صدا زده شود.

```
let payInvoiceInFutureData = {
  // ------ REQUIRED ------
  invoiceId: 0, // INVOICE ID
  date: 'YYYY/MM/DD'

  // ------ OPTIONAL (Use just one of them) ------
  // guildCode: 'GUILD CODE'
  // wallet: 'WALLET'
};

podBillingService.payInvoiceInFuture(payInvoiceInFutureData)
  .then(function (result) {
    console.log('function: payInvoiceInFuture ============>', result, '\n');
  })
  .catch(function (error) {
    console.log('error payInvoiceInFuture ============>', error);
  });
```

<div class="box-end">
</div>

## گرفتن لیست خروجی
17. getExportList: این تابع لینک دانلود فایل های اکسل تولید شده را به شما خواهد داد. همچنین  با داشتن id ای که تابع getInvoiceListAsFile در خروجی می دهد می توانید تنها لینک دانلود فایل مورد نظر خود را استخراج کنید.

```
let getExportListData = {
  // ------ REQUIRED ------
  offset: 0,
  sie: 0

  // ------ OPTIONAL ------
  // id: ID
  // statusCode: 'EXPORT_SERVICE_STATUS_CREATED' | 'EXPORT_SERVICE_STATUS_RUNNING' |'EXPORT_SERVICE_STATUS_SUCCESSFUL' | 'EXPORT_SERVICE_STATUS_FAILED'
  // serviceUrl: 'SERVICE URL'
};

podBillingService.getExportList(getExportListData)
  .then(function (result) {
    console.log('function: getExportList ============>', result, '\n');
  })
  .catch(function (error) {
    console.log('error getExportList ============>', error);
  });
```


نمونه خروجی
<br>

```
{ hasError: false,
  messageId: 0,
  referenceNumber: '234993235',
  errorCode: 0,
  count: 49,
  ott: '46d38b30c28d1985',
  result:
   [ { id: 1714,
       statusCode: 'EXPORT_SERVICE_STATUS_SUCCESSFUL',
       creationDate: 1563107956237,
       resultFile: [Object],
       service: '/nzh/biz/getInvoiceList/' } ] }
```

<div class="box-end">
</div>

## درخواست تسویه‌حساب کیف پول
18. requestWalletSettlement: این تابع انتقال پول از کیف پول به حساب بانکی را انجام می دهد. به عبارت دیگر مبلغ مورد نظر خود را با استفاده از این تابع می توانید از کیف پول خود به حساب بانکی منقل کنید.

```
let requestWalletSettlementData = {
  // ------ REQUIRED ------
  _ott_: 'OTT',
  amount: 0

  // ------ OPTIONAL ------
  // wallet: 'WALLET'
  // firstName: 'FIRST NAME'
  // lastName: 'LAST NAME'
  // sheba: 'SHEBA WITHOUT IR'
  // currencyCode: 'CURRENCY'
  // uniqueId: ID
  // description: 'DESCRIPTION'
};

podBillingService.requestWalletSettlement(requestWalletSettlementData)
  .then(function (result) {
    console.log('function: requestWalletSettlement ============>', result, '\n');
  })
  .catch(function (error) {
    console.log('error requestWalletSettlement ============>', error);
  });
```

<div class="box-end">
</div>

## درخواست تسویه‌حساب صنف
19. requestGuildSettlement: این تابع انتقال پول ازهر یک از حساب های صنفی را به حساب بانکی انجام می دهد.

```
let requestGuildSettlementData = {
  // ------ REQUIRED ------
  _ott_: 'OTT',
  amount: 0,
  guildCode: 'GUILD CODE'

  // ------ OPTIONAL ------
  // firstName: 'FIRST NAME'
  // lastName: 'LAST NAME'
  // sheba: 'SHEBA WITHOUT IR'
  // currencyCode: 'CURRENCY'
  // uniqueId: ID
  // description: 'DESCRIPTION'
};

podBillingService.requestGuildSettlement(requestGuildSettlementData)
  .then(function (result) {
    console.log('function: requestGuildSettlement ============>', result, '\n');
  })
  .catch(function (error) {
    console.log('error requestGuildSettlement ============>', error);
  });
```

<div class="box-end">
</div>

## درخواست تسویه‌حساب با ابزار
20. requestSettlementByTool: این تابع انتقال پول از هر یک از حساب های صنفی را به حساب بانکی انجام می دهد. علاوه بر این با استفاده از این تابع می توانید انتخاب  کنید که به چه روشی و به کدام حساب پول (کارت یا شبا) منتقل شود. در صورت استفاده از ابزار کارت به کارت، کارمزد بانکی از حساب کسب و کار کسر خواهد شد و در صورت استفاده از ابزار پایا، انتقال وجه در زمان مصوب بانک مرکزی انجام خواهد شد.

```
let requestSettlementByToolData = {
  // ------ REQUIRED ------
  _ott_: 'OTT',
  amount: 0,
  guildCode: 'GUILD CODE',
  toolCode: 'TOLL CODE', // 'SETTLEMENT_TOOL_SATNA' | 'SETTLEMENT_TOOL_PAYA' |'SETTLEMENT_TOOL_CARD'
  toolId: 'TOOL ID'

  // ------ OPTIONAL ------
  // firstName: 'FIRST NAME'
  // lastName: 'LAST NAME'
  // currencyCode: 'CURRENCY'
  // uniqueId: ID
  // description: 'DESCRIPTION'
};

podBillingService.requestSettlementByTool(requestSettlementByToolData)
  .then(function (result) {
    console.log('function: requestSettlementByTool ============>', result, '\n');
  })
  .catch(function (error) {
    console.log('error requestSettlementByTool ============>', error);
  });
```

<div class="box-end">
</div>

## لیست تسویه‌حساب‌ها
21. listSettlements: با استفاده از این تابع می توانید لیست تسویه حساب های خود را ببینید یا در میان آن ها جست و جو کنید.

```
let listSettlementsData = {
  // ------ REQUIRED ------
  offset: 0

  // ------ OPTIONAL ------
  // size: SIZE
  // statusCode: 'SETTLEMENT_REQUESTED' | 'SETTLEMENT_SENT' | 'SETTLEMENT_DONE'
  // currencyCode: 'CURRENCY'
  // fromAmount: 'FROM AMOUNT'
  // toAmount: 'TO AMOUNT'
  // fromDate: 'YYYY/MM/DD'
  // toDate: 'YYYY/MM/DD'
  // uniqueId: ID
};

podBillingService.listSettlements(listSettlementsData)
  .then(function (result) {
    console.log('function: listSettlements ============>', result, '\n');
  })
  .catch(function (error) {
    console.log('error listSettlements ============>', error);
  });
```


نمونه خروجی
<br>

```
{ hasError: false,
  messageId: 0,
  referenceNumber: '235007513',
  errorCode: 0,
  count: 13,
  ott: 'c32730a6480962f8',
  result:
   [ { id: 107627,
       amount: 100,
       requestDate: 1562944712133,
       customerProfileSrv: [Object],
       settleDate: 1562944717025,
       status: 'SETTLEMENT_DONE',
       currency: [Object],
       toolCode: 'SETTLEMENT_TOOL_PAYA',
       toolId: '080570100611513898506001',
       firstName: '&#x627;&#x62D;&#x633;&#x627;&#x646;',
       lastName: '&#x634;&#x6A9;&#x627;&#x631;&#x6CC;',
       referenceId: '464674555',
       settlementLogSrvs: [Object],
       wallet: 'PODLAND_WALLET',
       instant: false,
       sendToBankDate: 1562944713414 } ] }
```

<div class="box-end">
</div>

## تسویه‌حساب خودکار
22. addAutoSettlement: در صورتی که تسویه خودکار برای یک کسب و کار فعال شود، مبلغ قابل تسویه آن کسب و کار به طور خودکار، یکبار در شبانه روز به شماره شبای اعلام شده در پروفایل کسب و کار یا شماره شبای اعلامی در سرویس زیر، تسویه می گردد.  با این تابع می توانید تسویه خودکار را بر روی هر کدام از حساب های صنفی خود فعال کنید.

```
let addAutoSettlementData = {
  // ------ REQUIRED ------
  guildCode: 'GUILD CODE'

  // ------ OPTIONAL ------
  // firstName: 'FIRST NAME'
  // lastName: 'LAST NAME'
  // sheba: 'SHEBA WITHOUT IR'
  // currencyCode: 'CURRENCY'
  // instant:  true | false
};

podBillingService.addAutoSettlement(addAutoSettlementData)
  .then(function (result) {
    console.log('function: addAutoSettlement ============>', result, '\n');
  })
  .catch(function (error) {
    console.log('error addAutoSettlement ============>', error);
  });
```


نمونه خروجی
<br>

```
{ hasError: false,
  messageId: 0,
  referenceNumber: '235010223',
  errorCode: 0,
  count: 0,
  ott: 'b3f16ddae760abcf',
  result: true }
```

<div class="box-end">
</div>

## حذف تسویه‌حساب خودکار
23. removeAutoSettlement: با استفاده از این تابع می توانید تسویه حساب خودکار را از روی هر کدام از حساب های صنفی غیر فعال کنید

```
let removeAutoSettlementData = {
  // ------ REQUIRED ------
  guildCode: 'GUILD CODE'

  // ------ OPTIONAL ------
  // currencyCode: 'CURRENCY'
};

podBillingService.removeAutoSettlement(removeAutoSettlementData)
  .then(function (result) {
    console.log('function: addAutoSettlement ============>', result, '\n');
  })
  .catch(function (error) {
    console.log('error addAutoSettlement ============>', error);
  });
```


نمونه خروجی
<br>

```
{ hasError: false,
  messageId: 0,
  referenceNumber: '235012100',
  errorCode: 0,
  count: 0,
  ott: '2abe8672df8a35a6',
  result: true }
```

<div class="box-end">
</div>

## گرفتن لینک پرداخت فاکتور با کیف پول
24. getPayInvoiceByWalletLink: با این تابع می توانید لینک پرداخت یک فاکتور را دریافت کنید و فاکتور را از طریق  کیف پول و یا درگاه بانکی پرداخت کنید

```
let getPayInvoiceByWalletLinkData = {
  // ------ REQUIRED ------
  invoiceId: 0 // INVOICEID

  // ------ OPTIONAL ------
  // redirectUri: 'REDIRECT URI'
  // callUri: 'CALL URI'
};

try {
  let url = podBillingService.getPayInvoiceByWalletLink(getPayInvoiceByWalletLinkData);
  console.log('function: addAutoSettlement ============>', url, '\n');
}
catch (error) {
  console.log('error getPayInvoiceByWalletLink ============>', error);
}
```


نمونه خروجی
<br>

```
https://pay.pod.land/v1/pbc/payInvoice/?invoiceid=3526061&redirectUri=http://www.google.com/&callUri=http://www.google.com/
```

<div class="box-end">
</div>

## گرفتن لینک پرداخت فاکتور
25. getPayInvoiceByUniqueNumberLink: با این تابع می توانید لینک پرداخت یک فاکتور را دریافت کنید و فاکتور را از درگاه بانکی پرداخت کنید

```
let getPayInvoiceByUniqueNumberLinkData = {
  // ------ REQUIRED ------
  uniqueNumber: 'UNIQUE NUMBER'

  // ------ OPTIONAL ------
  // redirectUri: 'REDIRECT URI'
  // callUri: 'CALL URI'
  // gateway: 'PEP'
};

try {
  let url = podBillingService.getPayInvoiceByUniqueNumberLink(getPayInvoiceByUniqueNumberLinkData);
  console.log('function: addAutoSettlement ============>', url, '\n');
}
catch (error) {
  console.log('error getPayInvoiceByWalletLink ============>', error);
}
```


نمونه خروجی
<br>

```
https://pay.pod.land/v1/pbc/payInvoiceByUniqueNumber/?uniqueNumber=7d85b52c6b4b9b32&redirectUri=http://www.google.com/&callUri=http://www.google.com/&gateway=PEP
```

<div class="box-end">
</div>

## لیست اصناف
26. guildList: با این تابع لیست اصناف را در اختیار شما قرار می دهد

```
let guildListData = {
  // ------ REQUIRED ------

  // ------ OPTIONAL ------
  // offset: OFFSET
  // size: SIZE
};

podBillingService.guildList(guildListData)
  .then(function (result) {
    console.log('function: addAutoSettlement ============>', result, '\n');
  })
  .catch(function (error) {
    console.log('error addAutoSettlement ============>', error);
  });
```


نمونه خروجی
<br>

```
{ hasError: false,
  messageId: 0,
  referenceNumber: '235022387',
  errorCode: 0,
  count: 43,
  ott: 'b5287d57d6bbf5b3',
  result:
   [ { id: 44, name: '&#x622;&#x631;&#x627;&#x6CC;&#x634; &#x648; &#x632;&#x6CC;&#x628;&#x627;&#x6CC;&#x6CC;', code: 'TOILETRIES_GUILD' },
     { id: 45, name: '&#x628;&#x647;&#x62F;&#x627;&#x634;&#x62A; &#x648; &#x62F;&#x631;&#x645;&#x627;&#x646;', code: 'HEALTH_GUILD' } ] }
```

<div class="box-end">
</div>

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
