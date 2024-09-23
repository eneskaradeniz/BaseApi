# BaseApi
Modern web uygulamaları için tasarlanmış, .NET 8 ile oluşturulmuş esnek ve ölçeklenebilir bir temel API projesidir. authentication, authorization, logging, caching, file storage, message queue, real-time notifications gibi çeşitli temel özellikleri içerir.

# Teknolojiler

* .NET 8.0
* Microsoft SQL Server
* Entity Framework 8.0
* LINQ
* MediatR
* FluentValidation
* MassTransit
* AWSSDK.S3
* Serilog / Seq
* Swagger
* Docker

# Clean Architecture
Clean architecture, uygulamamızın bağımlıklarının tek yönlü ve içe doğru olmasını savunan bir yazılım mimarisidir.

### Domain
Tüm varlıkları (entities), değer nesnelerini (value objects), enumları, arayüzleri ve domaine özgü iş mantığını içerir. Sistemdeki hiçbir diğer katmana bağımlı değildir.

### Contracts
Katmanlar arasındaki bağımlılığı azaltmak için kullanılır. Application katmanı arasında iletişim kurmak için kullanılan DTO'lar, request-response modelleri gibi veri yapıları içerir.

### Application
Uygulama mantığını ve gerekli kullanım senaryolarını düzenlemekten sorumludur. Domain ve Contracts dışında başka katmanlara bağlı değildir.

Bu katman, uygulama mantığını desteklemek için gereken ve dış katmanlar tarafından kullanılan ek arayüzleri tanımlar. Örneğin **_IDbContext_** arayüzü bu katmanda tanımlanır ancak Persistence katmanı tarafından uygulanır.

Bu katman, uygulama mantığını komutlar (commands) ve sorgular (queries) olarak yapılandırmak için **CQRS desenini** kullanır ve bu amaçla MediatR kütüphanesini kullanır.

### Persistence
Veritabanı işlemlerini ve veri yönetimini gerçekleştiren katmandır. Bu katman, varlıklar (entities) için EF Core konfigürasyonlarını içerir, uygulamanın veritabanı bağlamını (context) uygular ve bazı kalıcıkla ilgili bağımlılıkları yapılandırır.

### Infrastructure
Dış kaynaklara erişmekle görevli sınıfları içerir. Bu sınıflar, application katmanında tanımlanan arayüzlere dayanır. Mevcut sistemde:
* Caching (Redis)
* Message Queue (RabbitMQ)
* Storage (AWS S3)
* Token (JWT)
* Email
* Cryptography

servislerini barındırır.

### Api
Tüm sistemi bir araya getirmekten sorumludur. Bu katmanın tek işlevi, HTTP isteklerini kabul etmek, bu istekleri komut veya sorgu olarak paketlemek, sistemin başka bir yerine göndererek işlenmesini sağlamak ve ardından sonucu yanıt olarak geri döndürmektir. Controller'lar olabildğince basit ve ince bir yapıda olacak şekilde tasarlanmıştır.

# Swagger UI
![Ekran görüntüsü 2024-09-23 161804](https://github.com/user-attachments/assets/00632dd2-fbd9-4f24-ae74-b899c1933137)

# Teşekkürler

Bu projeyi tasarlarken, **Gençay Yıldız** ve **Milan Jovanović**'in değerli eğitimlerinden öğrendiklerim için kendilerine teşekkür ederim.
