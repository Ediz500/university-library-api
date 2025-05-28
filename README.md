# 📚 Üniversite Çevrim İçi Kütüphane API'si

Bu proje, **OpenAPI 3.0** standardını kullanarak bir üniversiteye ait çevrim içi kütüphane sistemini yönetmek için bir RESTful API tanımlar.

## 🎯 Amaç

- Kitaplar, öğrenciler ve kitap ödünç alma işlemlerini yönetmek için bir API tasarlamak.
- Kütüphane sistemi için CRUD uç noktalarını modellemek.
- OpenAPI özelliklerine göre şema, parametreler, yanıtlar ve örnek yapıları oluşturmak.

## 🧱 Varlıklar

### 1. Kitaplar

Kitap bilgilerini içerir.

- `id`, `title`, `author`, `isbn`, `publisher`, `pageCount`, `stock`

### 2. Öğrenciler

Öğrenci bilgilerini içerir.

- `id`, `name`, `studentNumber`, `email`, `isActive`

### 3. Ödünçler

Kitap ödünç alma işlem bilgilerini içerir.

- `id`, `studentId`, `bookId`, `loanDate`, `returnDate`, `status`

## 🔗 API Uç Noktaları

### Kitaplar

- `GET /books`: Tüm kitapları sayfalama ile listele.
- `GET /books/{id}`: Belirli bir kitabı ID'sine göre getir.
- `POST /books`: Yeni bir kitap ekle.
- `PUT /books/{id}`: Var olan bir kitabı güncelle.
- `DELETE /books/{id}`: Bir kitabı kütüphaneden sil.

### Öğrenciler

- `GET /students`: Tüm öğrencileri listele.
- `GET /students/{id}`: Belirli bir öğrenciyi ID'sine göre getir.
- `POST /students`: Yeni bir öğrenci ekle.
- `PUT /students/{id}`: Var olan bir öğrenciyi güncelle.
- `DELETE /students/{id}`: Bir öğrenciyi sistemden sil.

### Ödünçler

- `GET /loans`: Tüm ödünç kayıtlarını listele.
- `GET /loans/{id}`: Belirli bir ödünç kaydını ID'sine göre getir.
- `POST /loans`: Bir kitaba ödünç verme işlemi başlat.
- `PATCH /loans/{id}/return`: Bir kitabı iade et.

## 📁 Dosya Yapısı

- /
  - `openapi.yaml` # API tanımı (Swagger uyumlu)
  - `README.md` # Proje açıklaması
  - `DELIVERY.md` # Teslim formatı (Google Classroom'a yüklenecek dosya)

## 🚀 Test

Swagger Editor kullanarak test etmek için:  
👉 [https://editor.swagger.io/](https://editor.swagger.io/)

1. `openapi.yaml` dosyasını yükleyin.
2. Uç noktaları deneyerek doğru çalıştığını doğrulayın.

## 🔐 Güvenlik

API örnek olarak `bearerAuth` tanımını içermektedir. Gerçek kimlik doğrulama mekanizması uygulanmamıştır.
