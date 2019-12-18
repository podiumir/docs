- [مقدمه](#menu)
- [دریافت اطلاعات کارت بانکی](#menu)
- [دریافت اطلاعات شبا](#menu)
- [لینک‌های مرتبط](#menu)

## مقدمه
** تمام امکانات سرویس‌های بانکی در پکیج Banking قرار دارد.برای اطلاعات بیشتر به [پکیج سرویس‌ها](/documents/packages/) مراجعه کنید**

<div class="box-end">
</div>

## دریافت اطلاعات کارت بانکی
دریافت اطلاعات کارت بانکی

<div class="tab-start">
</div>

# [C#](#tab/csharp)

``` csharp
try
    {
        var internalServiceCallVo = InternalServiceCallVo.ConcreteBuilder
            .SetToken("{Put your ApiToken}")
            //.SetScVoucherHash({Put your VoucherHash})
            //.SetScApiKey("{Put your ApiKey}")
            .Build();
            
    }
catch (PodException podException)
    {
        Console.WriteLine($"-- {podException.Code}-an error has occured : 
                              {Environment.NewLine{podException.Message}");
        throw;
    }
catch (Exception exception)
    {
        Console.WriteLine(exception.Message);
        throw;
    }
```
<div class="swaggerLink">http://core.pod.ir/apidocs/swagger-ui.html?srv=/nzh/biz/getDebitCardInfo/</div>

# [Java](#tab/java)

``` java
BaseInfoVo baseInfoVo = new BaseInfoVo.Builder()
                .setToken({TOKEN})
                .setToken_issuer(1)
                .setServerType(Enum_Server_type.SANDBOX)
//                .setScApiKey(API_KEY)
//                .setScVoucherHash(scVoucherHashs)
                .build();

        PodBank podBank = new PodBank();
        try {
            GetDebitCardInfoVo getDebitCardInfoVo = new GetDebitCardInfoVo.Builder(baseInfoVo)
                    .setCardNumber({cardNumber})
                    .build();
            podBank.getDebitCardInfo(getDebitCardInfoVo, new OnGetResponseListener<String>() {
                @Override
                public void onResponse(ResultVo<String> result) {
                    System.out.println(result.getResult());
                }

                @Override
                public void onFailed(PodException e) {
                    System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
                }
            });
        } catch (PodException e) {
            System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
        }
    }
To enable screen reader support, press Ctrl+Alt+Z To learn about keyboard shortcuts, press Ctrl+slash

```
<div class="swaggerLink">http://core.pod.ir/apidocs/swagger-ui.html?srv=/nzh/biz/getDebitCardInfo/</div>

# [PHP](#tab/php)

``` php
$param =
        [
            ## ============== Required Parameters  ====================
            "cardNumber"        => "Put Card Number",
            ## ============== Optional Parameters  ====================
            'token'                => 'Put token'
            'scVoucherHash'     => ['{Put Service Call Voucher Hashes}'],
            'scApiKey'          => '{Put service call Api Key}',
        ];
    try {
        $result = $BankingService->getDebitCardInfo($param);
        print_r($result);
    }
    catch (ValidationException $e) {
        print_r($e->getResult());
        print_r($e->getErrorsAsArray());
    } catch (PodException $e) {
        print_r($e->getResult());
    }
```
<div class="swaggerLink">http://core.pod.ir/apidocs/swagger-ui.html?srv=/nzh/biz/getDebitCardInfo/</div>

# [Nodejs](#tab/nodejs)

``` javascript
let getDebitCardInfoData = {
  // ------ REQUIRED ------
  cardNumber: '6280231465614898'

  // ------ OPTIONAL ------
  // scVoucherHash: ['HASH#1', 'HASH#2']
  // scApiKey: ' SC API KEY'

  // ------ OPTIONAL (JUST CHANGE THE CURRENT REQUEST) ------
  // token: 'TOKEN'
  // tokenIssuer: 0 | 1
};
podBanking.getDebitCardInfo(getDebitCardInfoData)
  .then(function (result) {
    console.log(JSON.stringify(result, null, 2));
  })
  .catch(function (error) {
    console.log(JSON.stringify(error, null, 2));
  });
```
<div class="swaggerLink">http://core.pod.ir/apidocs/swagger-ui.html?srv=/nzh/biz/getDebitCardInfo/</div>

<div class="tab-end">
</div>

<div class="box-end">
</div>

## دریافت اطلاعات شبا
دریافت اطلاعات شبا


<div class="tab-start">
</div>

# [C#](#tab/csharp)

``` csharp
try
    {
        var internalServiceCallVo = InternalServiceCallVo.ConcreteBuilder
            .SetToken("{Put your ApiToken}")
            //.SetScVoucherHash({Put your VoucherHash})
            //.SetScApiKey("{Put your ApiKey}")
            .Build();
            
    }
catch (PodException podException)
    {
        Console.WriteLine($"-- {podException.Code}-an error has occured : 
                              {Environment.NewLine{podException.Message}");
        throw;
    }
catch (Exception exception)
    {
        Console.WriteLine(exception.Message);
        throw;
    }
```
<div class="swaggerLink">http://core.pod.ir/apidocs/swagger-ui.html?srv=/nzh/biz/getShebaInfo/</div>

# [Java](#tab/java)

``` java
 BaseInfoVo baseInfoVo = new BaseInfoVo.Builder()
                .setToken({TOKEN})
                .setToken_issuer(1)
                .setServerType(Enum_Server_type.SANDBOX)
//                .setScApiKey(API_KEY)
//                .setScVoucherHash(scVoucherHashs)
                .build();

        PodBank podBank = new PodBank();
        try {
            GetShebaInfoVo getShebaInfoVo = new GetShebaInfoVo.Builder(baseInfoVo)
                    .setSheba({sheba})
                    .build();
            podBank.getShebaInfo(getShebaInfoVo, new OnGetResponseListener<ShebaInfoSrv>() {
                @Override
                public void onResponse(ResultVo<ShebaInfoSrv> result) {
                    System.out.println(result.getResult().getOwners().get(0).getLastName());
                }

                @Override
                public void onFailed(PodException e) {
                    System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
                }
            });
        } catch (PodException e) {
            System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
        }
```
<div class="swaggerLink">http://core.pod.ir/apidocs/swagger-ui.html?srv=/nzh/biz/getShebaInfo/</div>

# [PHP](#tab/php)

``` php
$param =
        [
            ## ============== Required Parameters  ====================
            "sheba"              => "Put Sheba Number",
            ## ============== Optional Parameters  ====================
            'token'                => 'Put token'
            'scVoucherHash'     => ['{Put Service Call Voucher Hashes}'],
            'scApiKey'           => '{Put service call Api Key}',
        ];
    try {
        $result = $BankingService->getShebaInfo($param);
        print_r($result);
    }
    catch (ValidationException $e) {
        print_r($e->getResult());
        print_r($e->getErrorsAsArray());
    } catch (PodException $e) {
        print_r($e->getResult());
    }
```
<div class="swaggerLink">http://core.pod.ir/apidocs/swagger-ui.html?srv=/nzh/biz/getShebaInfo/</div>

# [Nodejs](#tab/nodejs)

``` javascript

let getShebaInfoData = {
  // ------ REQUIRED ------
  sheba: 'SHEBA NUMBER'

  // ------ OPTIONAL ------
  // scVoucherHash: ['HASH#1', 'HASH#2']
  // scApiKey: ' SC API KEY'

  // ------ OPTIONAL (JUST CHANGE THE CURRENT REQUEST) ------
  // token: 'TOKEN'
  // tokenIssuer: 0 | 1
};
podBanking.getShebaInfo(getShebaInfoData)
  .then(function (result) {
    console.log(JSON.stringify(result, null, 2));
  })
  .catch(function (error) {
    console.log(JSON.stringify(error, null, 2));
  });
```
<div class="swaggerLink">http://core.pod.ir/apidocs/swagger-ui.html?srv=/nzh/biz/getShebaInfo/</div>

<div class="tab-end">
</div>

<div class="box-end">
</div>

## لینک‌های مرتبط

- [مقدمه](/documents/introduction/)
- [مفاهیم](/documents/concepts/)
- [استاندارد و خطاها](/documents/errors/)
- [شروع به کار](/documents/get-started/)
- [پکیج‌ها](/documents/packages/)

<div class="box-end">
</div>
