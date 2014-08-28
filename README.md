### Webmoney

Модуль оплаты WalletOne

##### Подключение через Composer:

composer.json

    "require": {
        "fresh-design/iiifx-WalletOne": "dev-master"
    },
    "repositories": [
        {
            "type": "git",
            "url": "https://github.com/fresh-design/iiifx-WalletOne"
        }
    ]


##### Использование:

Отправка запроса с пользователем:

```php
use iiifx\Component\Payment\WalletOne\PaymentForm as WalletOneForm;

$sellerPurse = 123234345456;
$paymentAmount = 1.00;
$currencyCode = 643;
$orderId = 1000;
$paymentTypeList = array (
    'LiqPayMoneyRUB',
    'CreditCardRUB'
);

# Создаем форму
$w1Form = new WalletOneForm( $sellerPurse );

# Страницы на которые будут отправлены ответы
$w1Form
    ->setSuccessLink( "http://site.me/shop/payment/success/{$orderId}" )
    ->setFailLink( "http://site.me/shop/payment/fail/{$orderId}" );

# Задаем разрешенные методы оплаты
if ( $paymentTypeList && is_array( $paymentTypeList ) ) {
    foreach ( $paymentTypeList as $paymentType ) {
        $w1Form->addPaymentType( $paymentType );
    }
}

# Параметры оплаты
$w1Form
    ->setPaymentAmount( $paymentAmount )
    ->setCurrencyCode( $currencyCode )
    ->setPaymentId( $orderId )
    ->setComment( "Оплата заказа #{$orderId}" )
    ->addCustomerValue( 'orderId', $orderId );

# Проверяем данные
if ( $w1Form->validateData() ) {

    # Включаем автосабмит формы сразу после загрузки страницы
    $w1Form->enableFormAutoSubmit();

    # Выводим форму
    echo $w1Form->buildFormView();

}
```

Проверка результата оплаты Result

```php
	# ...
```

Получаем ответ на страницах Success / Fail

```php
    # ...
```