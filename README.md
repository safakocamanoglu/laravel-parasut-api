<a name="readme-top"></a>
[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![MIT License][license-shield]][license-url]
[![LinkedIn][linkedin-shield]][linkedin-url]




<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://istanbulwebtasarim.pro">
    <img src="https://istanbulwebtasarim.pro/images/istanbul-web-tasarim-logo.webp" alt="İstanbul Web Tasarım" style="width: 40%">
  </a>

<h3 align="center">Paraşüt API Laravel Package</h3>

[![Laravel][Laravel.com]][Laravel-url]
![Packagist Downloads (custom server)][downloads-url]


  <p align="center">
    Laravel için yazılmış Paraşüt V4 API paketi.
    <br />
    <a href="https://github.com/theposeidonas/laravel-parasut-api"><strong>Dökümantasyon »</strong></a>
    <br />
    <br />
    <a href="https://github.com/theposeidonas/laravel-parasut-api">Demo</a>
    ·
    <a href="https://github.com/theposeidonas/laravel-parasut-api/issues">Buglar</a>
    ·
    <a href="https://github.com/theposeidonas/laravel-parasut-api/issues">İstekler</a>
  </p>
</div>



<!-- TABLE OF CONTENTS -->
<details>
  <summary>İçindekiler</summary>
  <ol>
    <li>
      <a href="#about-the-project">Proje Hakkında</a>
    </li>
    <li>
      <a href="#getting-started">Başlarken</a>
      <ul>
        <li><a href="#prerequisites">İhtiyaçlar</a></li>
        <li><a href="#installation">Projenize Ekleme</a></li>
        <li><a href="#configuration">Konfigürasyon</a></li>
      </ul>
    </li>
    <li><a href="#usage">Kullanım</a></li>
      <ul>
        <li><a href="#classes">Sınıf</a></li>
        <li><a href="#functions">Fonksiyonlar</a></li>
        <li><a href="#data">Veri Gönderme Şekli</a></li>
      </ul>
    <li><a href="#todo">TODO</a></li>
    <li><a href="#license">Lisans</a></li>
    <li><a href="#contact">İletişim</a></li>
  </ol>
</details>


## Proje Hakkında

laravel-parasut-api Laravel için oluşturulmuş kolayca Paraşüt V4 API ile bağlantı kurmanızı sağlayacak bir pakettir. Paraşüt API bilgilerinizi .env dosyasına girdikten sonra tekrar tekrar Auth işlemleri ile uğraşmadan kolayca istediğiniz fonksiyonu çalıştırabilirsiniz.

### Neden ihtiyaç var?

Laravel için yazılmış hızlı ve basit bir Paraşüt API paketi. OAuth2 işlemlerini otomatik olarak yapan, token süresi dolmuşsa otomatik olarak yeni token alan ve Controller içerisine sadece yapacağınız işlemi yazdıran sade bir pakete ihyaç duyuyorduk. Biz de bunu baştan yazdık.

Bug ve Hataları lütfen Issues kısmından bildirin.


<p align="right">(<a href="#readme-top">Başa dön</a>)</p>


## Başlarken

Kullanacağınız proje Laravel projesi olmalıdır. Kurulumu yaptıktan sonra composer ile projenize ekleyebilirsiniz.

### İhtiyaçlar

Paraşüt için yapacağınız tüm işlemler öncesinde, mutlaka bilgileri .env dosyasına girmelisiniz.

### Projenize ekleme

Laravel projenizde terminali açarak şu komutu çalıştırın;

```shell
composer require theposeidonas/laravel-parasut-api
```

Eğer gerekiyorsa config dosyasını paylaşmak için şu komutu çalıştırın;

```shell
php artisan vendor:publish --tag=parasut-config --force
```

Eğer Laravel versiyonunuz eskiyse, her yerde kullanmak için config/app.php dosyasında 'aliases' kısmına şu kodu ekleyin;

```php
'Parasut' => Theposeidonas\LaravelParasutApi\Facades\Parasut::class,
```

### Konfigürasyon

