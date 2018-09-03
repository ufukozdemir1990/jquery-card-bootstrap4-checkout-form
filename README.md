# JQuery Card - Bootstrap 4 Checkout Form Validation

Demo: [http://www.ufukozdemir.website/github/jquery-card-bootstrap4-checkout-form/](http://www.ufukozdemir.website/github/jquery-card-bootstrap4-checkout-form/)

Orjinal
JQuery Card : [https://jessepollak.github.io/card/](https://jessepollak.github.io/card/)

Bootstrap Checkout Form: [https://getbootstrap.com/docs/4.1/examples/checkout/](https://getbootstrap.com/docs/4.1/examples/checkout/)

## Özellikler
 - Kart tipi algılama (Visa – Mastercard vs)
 - Alan doğrulaması (Boşluk – Özel Karakter)
 - Giriş maskelemesi
 - Numara, isim, tarih ve CVC’ye özel yer alan alanlar

## Kurulum
#### Adım 1 (***Gerekli dosyaların sayfa içerisine entegre edilmesi***)

```html
<!--  HEADER  -->
<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/css/bootstrap.min.css">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/card/2.4.0/card.css">

<!-- FOOTER -->
<script src="https://code.jquery.com/jquery-3.3.1.slim.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.3/umd/popper.min.js"></script>
<script src="https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/js/bootstrap.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/card/2.4.0/jquery.card.min.js"></script>
```
---

#### Adım 2 (***Kartın görüneceği alanı ve ödeme verisi giriş alanlarımızı oluşturalım***)
```html
<!-- Kartın Gözükeceği Class -->
<div class="card-wrapper"></div>

<!-- Kart Bilgilerinin Doldurulacağı Form -->
<div class="form-container active">  
    <div class="row">  
        <div class="col-md-6 mb-3">  
            <label for="cc-name">Ad Soyad</label>  
            <input type="text" class="form-control" id="cc-name" placeholder="" maxlength="40" name="name" required>  
            <small class="text-muted">Kredi kartı üzerinde yazılan ad soyad</small>  
            <div class="invalid-feedback">Ad Soyad alanı gerekli.</div>  
        </div>  
        <div class="col-md-6 mb-3">  
            <label for="cc-number">Kredi Kartı Numarası</label>  
            <input type="text" class="form-control" id="cc-number" placeholder="" name="number" required>  
            <div class="invalid-feedback">Kredi Kartı Numarası alanı gerekli.</div>  
        </div>  
    </div>  
    <div class="row">  
        <div class="col-md-3 mb-3">  
            <label for="cc-expiration">Son Kullanım Tarihi</label>  
            <input type="text" class="form-control" id="cc-expiration" placeholder="" name="expiry" required>  
            <small class="text-muted">AA/YY şeklinde</small>  
            <div class="invalid-feedback">Son Kullanım Tarihi alanı gerekli.</div>  
        </div>  
        <div class="col-md-3 mb-3">  
            <label for="cc-cvv">CVV</label>  
            <input type="text" class="form-control" id="cc-cvv" placeholder="" name="cvc" required>  
            <small class="text-muted">Kartın arkasındaki kod</small>  
            <div class="invalid-feedback">CVV alanı gerekli.</div>  
        </div>  
    </div>  
</div>
```

---
#### Adım 3 (***card.js ve bootstrap validation  bilgilerini sayfamıza tanımlayalım***)
> Lütfen Class bilgilerine dikkat ediniz! Kart formunun çalışmasını istediğiniz Class kendiniz belirleyebilirsiniz. Ben burada ana formuma tanımladım.
```javascript
// Card Form
$('.needs-validation').card({
    container: '.card-wrapper',
});

// JavaScript Form Validation
(function() {
    'use strict';

    window.addEventListener('load', function() {
        // Fetch all the forms we want to apply custom Bootstrap validation styles to
        var forms = document.getElementsByClassName('needs-validation');

        // Loop over them and prevent submission
        var validation = Array.prototype.filter.call(forms, function(form) {
            form.addEventListener('submit', function(event) {
                if (form.checkValidity() === false) {
                    event.preventDefault();
                    event.stopPropagation();
                }
                form.classList.add('was-validated');
            }, false);
        });
    }, false);
})();
```