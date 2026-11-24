---
project_outline: "[[01-project-outline]]"
title: "Smart Parking Garage Management System — Presentation 2"
text-scale: 100%
table-scale: 90%
---

<!-- @set-align center -->
<!-- @set-scale 100% -->
# Smart Parking Garage Management System

Specification and implementation plan

Author: **Umut Can Birbir**  
Neptun: **DUJ3ZD**  
Supervisor: **Anett LENART**  
Project ID: **2026-LA-04**

<!-- @note -->
> Bu sunum bir teknik taslak ve geliştirme planıdır. Henüz kurulum, kod veya ölçüm sonucu yok. Tamamlanmış işler yerine neyi, nasıl geliştirmeyi planladığını anlat.

---

<!-- @set-align left -->
<!-- @set-scale 100% -->
## Specification summary

- A database system with a small web interface.
- First MVP: search, reserve, view and cancel.
- Later work includes visits, fees and operator tools.
- Current stage: planning before implementation.

<!-- @note -->
> MVP, temel işlevleri çalışan ilk küçük sürüm demek. Sonraki işlevler kapsamdan çıkarılmadı. Abonelikler, deneme ödemeleri, bakım, raporlar ve değerlendirme sonraki aşamalarda da gerekli.

---

<!-- @set-align left -->
<!-- @set-scale 100% -->
## Main user journeys

1. The customer selects a garage and time interval.
2. The system searches for available spaces.
3. The customer chooses a vehicle and confirms.
4. The customer views or cancels an eligible booking.

<!-- @note -->
> Arama sonucu kesin yer garantisi değildir; kaydederken tekrar kontrol yapılacak. İlk başarı ölçütü: ara, rezervasyon yap, görüntüle ve başlangıçtan önce iptal et. Aynı anda çakışan ikinci rezervasyon reddedilmeli.

---

<!-- @set-align left -->
<!-- @set-scale 100% -->
## Main requirements

- Customers can access only their own records.
- Operators record vehicle entry and exit.
- The database calculates fees from the actual stay.
- Occupied spaces and maintenance block conflicting use.

<!-- @note -->
> Görevli girişte park ziyaretini açar, çıkışta kapatır. Veritabanı park yeri durumunu ve ilgili kayıtları birlikte günceller. Ücret, girişte geçerli tarife ve gerçek süreyle hesaplanır; uygun abonelik dikkate alınır. Çıkış ve deneme ödeme kaydı ayrı işlemlerdir. Süresini aşan araç çıkmadan aynı yere sonraki fiziksel giriş yapılamaz.

---

<!-- @set-align left -->
<!-- @set-scale 100% -->
## Initial technical proposal

- Oracle Database with SQL and PL/SQL.
- Python and FastAPI for the application layer.
- python-oracledb for database access.
- Simple HTML pages with CSS and Jinja2.