Kullanım için projenize eklemeyi yaptıktan sonra, .env dosyası içerisinde yukarıya şu satırı ekleyip düzeltmelisiniz;
```dotenv
PARASUT_USERNAME="demo@parasut.com"  // Username
PARASUT_PASSWORD="XXXXXXXXX"  // Password
PARASUT_IS_STAGE="0"  // TODO Staging aktif değil şimdilik default olarak 0
PARASUT_COMPANY_ID="123123" // Company ID
PARASUT_CLIENT_ID="XXXXXXXXXXXXXXXXX" // Paraşüt Client ID
PARASUT_CLIENT_SECRET="XXXXXXXXXXXXXXXXX" // Paraşüt Client Secret
PARASUT_REDIRECT_URI="urn:ietf:wg:oauth:2.0:oob" // Paraşüt Redirect URI, değiştirmenize gerek yok 
```
<p align="right">(<a href="#readme-top">Başa dön</a>)</p>


## Kullanım

Kullanacağınız Controller içerisine paketi dahil etmeniz gerekiyor;

```php   
use Theposeidonas\LaravelParasutApi\Facades\Parasut;
```

#### Sınıflar
Tüm ayarlamaları ve konfigürasyonlarınızı yaptıktan sonra kullanacağınız Controller içerisinde belirli sınıfları çağırabilirsiniz. Bu sınıflar şu şekilde;

```php
/* Satışlar */
Parasut::Bill();            // Satış faturası           https://apidocs.parasut.com/#tag/SalesInvoices
Parasut::Customer();        // Müşteri                  https://apidocs.parasut.com/#tag/Contacts
        
/* Giderler */      
Parasut::Receipt();         // Fiş - Fatura             https://apidocs.parasut.com/#tag/PurchaseBills
Parasut::Bank();            // Banka giderleri          https://apidocs.parasut.com/#tag/BankFees
Parasut::Salary();          // Maaş giderleri           https://apidocs.parasut.com/#tag/Salaries
Parasut::Tax();             // Vergi giderleri          https://apidocs.parasut.com/#tag/Taxes
Parasut::Supplier();        // Tedarikçi                https://apidocs.parasut.com/#tag/Contacts
Parasut::Employee();        // Çalışan                  https://apidocs.parasut.com/#tag/Employees
    
/* Resmileştirme */ 
Parasut::Inbox();           // E-Fatura Gelen Kutusu    https://apidocs.parasut.com/#tag/EInvoiceInboxes
Parasut::EArchive();        // E-Arşiv                  https://apidocs.parasut.com/#tag/EArchives
Parasut::EBill();           // E-Fatura                 https://apidocs.parasut.com/#tag/EInvoices
Parasut::ESmm();            // E SMM                    https://apidocs.parasut.com/#tag/ESmms
    
/* Nakit */ 
Parasut::Account();         // Kasa ve Banka            https://apidocs.parasut.com/#tag/Accounts
Parasut::Transaction();     // İşlem                    https://apidocs.parasut.com/#tag/Transactions
    
/* Stok */  
Parasut::Product();         // Ürün                     https://apidocs.parasut.com/#tag/Products
Parasut::Warehouse();       // Depo                     https://apidocs.parasut.com/#tag/Warehouses
Parasut::Waybill();         // İrsaliye                 https://apidocs.parasut.com/#tag/ShipmentDocuments
Parasut::StockMovement();   // Stok Hareketi            https://apidocs.parasut.com/#tag/StockMovements

/* Ayarlar */
Parasut::Category();        // Kategori                 https://apidocs.parasut.com/#tag/ItemCategories
Parasut::Tag();             // Etiket                   https://apidocs.parasut.com/#tag/Tags
```

_Bunlar dışında kalan, ürünlerin stok seviyesini kontrol etmek için ```Parasut::Product()->inventory($id); ``` kullanmanız gerekir._

#### Fonksiyonlar

Paraşüt içindeki sınıfları kullanırken, https://apidocs.parasut.com sayfasında yer alan fonksiyonları kullanabilirsiniz.

Örneğin;  
Müşteri index fonksiyonu için:  ```Parasut::Customer()->index(); ```  
Müşteri create fonksiyonu için: ```Parasut::Customer()->create($data); ```  
Müşteri show fonksiyonu için: ```Parasut::Customer()->show($id); ```  
Müşteri edit fonksiyonu için: ```Parasut::Customer()->edit($id, $data); ```

