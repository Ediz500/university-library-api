# OpenAPI Tasarımı Ödevi Teslim Raporu

## 👤 Öğrenci Bilgileri

- **Ad Soyad**: Ediz Engin
- **Öğrenci Numarası**: 170422039

---

## 📂 OpenAPI YAML Dosyası

```yaml
openapi: 3.0.1
info:
  title: University Online Library API
  description: This API is designed for managing an online library system at a university.
  version: 1.0.0
servers:
  - url: "http://localhost:8080/api"
    description: Local server

paths:
  /books:
    get:
      summary: Get all books
      description: Retrieve a list of all books with pagination.
      parameters:
        - name: page
          in: query
          description: The page number to retrieve.
          required: false
          schema:
            type: integer
            default: 1
        - name: size
          in: query
          description: The number of books per page.
          required: false
          schema:
            type: integer
            default: 10
      responses:
        "200":
          description: A list of books.
          content:
            application/json:
              schema:
                type: object
                properties:
                  page:
                    type: integer
                  size:
                    type: integer
                  total:
                    type: integer
                  data:
                    type: array
                    items:
                      $ref: "#/components/schemas/Book"
        "400":
          description: Bad request
        "500":
          description: Server error

    post:
      summary: Add a new book
      description: Create a new book record.
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: "#/components/schemas/Book"
      responses:
        "201":
          description: Book created successfully
        "400":
          description: Invalid input data

  /books/{id}:
    get:
      summary: Get a book by ID
      description: Retrieve the details of a specific book by its ID.
      parameters:
        - name: id
          in: path
          description: The ID of the book to retrieve.
          required: true
          schema:
            type: string
      responses:
        "200":
          description: A single book.
          content:
            application/json:
              schema:
                $ref: "#/components/schemas/Book"
        "404":
          description: Book not found

    put:
      summary: Update a book by ID
      description: Update the details of an existing book.
      parameters:
        - name: id
          in: path
          description: The ID of the book to update.
          required: true
          schema:
            type: string
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: "#/components/schemas/Book"
      responses:
        "200":
          description: Book updated successfully
        "400":
          description: Invalid input data
        "404":
          description: Book not found

    delete:
      summary: Delete a book by ID
      description: Remove a book from the library.
      parameters:
        - name: id
          in: path
          description: The ID of the book to delete.
          required: true
          schema:
            type: string
      responses:
        "200":
          description: Book deleted successfully
        "404":
          description: Book not found

  /students:
    get:
      summary: Get all students
      description: Retrieve a list of all students.
      responses:
        "200":
          description: A list of students.
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: "#/components/schemas/Student"
        "500":
          description: Server error

    post:
      summary: Add a new student
      description: Create a new student record.
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: "#/components/schemas/Student"
      responses:
        "201":
          description: Student created successfully
        "400":
          description: Invalid input data

  /students/{id}:
    get:
      summary: Get a student by ID
      description: Retrieve the details of a specific student by their ID.
      parameters:
        - name: id
          in: path
          description: The ID of the student to retrieve.
          required: true
          schema:
            type: string
      responses:
        "200":
          description: A single student.
          content:
            application/json:
              schema:
                $ref: "#/components/schemas/Student"
        "404":
          description: Student not found

    put:
      summary: Update a student by ID
      description: Update the details of an existing student.
      parameters:
        - name: id
          in: path
          description: The ID of the student to update.
          required: true
          schema:
            type: string
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: "#/components/schemas/Student"
      responses:
        "200":
          description: Student updated successfully
        "400":
          description: Invalid input data
        "404":
          description: Student not found

    delete:
      summary: Delete a student by ID
      description: Remove a student from the system.
      parameters:
        - name: id
          in: path
          description: The ID of the student to delete.
          required: true
          schema:
            type: string
      responses:
        "200":
          description: Student deleted successfully
        "404":
          description: Student not found

  /loans:
    get:
      summary: Get all loans
      description: Retrieve a list of all loan records.
      responses:
        "200":
          description: A list of loan records.
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: "#/components/schemas/Loan"
        "500":
          description: Server error

    post:
      summary: Loan a book
      description: Loan a book to a student.
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: "#/components/schemas/Loan"
      responses:
        "201":
          description: Loan created successfully
        "400":
          description: Invalid input data

  /loans/{id}:
    get:
      summary: Get a loan by ID
      description: Retrieve a specific loan record by its ID.
      parameters:
        - name: id
          in: path
          description: The ID of the loan to retrieve.
          required: true
          schema:
            type: string
      responses:
        "200":
          description: A single loan record.
          content:
            application/json:
              schema:
                $ref: "#/components/schemas/Loan"
        "404":
          description: Loan not found

    patch:
      summary: Return a loaned book
      description: Mark a book as returned.
      parameters:
        - name: id
          in: path
          description: The ID of the loan to update.
          required: true
          schema:
            type: string
      responses:
        "200":
          description: Loan status updated to returned
        "400":
          description: Invalid loan ID
        "404":
          description: Loan not found

components:
  schemas:
    Book:
      type: object
      required:
        - title
        - author
        - isbn
        - publisher
        - pageCount
        - stock
      properties:
        id:
          type: string
          format: uuid
        title:
          type: string
        author:
          type: string
        isbn:
          type: string
          pattern: '^\d{3}-\d{1,5}-\d{1,7}-\d{1,7}-\d{1}$'
        publisher:
          type: string
        pageCount:
          type: integer
        stock:
          type: integer

    Student:
      type: object
      required:
        - name
        - studentNumber
        - email
        - isActive
      properties:
        id:
          type: string
          format: uuid
        name:
          type: string
        studentNumber:
          type: string
        email:
          type: string
          format: email
        isActive:
          type: boolean

    Loan:
      type: object
      required:
        - studentId
        - bookId
        - loanDate
        - status
      properties:
        id:
          type: string
          format: uuid
        studentId:
          type: string
          format: uuid
        bookId:
          type: string
          format: uuid
        loanDate:
          type: string
          format: date
        returnDate:
          type: string
          format: date
          nullable: true
        status:
          type: string
          enum:
            - ongoing
            - returned
            - late
```