<!-- @note -->
> Bunlar önerilen teknolojiler; kurulum yapılmış değil. PL/SQL, Oracle içinde iş kuralları yazmak için kullanılacak. FastAPI ekranlarla veritabanı arasındaki küçük uygulama katmanı. Jinja2, Python tarafında HTML sayfaları oluşturacak. Kaynaklar: [Specification](./02-specification.md), [python-oracledb](https://python-oracledb.readthedocs.io/en/latest/user_guide/installation.html), [FastAPI templates](https://fastapi.tiangolo.com/advanced/templates/).

---

<!-- @set-align left -->
<!-- @set-scale 100% -->
## Architecture and responsibilities

| Layer | Responsibility |
| --- | --- |
| Web pages | Forms, results and feedback |
| FastAPI | User identity and database calls |
| Oracle / PL/SQL | Rules, transactions and stored data |

<!-- @note -->
> Müşteri formu doldurur, FastAPI kullanıcının kimliğini doğrular ve PL/SQL işlevini çağırır. Veritabanı kural kontrollerini ve veri değişikliklerini yapar. Servis, başarılı işlemde commit, hatada rollback yapar. Yani değişikliklerin tamamı kaydedilir veya tamamı geri alınır. Tarayıcı veritabanına doğrudan bağlanmaz. Kaynak: [Specification, section 8](./02-specification.md).

---

<!-- @set-align left -->
<!-- @set-scale 100% -->
## Data model proposal

- 19 related tables in the initial proposal.
- Garages contain floors and parking spaces.
- Vehicles link customers to reservations and visits.
- Keys and constraints protect data relationships.

<!-- @note -->
> 19 tablo mevcut belge önerisidir, oluşturulmuş tablolar değil. Diğer gruplar: hesap/rol, tarifeler, abonelikler, ödeme, bakım ve geçmiş kayıtları. Ayrıntılı ERD'de alanlar, anahtarlar ve ilişkinin çoklukları belirlenecek; en az üçüncü normal form açıklanacak. Amaç aynı bilgiyi gereksiz yere tekrar etmemek. Bir park olayı ilgili rezervasyona bağlıdır. Kaynak: [Specification, section 8.3](./02-specification.md).

---

<!-- @set-align left -->
<!-- @set-scale 100% -->
## Planned screens

- Search: garage, dates and available spaces.
- Confirmation: selected space, vehicle and booking.
- My reservations: details and cancellation.
- Operator: occupancy, entry/exit and reports.

<!-- @note -->
> Bunlar planlanan ana ekranlar; çalışan arayüz veya tamamlanmış prototip değil. Basit metin wireframe'leri specification bölüm 5'te bulunuyor. Müşterinin araç ve geçmiş sayfaları, görevlinin bakım ve deneme ödeme işlemleri de sonraki kapsamın parçası. Kaynak: [UI wireframes](./02-specification.md#5-user-interface-and-workflow).

---

<!-- @set-align left -->
<!-- @set-scale 100% -->
## Reservation safety

- Lock the selected space during booking.
- Recheck availability before saving.
- Save the whole operation or undo it.
- Compare two transaction approaches in tests.

<!-- @note -->
> Örnek: iki kişi aynı yeri aynı saate ayırmak isterse ikisi de başarılı olmamalı. İlk aday ortak araç/park yeri koruma kayıtlarında açık satır kilitleme; ikinci aday aynı koruma kayıtlarını güncelleyen SERIALIZABLE işlemler. Yalnızca SERIALIZABLE seçmek veya yalnızca arama anında kontrol etmek yeterli çözüm sayılmıyor. Her iki yaklaşım test edilecek; henüz kazanan veya performans sonucu yok. Kilitleme hatası, zaman aşımı ve iptal/bakım yarışları da denenecek. Kaynak: [Specification, section 8.4](./02-specification.md).

---

<!-- @set-align left -->
<!-- @set-scale 100% -->
## Testing and evaluation plan

- Test workflows, permissions and failed operations.
- Check conflicting bookings from parallel clients.
- Generate 100,000+ reservations and 100,000+ events.
- Prepare 12 queries and measure 5 optimizations.

<!-- @note -->
> Bunlar hedefler, elde edilmiş sonuçlar değil. Ayrı ayrı 100 bin rezervasyon ve 100 bin park olayı bizim mevcut belge hedefimiz. Aynı sabit başlangıç değeriyle test verisi yeniden üretilebilecek. Beş sorgunun iyileştirme öncesi/sonrası süreleri, okuma miktarları ve çalışma planları karşılaştırılacak. İki işlem yaklaşımı için doğruluk, gecikme ve işlem kapasitesi ölçülecek. Kaynak: [Specification, sections 6 and 8](./02-specification.md).

---

<!-- @set-align left -->
<!-- @set-scale 100% -->
## Semester-2 implementation plan

- **Weeks 1–2:** Verify Oracle and the Python connection.
- **Weeks 3–4:** Complete the ERD and schema scripts.
- **Weeks 5–6:** Build and test the reservation MVP.

<!-- @scale 85% -->
Proposed schedule, subject to course dates and feedback.

<!-- @note -->
> 14 haftalık toplam plan bizim çalışma varsayımımız; okulun zorunlu haftaları değil. İlk aşama kabulü: bir sorgu ve bir PL/SQL çağrısı. Tasarım kabulü: ilişkileri ve kısıtları belirli, yeniden kurulabilir şema ve 3NF açıklaması. İlk MVP kabulü: ara, ayır, görüntüle, iptal et; rakip rezervasyonu güvenle reddet. Test hesapları ve araçlar başlangıçta önceden hazırlanabilir.

---

<!-- @set-align left -->
<!-- @set-scale 100% -->
## Later milestones

- **Weeks 7–8:** Entry/exit and fee calculation.
- **Weeks 9–10:** Subscriptions, payments and maintenance.
- **Weeks 11–12:** Reports, test data and benchmarks.
- **Weeks 13–14:** Improvements, fixes and documentation.

<!-- @note -->
> Testler her aşamada yapılacak; yalnızca son haftalarda başlamayacak. Görevli ekranları ilgili işlevlerle birlikte geliştirilecek. Son aşamada ölçümler tekrarlanacak, temiz kurulum ve test yönergeleri yazılacak. Dönem takvimine göre danışmanla öncelikleri güncelleyeceğiz; zorunlu kapsamı kendiliğimizden çıkarmayacağız. Karmaşık görseller ve isteğe bağlı ekler öncelik değil.

---

<!-- @set-align left -->
<!-- @set-scale 100% -->
## Open risks and next steps

- Verify Oracle access and driver compatibility.
- Confirm entry and pricing policies with the supervisor.
- Review the design and refine the schedule.
- Set up GitHub Projects and begin the first milestone.

<!-- @note -->
> Kurulum/sürüm uyumu ilk teknik risk. Rezervasyonsuz giriş ve fiyat/giriş ayrıntıları açık kararlar: mevcut ilk akış rezervasyonlu; danışman onayı yok. Ortam kısıtları ve paralel işlem performansı erken denemelerle incelenecek. Kamera/bariyer, gerçek ödeme, mobil uygulama ve 3D kapsam dışı kalıyor. Eski belgelerdeki Trello alanları da GitHub Projects bağlantısı alındığında tutarlı biçimde güncellenmeli. İlgili kaynaklar: [Outline](./01-project-outline.md), [Specification](./02-specification.md).