şeklinde kullanabilirsiniz. Dökümanlarda gösterilen tüm fonksiyonlar mevcuttur.

##### Veri gönderme şekli

Bir sınıfta create fonksiyonu için veri gönderirken, https://apidocs.parasut.com tarafında bahsedilen gibi veri göndermelisiniz. Fakat veriyi JSON olarak değil, Array olarak göndermeniz gereklidir.

Örnek Müşteri oluşturma;
```php
$customer = [
            'data'=>[
                'type'=>'contacts',
                'attributes'=>[
                    'email'=>'demo@parasut.com',
                    'name'=>'İsim Soyisim',
                    'contact_type'=>'person',
                    'tax_number'=>'11111111111',
                    'account_type'=>'customer'
                ]
            ]
        ];
$response = Parasut::Customer()->create($customer);
```

Eğer işlemleriniz başarılıysa size şöyle bir Array geri dönecektir;

```php
Array
(
    [success] => true // İşlem başarılı ise true
    [error] => false // İşlem başarısız ise true
    [body] => stdClass Object // Paraşüt dökümanlarında yazan response Object şeklinde
    [status] => 200 // Response Status
)
```

Yani geri dönüş yapan işlemi şu şekilde sorgulayabilirsiniz;
```php
if($response['success'])
{
    // İşlem başarılı ise yapılacak şeyler
}
$customer = Parasut::Customer()->show($response['body']->data->id);
echo $customer['body']->data->attributes->name; // Oluşturulan müşterinin ismini görme


```
<p align="right">(<a href="#readme-top">Başa dön</a>)</p>

### TODO

Eksikleri ve hataları Issues kısmından yazabilirsiniz.
- [x] Fonksiyonların hepsi dahil edildi
- [ ] Fonksiyonların ekstra parametreleri dahil edilecek (Query Parameters)
- [ ] Staging dahil edilecek (Api test modu)



<p align="right">(<a href="#readme-top">Başa dön</a>)</p>

<!-- LICENSE -->
## Lisanslama

MIT Lisansı altında dağıtılmaktadır. Daha fazla bilgi için 'LICENSE' dosyasına bakın.

<p align="right">(<a href="#readme-top">Başa dön</a>)</p>



<!-- CONTACT -->
## İletişim

Baran Arda - [@theposeidonas](https://twitter.com/theposeidonas) - info@baranarda.com

Proje Linki: [https://github.com/theposeidonas/laravel-parasut-api](https://github.com/theposeidonas/laravel-parasut-api)

<p align="right">(<a href="#readme-top">Başa dön</a>)</p>


<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/theposeidonas/laravel-parasut-api.svg?style=for-the-badge
[contributors-url]: https://github.com/theposeidonas/laravel-parasut-api/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/theposeidonas/laravel-parasut-api.svg?style=for-the-badge
[forks-url]: https://github.com/theposeidonas/laravel-parasut-api/network/members
[stars-shield]: https://img.shields.io/github/stars/theposeidonas/laravel-parasut-api.svg?style=for-the-badge
[stars-url]: https://github.com/theposeidonas/laravel-parasut-api/stargazers
[issues-shield]: https://img.shields.io/github/issues/theposeidonas/laravel-parasut-api.svg?style=for-the-badge
[issues-url]: https://github.com/theposeidonas/laravel-parasut-api/issues
[license-shield]: https://img.shields.io/github/license/theposeidonas/laravel-parasut-api.svg?style=for-the-badge
[license-url]: https://github.com/theposeidonas/laravel-parasut-api/blob/master/LICENSE.txt
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://www.linkedin.com/in/theposeidonas/
[Laravel.com]: https://img.shields.io/badge/Laravel-FF2D20?style=for-the-badge&logo=laravel&logoColor=white
[Laravel-url]: https://laravel.com
[downloads-url]: https://img.shields.io/packagist/dt/theposeidonas/laravel-parasut-api?style=for-the-badge&color=007ec6&cacheSeconds=3600