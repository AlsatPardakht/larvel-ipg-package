
<p align="center">
  <a href="" rel="noopener">
 <img width=200px height=200px src="./logo.png" alt="Project logo"></a>
</p>

<h3 align="center">Alsat IPG Laravel Package</h3>

<div align="center">

[![Status](https://img.shields.io/badge/status-active-success.svg)]()
[![GitHub Issues](https://img.shields.io/github/issues/AlsatPardakht/AlsatIPGAndroid.svg)](https://github.com/AlsatPardakht/AlsatIPGAndroid/issues)
[![GitHub Pull Requests](https://img.shields.io/github/issues-pr/AlsatPardakht/AlsatIPGAndroid.svg)](https://github.com/AlsatPardakht/AlsatIPGAndroid/pulls)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](/LICENSE)

</div>

---

<p align="center">پکیج لاراولی درگاه آلسات پرداخت</p>

# گام اول
راهنمای نصب پکیج درگاه پرداخت آلسات پرداخت :
Install this package with composer
```bash
composer require alsatpardakht/payment
```
# گام دوم
You should publish and run the migrations with:

```bash
php artisan vendor:publish --provider="Alsatpardakht\Payment\PaymentServiceProvider" --tag="migrations"
```
# گام سوم
```bash
php artisan migrate
```

# گرفتن url جهت پرداخت
$pay = new Paymethods();
$params = [
    'Api' => env('payApi'),
    'Amount' => $payAmount,
    'RedirectAddress' => route('buyPayVerify'),
    'InvoiceNumber' => $order->InvoiceNumber
];

return $pay->getPayUrl($params);

# وریفای کردن پرداخت ها
$pay = new Paymethods();
$response = $pay->verifyPay($request, env('payApi'));
$order = 
$payLink = Paylink::where('InvoiceNumber', $request->iN)->first();
if ($response->getStatusCode() == 405) {
  //some problem occurred
} else if($response->getStatusCode() == 200) {
  //it is true
}

در متد بالا اگر ریسپانس شما 405 باشد پرداخت با مشکل مواجه شده است در صورتی که 200 از ریسپانس برگشت داده شود یعنی وریفای انجام شده است.

more methods:
1-getPayLinks($InvoiceNumber);
2-getPayLinksWithPaginate($InvoiceNumber,$count);
3-getPayVerify($InvoiceNumber);
4-getPayVerifyWithPaginate($InvoiceNumber,$count);