---

### 🔗 GitHub Repo Linki

[https://github.com/Ediz500/university-library-api](https://github.com/Ediz500/university-library-api)

---

## 📝 API Açıklaması

Aşağıda tasarladığınız API’nin genel yapısını ve önemli noktalarını açıklayınız:

- **Hangi varlıklar (entities) yer almaktadır?**
  - **Book**: Kitaplar hakkında bilgiler (başlık, yazar, ISBN, yayınevi, sayfa sayısı, stok durumu).
  - **Student**: Öğrenciler hakkında bilgiler (isim, öğrenci numarası, e-posta, aktiflik durumu).
  - **Loan**: Kitap ödünç verme işlemleri (öğrenci ID'si, kitap ID'si, ödünç alma tarihi, durum).
- **CRUD işlemleri hangi endpoint’lerle sağlanmaktadır?**

  - **/books**:
    - `GET`: Kitapların listesini alır.
    - `POST`: Yeni kitap ekler.
  - **/books/{id}**:
    - `GET`: Belirli bir kitabı ID ile alır.
    - `PUT`: Kitap bilgilerini günceller.
    - `DELETE`: Kitap siler.
  - **/students**:
    - `GET`: Öğrencilerin listesini alır.
    - `POST`: Yeni öğrenci ekler.
  - **/students/{id}**:
    - `GET`: Belirli bir öğrenciyi ID ile alır.
    - `PUT`: Öğrenci bilgilerini günceller.
    - `DELETE`: Öğrenci siler.
  - **/loans**:
    - `GET`: Ödünç işlemlerinin listesini alır.
    - `POST`: Kitap ödünç verir.
  - **/loans/{id}**:
    - `GET`: Belirli bir ödünç işlemini ID ile alır.
    - `PATCH`: Kitap iade durumunu günceller.

- **`components/schemas`, `parameters`, `responses` gibi bölümleri nasıl kullandınız?**

  - **components/schemas**: API'deki varlıkların (Book, Student, Loan) şemalarını tanımladım. Bu, her bir varlık için gereken alanları (örneğin, başlık, yazar, ISBN gibi) ve veri türlerini belirtir.
  - **parameters**: API uç noktalarındaki parametreler tanımlandı. Örneğin, `GET /books` endpoint'inde sayfalama için `page` ve `size` parametreleri kullanıldı.
  - **responses**: API uç noktalarındaki yanıtlar tanımlandı. Başarılı bir işlem (`200`), kaynak bulunamadığında dönen yanıt (`404`), hatalı bir istek (`400`) gibi farklı durumlar için uygun yanıtlar belirledim.

- **Sayfalama ve hata durumları nasıl ele alındı?**
  - **Sayfalama**: `GET /books` endpoint'inde sayfalama sağlandı. `page` ve `size` parametreleri ile hangi sayfa ve sayfa başına kaç kitap döneceği belirlenebilir. Bu parametreler opsiyoneldir, varsayılan olarak 1. sayfa ve 10 kitap döner.
  - **Hata Durumları**: Hatalı isteklerde, örneğin eksik veya yanlış veri sağlandığında, API `400` hata kodu döndürür. Eğer istenen kaynak bulunamazsa, `404` yanıtı verilir. Sunucu hatalarında ise `500` yanıtı döner.

---

## 🧪 Test Notları

Swagger Editor üzerinden test ettiğiniz örnek istek/yanıtları özetleyebilirsiniz:

- **`GET /books`** çağrısında ne döner?
  - Bu çağrı, kitapların listelendiği bir JSON yanıtı döner. Yanıt, kitapların sayfalama verilerini (toplam kitap sayısı, mevcut sayfa vb.) içerir.
- **`POST /students`** için örnek `requestBody` nedir?

  - Yeni bir öğrenci eklemek için kullanılan `requestBody` şu şekilde olabilir:
    ```json
    {
      "name": "Ediz Engin",
      "studentNumber": "170422039",
      "email": "ediz@ediz500.com",
      "isActive": true
    }
    ```

- **Hatalı bir istek için dönen `400` örneği var mı?**
  - Evet, örneğin eksik veri sağlandığında, örneğin `POST /students` çağrısında öğrenci adı verilmediğinde API `400` hata kodu ile döner ve geçersiz giriş mesajı verir.

---

## 📌 Ek Açıklamalar

Varsa proje hakkında ekstra notlarınızı buraya ekleyebilirsiniz.
